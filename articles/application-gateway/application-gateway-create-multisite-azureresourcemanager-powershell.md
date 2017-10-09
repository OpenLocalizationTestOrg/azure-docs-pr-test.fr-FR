---
title: "une passerelle d’application pour l’hébergement de plusieurs sites d’aaaCreate | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurez une passerelle d’application Windows Azure pour héberger plusieurs applications web sur hello même passerelle."
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: b107d647-c9be-499f-8b55-809c4310c783
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/12/2016
ms.author: amsriva
ms.openlocfilehash: bad9a76be0a73a7026a770630fa7156f6e5940c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-for-hosting-multiple-web-applications"></a>Créer une passerelle Application Gateway pour l’hébergement de plusieurs applications web

> [!div class="op_single_selector"]
> * [portail Azure](application-gateway-create-multisite-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-multisite-azureresourcemanager-powershell.md)

Hébergement de plusieurs sites vous permet de toodeploy plus d’une application web sur hello même passerelle d’application. Il s’appuie sur la présence de l’en-tête d’hôte dans la requête HTTP entrante hello, toodetermine quels écouteur reçoit le trafic. écouteur de Hello dirige ensuite pool principal de tooappropriate trafic tel que configuré dans la définition des règles de passerelle de hello hello. Dans les applications web SSL est activé, passerelle d’application s’appuie sur hello Indication de nom de serveur (SNI) extension toochoose hello correct écouteur pour le trafic web hello. Une utilisation courante pour l’hébergement de plusieurs sites est équilibrer les demandes de tooload pour les pools de serveur principal toodifferent web différents domaines. De même, plusieurs sous-domaines de hello même domaine racine peut également être hébergé sur hello même passerelle d’application.

## <a name="scenario"></a>Scénario

Dans l’exemple suivant de hello, passerelle d’application sert le trafic pour contoso.com et fabrikam.com avec deux pools de serveur principal : contoso pool de serveurs et de pool de serveurs de fabrikam. Le programme d’installation similaire peut être sous-domaines toohost utilisés comme app.contoso.com et blog.contoso.com.

![imageURLroute](./media/application-gateway-create-multisite-azureresourcemanager-powershell/multisite.png)

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. les serveurs Hello ajouté passerelle d’application hello toohello principal pool toouse doit exister ou ont créé leurs points de terminaison dans le réseau virtuel de hello dans un sous-réseau distinct ou avec une adresse IP publique/VIP attribué.

## <a name="requirements"></a>Configuration requise

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique. Le nom de domaine complet peut également être utilisé.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL). Pour les passerelles Application Gateway activées pour plusieurs sites, le nom d’hôte et les indicateurs SNI sont également ajoutés.
* **La règle :** règle de hello lie écouteur hello, pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier. Les règles sont traitées dans l’ordre de hello qu’ils sont répertoriés, et le trafic est dirigé via hello première règle qui correspond, quelle que soit la spécificité. Par exemple, si vous disposez d’une règle à l’aide d’un écouteur de base et une règle à l’aide d’un écouteur de plusieurs site à la fois sur hello même règle de port, hello avec écouteur de plusieurs sites hello doit figurer avant les règle hello qu’un écouteur de base hello dans l’ordre pour toofunction de règle de plusieurs sites hello en tant que attendu.

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

Hello Voici les étapes de hello nécessaires toocreate une passerelle d’application :

1. Créer un groupe de ressources pour Resource Manager
2. Créer un réseau virtuel, des sous-réseaux et adresse IP publique pour la passerelle d’application hello.
3. Créer un objet de configuration de passerelle Application Gateway
4. Créez une ressource Application Gateway.

## <a name="create-a-resource-group-for-resource-manager"></a>Créer un groupe de ressources pour Resource Manager

Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello. Pour plus d’informations, voir l’article [Utilisation de Windows Powershell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Étape 1

Connectez-vous à tooAzure

```powershell
Login-AzureRmAccount
```
Vous êtes invité à tooauthenticate avec vos informations d’identification.

### <a name="step-2"></a>Étape 2

Vérifiez les abonnements hello pour le compte de hello.

```powershell
Get-AzureRmSubscription
```

### <a name="step-3"></a>Étape 3 :

Choisissez parmi vos toouse abonnements Azure.

```powershell
Select-AzureRmSubscription -Subscriptionid "GUID of subscription"
```

### <a name="step-4"></a>Étape 4

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).

```powershell
New-AzureRmResourceGroup -Name appgw-RG -location "West US"
```

Vous pouvez également créer des balises pour un groupe de ressources pour la passerelle Application Gateway :

```powershell
$resourceGroup = New-AzureRmResourceGroup -Name appgw-RG -Location "West US" -Tags @{Name = "testtag"; Value = "Application Gateway multiple site"}
```

Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cet emplacement est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.

Dans l’exemple hello ci-dessus, nous avons créé un groupe de ressources appelé **appgw-RG** avec un emplacement de **ouest des États-Unis**.

> [!NOTE]
> Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’application, consultez [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-ps.md). Consultez les informations sur les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md).

## <a name="create-a-virtual-network-and-subnets"></a>Créer un réseau virtuel et des sous-réseaux

Hello suivant montre l’exemple de comment toocreate un réseau virtuel à l’aide du Gestionnaire de ressources. Deux sous-réseaux sont créés au cours de cette étape. sous-réseau de première Hello est pour la passerelle d’application hello lui-même. Passerelle d’application nécessite son propre toohold sous-réseau ses instances. Seules d’autres passerelles Application Gateway peuvent être déployées dans ce sous-réseau. sous-réseau de deuxième Hello est utilisé toohold hello application back-end serveurs.

### <a name="step-1"></a>Étape 1

Assigner hello adresse plage 10.0.0.0/24 toohello sous-réseau toobe variable toohold utilisé hello application passerelle.

```powershell
$subnet = New-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -AddressPrefix 10.0.0.0/24
```
### <a name="step-2"></a>Étape 2

Affecter hello adresse plage 10.0.1.0/24 toohello subnet2 variable toobe les pools principaux hello.

```powershell
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -AddressPrefix 10.0.1.0/24
```

### <a name="step-3"></a>Étape 3 :

Créer un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello avec le sous-réseau 10.0.0.0/24, à l’aide de hello préfixe 10.0.0.0/16 et 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name appgwvnet -ResourceGroupName appgw-RG -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $subnet,$subnet2
```

### <a name="step-4"></a>Étape 4

Attribuer une variable de sous-réseau pour les étapes suivantes de hello, qui crée une passerelle d’application.

```powershell
$appgatewaysubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name appgatewaysubnet -VirtualNetwork $vnet
$backendsubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name backendsubnet -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Créer une adresse IP publique pour la configuration frontale de hello

Créer une ressource IP publique **publicIP01** dans le groupe de ressources **appgw-rg** pour la région ouest des États-Unis hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-RG -name publicIP01 -location "West US" -AllocationMethod Dynamic
```

Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.

## <a name="create-application-gateway-configuration"></a>Créer une configuration de passerelle Application Gateway

Vous avez tooset tous les éléments de configuration avant de créer la passerelle d’application hello. Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.

### <a name="step-1"></a>Étape 1

Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**. Au démarrage de la passerelle d’application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end. Gardez à l’esprit que chaque instance utilise une adresse IP unique.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name gatewayIP01 -Subnet $appgatewaysubnet
```

### <a name="step-2"></a>Étape 2

Configurer le pool d’adresses IP principal hello nommé **pool01** et **pool2** avec des adresses IP **134.170.185.46**, **134.170.188.221**, **134.170.185.50** pour **pool1** et **134.170.186.46**, **134.170.189.221**, **134.170.186.50**  pour **pool2**.

```powershell
$pool1 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool01 -BackendIPAddresses 10.0.1.100, 10.0.1.101, 10.0.1.102
$pool2 = New-AzureRmApplicationGatewayBackendAddressPool -Name pool02 -BackendIPAddresses 10.0.1.103, 10.0.1.104, 10.0.1.105
```

Dans cet exemple, il existe deux principaux pools tooroute le trafic réseau selon le site demandé de hello. Un pool reçoit le trafic du site « contoso.com » et l’autre le trafic du site « fabrikam.com ». Vous avez hello tooreplace précédant tooadd d’adresses IP de vos propres points de terminaison application IP adresse. À la place des adresses IP internes, vous pouvez également utiliser des adresses IP publiques, un nom de domaine complet ou une carte réseau d’une machine virtuelle pour les instances de backend. toospecify noms de domaine complets au lieu d’adresses IP dans PowerShell, utilisez «-BackendFQDNs » paramètre.

### <a name="step-3"></a>Étape 3 :

Configurer le paramètre de passerelle d’application **poolsetting01** et **poolsetting02** hello équilibrés en charge le trafic réseau dans le pool principal d’hello. Dans cet exemple, vous configurez les paramètres de pool principal différent pour les pools principaux hello. Chaque pool principal peut avoir son propre paramètre de pool principal.

```powershell
$poolSetting01 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled -RequestTimeout 120
$poolSetting02 = New-AzureRmApplicationGatewayBackendHttpSettings -Name "besetting02" -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 240
```

### <a name="step-4"></a>Étape 4

Configuration IP frontale de hello avec le point de terminaison IP public.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-5"></a>Étape 5

Configurer le port frontal de hello pour une passerelle d’application.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "fep01" -Port 443
```

### <a name="step-6"></a>Étape 6

Configurer les deux certificats SSL pour les sites Web de hello deux, nous allons toosupport dans cet exemple. Un seul certificat pour le trafic de contoso.com et hello autres est pour le trafic fabrikam.com. Il doit s’agir de certificats émis par une autorité de certification pour vos sites Web. Les certificats auto-signés sont pris en charge mais déconseillés pour le trafic de production.

```powershell
$cert01 = New-AzureRmApplicationGatewaySslCertificate -Name contosocert -CertificateFile <file path> -Password <password>
$cert02 = New-AzureRmApplicationGatewaySslCertificate -Name fabrikamcert -CertificateFile <file path> -Password <password>
```

### <a name="step-7"></a>Étape 7

Configurez les deux écouteurs pour les deux sites web de hello dans cet exemple. Cette étape configure les écouteurs hello pour public hôte, port et adresse IP utilisé tooreceive du trafic entrant. Paramètre de nom d’hôte est requis pour la prise en charge de plusieurs sites et doit être ensemble toohello site Web approprié pour le hello le trafic est reçu. RequireServerNameIndication paramètre doit être défini tootrue pour les sites Web à prendre en charge pour le protocole SSL dans un scénario à plusieurs hôtes. Si la prise en charge SSL est requis, vous devez également toospecify hello SSL certificat trafic toosecure utilisé pour cette application web. combinaison de Hello de configuration IP frontale, port du serveur frontal et de nom d’hôte doit être unique tooa écouteur. Chaque écouteur peut prendre en charge un seul certificat.

```powershell
$listener01 = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "contoso11.com" -RequireServerNameIndication true  -SslCertificate $cert01
$listener02 = New-AzureRmApplicationGatewayHttpListener -Name "listener02" -Protocol Https -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -HostName "fabrikam11.com" -RequireServerNameIndication true -SslCertificate $cert02
```

### <a name="step-8"></a>Étape 8

Créez deux règle définissant deux applications web pour hello dans cet exemple. Une règle associe les écouteurs, les pools principaux et les paramètres http. Cette étape configure hello application passerelle toouse base règle de routage, un pour chaque site Web. Site Web de tooeach le trafic est reçu par son écouteur configuré et est ensuite dirigé de tooits configuré pool principal, à l’aide des propriétés hello spécifiées dans hello serveur principal s’élève.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule01" -RuleType Basic -HttpListener $listener01 -BackendHttpSettings $poolSetting01 -BackendAddressPool $pool1
$rule02 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule02" -RuleType Basic -HttpListener $listener02 -BackendHttpSettings $poolSetting02 -BackendAddressPool $pool2
```

### <a name="step-9"></a>Étape 9

Configurer le nombre de hello d’instances et de taille pour la passerelle d’application hello.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "Standard_Medium" -Tier Standard -Capacity 2
```

## <a name="create-application-gateway"></a>Créer une passerelle Application Gateway

Créer une passerelle d’application avec tous les objets de configuration à partir de hello étapes précédentes.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgwtest -ResourceGroupName appgw-RG -Location "West US" -BackendAddressPools $pool1,$pool2 -BackendHttpSettingsCollection $poolSetting01, $poolSetting02 -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener01, $listener02 -RequestRoutingRules $rule01, $rule02 -Sku $sku -SslCertificates $cert01, $cert02
```

> [!IMPORTANT]
> Approvisionnement de passerelle d’application est une opération longue et peut prendre quelques toocomplete de temps.
> 
> 

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

Découvrez comment tooprotect vos sites Web avec [passerelle d’Application - pare-feu d’applications Web](application-gateway-webapplicationfirewall-overview.md)

