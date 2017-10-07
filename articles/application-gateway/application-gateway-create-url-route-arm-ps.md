---
title: "aaaCreate une passerelle d’application à l’aide de routage d’URL règles | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurez une passerelle d’application Windows Azure à l’aide des règles de routage d’URL"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d141cfbb-320a-4fc9-9125-10001c6fa4cf
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/03/2017
ms.author: gwallace
ms.openlocfilehash: 54fcccc39e48a933576968ce3d8160518c0d0b7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-using-path-based-routing"></a>Créer une passerelle Application Gateway à l’aide du routage basé sur le chemin

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-url-route-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-url-route-arm-ps.md)
> * [Azure CLI 2.0](application-gateway-create-url-route-cli.md)

Le routage basé sur le chemin d’accès URL permet d’itinéraires tooassociate vous selon le chemin d’URL de hello d’une requête Http. Il vérifie s’il existe un pool de back-end tooa itinéraire configuré pour hello les URL présentée dans hello passerelle d’Application. Il envoie ensuite toohello de trafic réseau hello défini par pool de back-end. Une utilisation courante pour le routage basé sur l’URL est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent différents types de contenu.

Le routage basé sur des URL introduit une nouvelle passerelle de tooapplication de type de règle. La passerelle Application Gateway comporte deux types de règles : une règle de base et PathBasedRouting. Type de règle de base fournit des service tourniquet pour les principaux hello pools lors PathBasedRouting en outre distribution Round robin de tooround, prend également le modèle de chemin d’accès de l’URL de demande hello en compte lors du choix du pool principal d’hello.

## <a name="scenario"></a>Scénario

Dans l’exemple suivant de hello, passerelle d’Application sert le trafic pour contoso.com avec deux pools de serveur principal : pool de serveurs vidéo et pool de serveurs d’image.

Les demandes d’http://contoso.com/image * sont acheminés pool de serveurs tooimage (pool1) et http://contoso.com/video * sont acheminés pool de serveurs toovideo (pool2). Si aucun des modèles de chemin d’accès hello correspondent, un pool de serveurs par défaut (pool1) est sélectionné.

![itinéraire d’URL](./media/application-gateway-create-url-route-arm-ps/figure1.png)

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Vous créez un réseau virtuel et un sous-réseau pour la passerelle Application Gateway. Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello. passerelle d’application Hello doit être par lui-même dans un sous-réseau de réseau virtuel.
3. les serveurs Hello ajouté passerelle d’application hello toohello principal pool toouse doit exister ou ont créé leurs points de terminaison dans le réseau virtuel de hello ou avec une adresse IP publique/VIP attribué.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Qu’est requis toocreate une passerelle d’application ?

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie écouteur hello, pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

Hello diffère entre l’utilisation classique Azure et Azure Resource Manager commande hello dans lequel vous créez passerelle d’application hello et articles hello toobe configuré.

Avec le Gestionnaire de ressources, tous les éléments qui rendent une passerelle d’application sont configurées individuellement et rassembler puis toocreate ressource de passerelle d’application hello.

Voici les étapes hello qui sont nécessaire toocreate une passerelle d’application :

1. Créer un groupe de ressources pour Resource Manager
2. Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour la passerelle d’application hello.
3. Créer un objet de configuration de passerelle Application Gateway
4. Créez une ressource Application Gateway.

## <a name="create-a-resource-group-for-resource-manager"></a>Créer un groupe de ressources pour Resource Manager

Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello. Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Étape 1

Connectez-vous à tooAzure

```powershell
Login-AzureRmAccount
```

Vous êtes invité à tooauthenticate avec vos informations d’identification.<BR>

### <a name="step-2"></a>Étape 2

Vérifiez les abonnements hello pour le compte de hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Étape 3 :

Choisissez parmi vos toouse abonnements Azure. <BR>

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Étape 4

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US"
```

Vous pouvez également créer des balises pour un groupe de ressources pour la passerelle Application Gateway :

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway URL routing"} 
```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Ce groupe de ressources est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.

Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé « appgw-RG » et l’emplacement « Ouest des États-Unis ».

> [!NOTE]
> Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’application, consultez [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md). Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .
> 
> 

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello

Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources. Cet exemple crée un réseau virtuel pour hello passerelle d’Application. Passerelle d’application nécessite son propre sous-réseau, c’est pourquoi sous-réseau hello créé pour hello passerelle d’Application est plus petit que hello espace d’adressage de réseau virtuel. Ainsi, pour les autres ressources, y compris mais non limité tooweb serveurs toobe dans hello même réseau virtuel.

### <a name="step-1"></a>Étape 1

Affecter hello adresse plage 10.0.0.0/24 toohello sous-réseau toobe variable utilisée toocreate un réseau virtuel.  Cela crée d’objet de configuration de sous-réseau hello pour hello passerelle d’Application, qui est utilisé dans l’exemple suivant de hello.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name subnet01 -AddressPrefix 10.0.0.0/24
```

### <a name="step-2"></a>Étape 2

Créer un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec le sous-réseau 10.0.0.0/24. Configuration de hello Hello réseau virtuel avec un sous-réseau unique pour tooreside de passerelle d’Application hello est terminée.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet
```

### <a name="step-3"></a>Étape 3 :

Attribuer variable de sous-réseau de hello hello pour les étapes suivantes, il est passé toohello `New-AzureRMApplicationGateway` applet de commande dans une étape ultérieure.

```powershell
$subnet=$vnet.Subnets[0]
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Créer une adresse IP publique pour la configuration frontale de hello

Créer une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello. Passerelle d’application peut utiliser une adresse IP publique, adresse IP interne ou les deux requêtes tooreceive pour l’équilibrage de charge.  Cet exemple utilise uniquement une adresse IP publique. Dans l’exemple suivant de hello, aucun nom DNS n’est configuré pour la création d’adresse IP publique de hello.  Application Gateway ne prend pas en charge de noms DNS personnalisés sur des adresses IP publiques.  Si un nom personnalisé est requis pour le point de terminaison public hello, un enregistrement CNAME doit être créé nom_DNS toopoint toohello généré automatiquement pour l’adresse IP publique de hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.

## <a name="create-application-gateway-configuration"></a>Créer une configuration de passerelle Application Gateway

Tous les éléments de configuration doivent être configurés avant de créer la passerelle d’application hello. Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.

### <a name="step-1"></a>Étape 1

Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**. Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end. Gardez à l’esprit que chaque instance utilise une adresse IP unique.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $subnet
```

### <a name="step-2"></a>Étape 2

Configurer le pool d’adresses IP principal hello nommé **pool01** et **pool2** avec des adresses IP pour **pool1** et **pool2**. Ces adresses IP sont des adresses IP de hello des ressources hello qui hébergent hello web application toobe protégé par la passerelle d’application hello. Ces membres du pool principal sont tous les toobe validé intègre par les sondes qu’ils soient sondes de base ou des sondes personnalisé.  Le trafic est alors acheminé toothem lorsque des demandes parviennent à la passerelle d’application hello. Pools principaux peuvent être utilisées par plusieurs règles au sein de la passerelle d’application hello, ce qui signifie un pool principal peut être utilisé pour plusieurs applications web qui résident sur hello même hôte.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 134.170.185.46, 134.170.188.221, 134.170.185.50

$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 134.170.186.47, 134.170.189.222, 134.170.186.51
```

Dans cet exemple, il existe deux principaux pools tooroute le trafic réseau selon le chemin d’URL de hello. Un pool reçoit le trafic du chemin d’URL « /video » et l’autre pool reçoit le trafic du chemin « /image ». Remplacez hello précédant tooadd d’adresses IP de vos propres points de terminaison application IP adresse. 

### <a name="step-3"></a>Étape 3 :

Configurer le paramètre de passerelle d’application **poolsetting01** et **poolsetting02** hello équilibrés en charge le trafic réseau dans le pool principal d’hello. Dans cet exemple, vous configurez les paramètres de pool principal différent pour les pools principaux hello. Chaque pool principal peut avoir son propre paramètre de pool principal.  Paramètres HTTP du serveur principal sont utilisées par les règles tooroute trafic toohello les membres du pool principal approprié. Ce paramètre détermine le protocole de hello et port qui est utilisé lors de l’envoi de trafic toohello les membres du pool principal. Sessions basées sur un cookie sont également déterminées par les paramètres HTTP hello principal.  S’il est activé, l’affinité de basé sur cookie de session envoie le trafic toohello même principal en tant que requêtes précédentes pour chaque paquet.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120

$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Étape 4

Configuration IP frontale de hello avec le point de terminaison IP public. objet de configuration IP frontale Hello est utilisé par un Bonjour de toorelate écouteur vers l’adresse IP qu’un écouteur hello extérieur.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Étape 5

Configurer le port frontal de hello pour une passerelle d’application. objet de configuration du port frontal Hello est utilisé par un toodefine écoute le port d’écoute de passerelle d’Application hello pour le trafic sur le port d’écoute hello.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 80
```

### <a name="step-6"></a>Étape 6

Configurer un écouteur de hello. Cette étape configure l’écouteur hello pour l’adresse IP publique de hello et le port utilisé tooreceive du trafic réseau entrant. Hello, l’exemple suivant prend une configuration IP frontale de hello précédemment configuré, la configuration de port frontal et un protocole (http ou https) et configure l’écouteur de hello. Dans cet exemple, port d’écoute hello écoute tooHTTP du trafic sur le port 80 sur l’adresse IP publique hello qui a été créé précédemment.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Http -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01
```

### <a name="step-7"></a>Étape 7

Configurer les chemins d’accès de la règle URL pour les pools principaux hello. Cette étape configure le chemin d’accès relatif hello utilisé par la passerelle d’application et définit le mappage hello entre le chemin d’accès des URL hello et pool principal hello qui reçoit le trafic entrant de toohandle hello.

> [!IMPORTANT]
> Chaque chemin d’accès doit commencer par / et hello uniquement une «\*» est autorisé, à la fin de hello. /xyz, /xyz* ou /xyz/* sont des exemples valides. Hello chaîne fed détecteur de chemin d’accès toohello n’inclut pas de texte après hello tout d’abord « ? » ou « # » et ces caractères ne sont pas autorisés. 

Hello exemple suivant crée deux règles : une pour le chemin d’accès « image / » routage du trafic tooback-end « pool1 » et une autre pour « video / » chemin d’accès de routage du trafic tooback-end « pool2 ». Ces règles vous assurer que le trafic pour chaque jeu d’URL est routé toohello principal. Par exemple, http://contoso.com/image/figure1.jpg devient toopool1 et http://contoso.com/video/example.mp4 devient toopool2.

```powershell
$imagePathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule1" -Paths "/image/*" -BackendAddressPool $pool1 -BackendHttpSettings $poolSetting01

$videoPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "pathrule2" -Paths "/video/*" -BackendAddressPool $pool2 -BackendHttpSettings $poolSetting02
```

Si le chemin d’accès hello ne correspond pas à une des règles de chemin d’accès prédéterminé hello, configuration de mappage de chemin d’accès de règle hello configure également un pool d’adresses principal par défaut. Par exemple, http://contoso.com/shoppingcart/test.html devient toopool1 telle qu’elle est définie en tant que pool par défaut de hello pour le trafic non apparié.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $videoPathRule, $imagePathRule -DefaultBackendAddressPool $pool1 -DefaultBackendHttpSettings $poolSetting02
```

### <a name="step-8"></a>Étape 8

Créez un paramètre de règle. Cette étape configure hello application passerelle toouse basée sur le chemin d’accès au routage d’URL. Hello `$urlPathMap` variable définie dans hello étape antérieure est maintenant utilisé toocreate hello chemin d’accès règle. Dans cette étape, nous associons règle de hello avec un écouteur et le mappage de chemin d’accès d’url hello créé précédemment.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-9"></a>Étape 9

Configurer le nombre de hello d’instances et de taille pour la passerelle d’application hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Small" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Créer une passerelle Application Gateway

Créer une passerelle d’application avec tous les objets de configuration à partir de hello étapes précédentes.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku
```

## <a name="get-application-gateway-dns-name"></a>Obtenir le nom DNS d’une passerelle Application Gateway

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, la passerelle Application Gateway requiert un nom DNS attribué dynamiquement, ce qui n’est pas convivial. les utilisateurs finaux de tooensure pouvez atteindre la passerelle d’application hello, un enregistrement CNAME peut être le point de terminaison utilisé toopoint toohello public de la passerelle d’application hello. [Configuration d’un nom de domaine personnalisé pour Azure](../cloud-services/cloud-services-custom-domain-name-portal.md). tooconfigure hello frontal enregistrement CNAME d’IP, de récupérer les détails de la passerelle d’application hello et son nom IP/DNS associé à l’aide de la passerelle d’application hello PublicIPAddress élément attaché toohello. nom DNS de la passerelle d’application Hello doit être utilisé toocreate un enregistrement CNAME. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle d’application.

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

Si vous souhaitez toolearn décharger de Secure Sockets Layer (SSL), consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl-arm.md).

