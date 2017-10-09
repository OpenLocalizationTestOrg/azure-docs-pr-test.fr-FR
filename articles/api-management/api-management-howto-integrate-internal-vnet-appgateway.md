---
title: "aaaHow toouse gestion des API Azure dans un réseau virtuel avec la passerelle d’Application | Documents Microsoft"
description: "Découvrez comment toosetup et configurer la gestion des API Azure dans un réseau virtuel interne avec Application Gateway (WAF) en tant que serveur frontal"
services: api-management
documentationcenter: 
author: solankisamir
manager: kjoshi
editor: antonba
ms.assetid: a8c982b2-bca5-4312-9367-4a0bbc1082b1
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2017
ms.author: sasolank
ms.openlocfilehash: 74303a2ee8a10db633ab1740ec7267728eacb473
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-api-management-in-an-internal-vnet-with-application-gateway"></a>Intégrer le service Gestion des API dans un réseau virtuel interne avec Application Gateway 

##<a name="overview"></a> Vue d'ensemble
 
service de gestion des API de Hello peut être configuré dans un réseau virtuel en mode interne, ce qui le rend accessible uniquement à partir de hello réseau virtuel. La passerelle Azure Application Gateway est un service PAAS qui propose un équilibreur de charge de couche 7. Il agit comme un service proxy inverse et fournit dans son offre un pare-feu d’applications web (WAF).

Combinaison de gestion des API configuré dans un réseau interne avec un serveur frontal de passerelle d’Application hello permet hello les scénarios suivants :

* Utilisez hello même ressource de gestion des API pour la consommation par les consommateurs internes et externes aux consommateurs.
* Utilisez une seule ressource de gestion des API et mettez à disposition un sous-ensemble d’API défini dans la gestion des API pour les consommateurs externes.
* Fournir un accès tooAPI gestion de clés en main moyen tooswitch de hello Internet public et désactiver. 

##<a name="scenario"></a> Scénario
Cet article couvre comment toouse un unique de gestion des API de service par les utilisateurs internes et externes et rendre agissent comme un seul serveur frontal pour à la fois localement et dans le cloud d’API. Vous verrez également comment tooexpose uniquement un sous-ensemble de votre API (dans l’exemple hello qu’ils sont mis en surbrillance en vert) pour la consommation externe à l’aide de la fonctionnalité de PathBasedRouting hello disponible dans la passerelle d’Application.

Dans le premier exemple de programme d’installation hello tous vos API sont gérés uniquement à partir de votre réseau virtuel. Les consommateurs internes (mis en surbrillance en orange) peuvent accéder à toutes vos API internes et externes. Le trafic est jamais tooInternet qu'une haute performance est remis via des circuits Expressroute.

![itinéraire d’URL](./media/api-management-howto-integrate-internal-vnet-appgateway/api-management-howto-integrate-internal-vnet-appgateway.png)

## <a name="before-you-begin"></a> Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Créez un réseau virtuel et des sous-réseaux distincts pour le service Gestion des API et Application Gateway. 
3. Si vous envisagez de toocreate un serveur DNS personnalisé pour hello réseau virtuel, le faire avant de commencer le déploiement de hello. Vérifiez qu’il fonctionne en garantissant une machine virtuelle créée dans un nouveau sous-réseau Bonjour réseau virtuel peut résoudre et accéder à tous les points de terminaison de service Azure.

## <a name="what-is-required-toocreate-an-integration-between-api-management-and-application-gateway"></a>Qu’est requis toocreate une intégration entre la gestion des API et la passerelle d’Application ?

* **Pool de serveur principal :** hello interne adresse IP virtuelle de hello service de gestion des API.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont appliqués tooall des serveurs au sein du pool de hello.
* **Port frontal :** hello port public qui est ouvert sur la passerelle d’application hello. Le trafic en appuyant sur elle obtient tooone redirigé Hello serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie un pool de serveur principal tooa écouteur.
* **Sonde d’intégrité personnalisé :** passerelle d’Application, par défaut, utilise toofigure de sondes en fonction des adresses IP quels serveurs Bonjour BackendAddressPool sont actifs. Hello service de gestion des API répond uniquement toorequests qui présentent l’en-tête d’hôte correct hello, par conséquent, les sondes par défaut de hello échouent. Une sonde d’intégrité personnalisé doit toobe défini passerelle d’application toohelp déterminer que hello service est actif et il doit transférer les demandes.
* **Certificat de domaine personnalisé :** tooaccess gestion des API de hello internet, vous devez toocreate un mappage CNAME de son nom DNS nom d’hôte toohello passerelle d’Application frontale. Cela garantit qu’en-tête de nom d’hôte hello et certificat envoyé tooApplication passerelle est transféré tooAPI gestion une QU'APIM peut reconnaître comme valide.

## <a name="overview-steps"></a> Étapes requises pour l’intégration de la gestion des API et d’Application Gateway 

1. Créer un groupe de ressources pour Resource Manager
2. Créer un réseau virtuel, un sous-réseau et une adresse IP publique pour hello passerelle d’Application. Créer un autre sous-réseau pour le service Gestion des API
3. Créer un service de gestion des API à l’intérieur du sous-réseau de réseau virtuel hello créé ci-dessus et assurez-vous que vous utilisez le mode interne hello.
4. Le programme d’installation de nom de domaine personnalisé hello Bonjour service de gestion des API.
5. Créer un objet de configuration de passerelle Application Gateway
6. Créer une ressource Application Gateway
7. Créer un enregistrement CNAME à partir de hello nom DNS public du nom d’hôte du serveur proxy de gestion des API toohello hello passerelle d’Application.

## <a name="create-a-resource-group-for-resource-manager"></a>Créer un groupe de ressources pour Resource Manager

Assurez-vous que vous utilisez la version la plus récente d’Azure PowerShell hello. Pour plus d’informations, voir [Utilisation de Windows PowerShell avec Azure Resource Manager](../powershell-azure-resource-manager.md).

### <a name="step-1"></a>Étape 1

Connectez-vous à tooAzure

```powershell
Login-AzureRmAccount
```

Authentifiez-vous à l’aide de vos informations d’identification.<BR>

### <a name="step-2"></a>Étape 2

Vérifiez les abonnements hello pour le compte de hello et sélectionnez-le.

```powershell
Get-AzureRmSubscription -Subscriptionid "GUID of subscription" | Select-AzureRmSubscription
```

### <a name="step-3"></a>Étape 3 :

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).

```powershell
New-AzureRmResourceGroup -Name "apim-appGw-RG" -Location "West US"
```
Azure Resource Manager requiert que tous les groupes de ressources spécifient un emplacement. Cela est utilisé comme emplacement par défaut de hello pour les ressources dans ce groupe de ressources. Assurez-vous que toutes les commandes toocreate un hello d’utilisation de passerelle application même groupe de ressources.

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello

Bonjour à l’exemple suivant montre comment un réseau virtuel à l’aide de toocreate hello Gestionnaire de ressources.

### <a name="step-1"></a>Étape 1

Affecter hello adresse plage 10.0.0.0/24 toohello sous-réseau variable toobe utilisé pour la passerelle d’Application lors de la création d’un réseau virtuel.

```powershell
$appgatewaysubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim01" -AddressPrefix "10.0.0.0/24"
```

### <a name="step-2"></a>Étape 2

Affecter hello adresse plage 10.0.1.0/24 toohello sous-réseau variable toobe utilisé pour la gestion de l’API lors de la création d’un réseau virtuel.

```powershell
$apimsubnet = New-AzureRmVirtualNetworkSubnetConfig -Name "apim02" -AddressPrefix "10.0.1.0/24"
```

### <a name="step-3"></a>Étape 3 :

Créer un réseau virtuel nommé **appgwvnet** dans le groupe de ressources **apim-appGw-RG** pour la région ouest des États-Unis hello à l’aide de hello préfixe 10.0.0.0/16 avec les sous-réseaux 10.0.0.0/24 et 10.0.1.0/24.

```powershell
$vnet = New-AzureRmVirtualNetwork -Name "appgwvnet" -ResourceGroupName "apim-appGw-RG" -Location "West US" -AddressPrefix "10.0.0.0/16" -Subnet $appgatewaysubnet,$apimsubnet
```

### <a name="step-4"></a>Étape 4

Attribuer une variable de sous-réseau pour les étapes suivantes de hello

```powershell
$appgatewaysubnetdata=$vnet.Subnets[0]
$apimsubnetdata=$vnet.Subnets[1]
```
## <a name="create-an-api-management-service-inside-a-vnet-configured-in-internal-mode"></a>Créer un service Gestion des API dans un réseau virtuel configuré en mode interne

Hello suivant montre comment toocreate un service de gestion des API dans un réseau virtuel configuré pour l’accès interne uniquement.

### <a name="step-1"></a>Étape 1
Créez un objet de réseau virtuel de gestion des API à l’aide de sous-réseau de hello $apimsubnetdata créé ci-dessus.

```powershell
$apimVirtualNetwork = New-AzureRmApiManagementVirtualNetwork -Location "West US" -SubnetResourceId $apimsubnetdata.Id
```
### <a name="step-2"></a>Étape 2
Créer un service de gestion des API à l’intérieur de hello réseau virtuel.

```powershell
$apimService = New-AzureRmApiManagement -ResourceGroupName "apim-appGw-RG" -Location "West US" -Name "ContosoApi" -Organization "Contoso" -AdminEmail "admin@contoso.com" -VirtualNetwork $apimVirtualNetwork -VpnType "Internal" -Sku "Developer"
```
Après hello ci-dessus commande réussit consultez trop[Configuration DNS requise service de gestion des API réseau virtuel interne tooaccess](api-management-using-with-internal-vnet.md#apim-dns-configuration) tooaccess il.

## <a name="set-up-a-custom-domain-name-in-api-management"></a>Configurer un nom de domaine personnalisé dans le service Gestion des API

### <a name="step-1"></a>Étape 1
Téléchargez le certificat de hello avec une clé privée pour le domaine de hello. Pour cet exemple, c’est `*.contoso.net`. 

```powershell
$certUploadResult = Import-AzureRmApiManagementHostnameCertificate -ResourceGroupName "apim-appGw-RG" -Name "ContosoApi" -HostnameType "Proxy" -PfxPath <full path too.pfx file> -PfxPassword <password for certificate file> -PassThru
```

### <a name="step-2"></a>Étape 2
Une fois que le certificat de hello est téléchargé, créer un objet de configuration de nom d’hôte pour le proxy de hello avec un nom d’hôte de `api.contoso.net`, comme le certificat d’exemple hello prévoit autorité hello `*.contoso.net` domaine. 

```powershell
$proxyHostnameConfig = New-AzureRmApiManagementHostnameConfiguration -CertificateThumbprint $certUploadResult.Thumbprint -Hostname "api.contoso.net"
$result = Set-AzureRmApiManagementHostnames -Name "ContosoApi" -ResourceGroupName "apim-appGw-RG" -ProxyHostnameConfiguration $proxyHostnameConfig
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Créer une adresse IP publique pour la configuration frontale de hello

Créer une ressource IP publique **publicIP01** dans le groupe de ressources **apim-appGw-RG** pour la région ouest des États-Unis hello.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -name "publicIP01" -location "West US" -AllocationMethod Dynamic
```

Une adresse IP est attribuée toohello passerelle d’application au démarrage du service de hello.

## <a name="create-application-gateway-configuration"></a>Créer une configuration de passerelle Application Gateway

Tous les éléments de configuration doivent être configurés avant de créer la passerelle d’application hello. Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.

### <a name="step-1"></a>Étape 1

Créez une configuration IP de passerelle Application Gateway nommée **gatewayIP01**. Au démarrage de la passerelle d’Application, il récupère une adresse IP du sous-réseau hello configuré et acheminer les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end. Gardez à l’esprit que chaque instance utilise une adresse IP unique.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name "gatewayIP01" -Subnet $appgatewaysubnetdata
```

### <a name="step-2"></a>Étape 2

Configurer les ports IP front-end hello pour le point de terminaison IP public hello. Ce port est le port hello qui les utilisateurs finaux se connectent à.

```powershell
$fp01 = New-AzureRmApplicationGatewayFrontendPort -Name "port01"  -Port 443
```
### <a name="step-3"></a>Étape 3 :

Configuration IP frontale de hello avec le point de terminaison IP public.

```powershell
$fipconfig01 = New-AzureRmApplicationGatewayFrontendIPConfig -Name "frontend1" -PublicIPAddress $publicip
```

### <a name="step-4"></a>Étape 4

Configurer le certificat de hello pour Application Gateway, hello utilisé toodecrypt et re-chiffrer le trafic hello en passant par.

```powershell
$cert = New-AzureRmApplicationGatewaySslCertificate -Name "cert01" -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

### <a name="step-5"></a>Étape 5

Créer l’écouteur HTTP hello pour hello passerelle d’Application. Affecter la configuration IP frontale de hello, le port et tooit du certificat ssl.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name "listener01" -Protocol "Https" -FrontendIPConfiguration $fipconfig01 -FrontendPort $fp01 -SslCertificate $cert
```

### <a name="step-6"></a>Étape 6

Créer un service de gestion des API de toohello sonde personnalisée `ContosoApi` le point de terminaison proxy domaine. chemin d’accès Hello `/status-0123456789abcdef` est un point de terminaison de contrôle d’intégrité par défaut hébergée sur tous les services de gestion des API hello. Définir `api.contoso.net` comme un toosecure de nom d’hôte de sonde personnalisée avec un certificat SSL.

> [!NOTE]
> nom d’hôte de Hello `contosoapi.azure-api.net` est le nom d’hôte proxy hello par défaut configuré lorsqu’un service nommé `contosoapi` est créé dans Azure publique. 
> 

```powershell
$apimprobe = New-AzureRmApplicationGatewayProbeConfig -Name "apimproxyprobe" -Protocol "Https" -HostName "api.contoso.net" -Path "/status-0123456789abcdef" -Interval 30 -Timeout 120 -UnhealthyThreshold 8
```

### <a name="step-7"></a>Étape 7

Téléchargez le certificat hello toobe utilisé sur les ressources de pool hello SSL activé le serveur principal. Il s’agit de hello même certificat que vous avez fournies à l’étape 4 ci-dessus.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name "whitelistcert1" -CertificateFile <full path too.cer file>
```

### <a name="step-8"></a>Étape 8

Configurer les paramètres de serveur principal HTTP pour hello passerelle d’Application. Définissez notamment une limite de délai d’expiration pour les demandes de serveur principal après laquelle elles sont annulées. Cette valeur est différente de délai d’attente de la sonde hello.

```powershell
$apimPoolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "apimPoolSetting" -Port 443 -Protocol "Https" -CookieBasedAffinity "Disabled" -Probe $apimprobe -AuthenticationCertificates $authcert -RequestTimeout 180
```

### <a name="step-9"></a>Étape 9

Configurer un pool d’adresses IP principal nommé **apimbackend** avec l’adresse IP virtuelle interne, hello adresse du service de gestion des API de hello créé ci-dessus.

```powershell
$apimProxyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "apimbackend" -BackendIPAddresses $apimService.StaticIPs[0]
```

### <a name="step-10"></a>Étape 10

Créez des paramètres pour un serveur principal factice (inexistant). Demandes tooAPI chemins d’accès que nous ne souhaitez pas tooexpose à partir de la gestion des API via une passerelle d’Application sera atteint ce serveur principal et de renvoyer l’erreur 404.

Configurez les paramètres HTTP pour les principaux factice hello.

```powershell
$dummyBackendSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name "dummySetting01" -Port 80 -Protocol Http -CookieBasedAffinity Disabled
```

Configurer un serveur principal factice **dummyBackendPool**, qui pointe l’adresse du nom de domaine complet tooa **dummybackend.com**. Cette adresse de nom de domaine complet n’existe pas dans le réseau virtuel de hello.

```powershell
$dummyBackendPool = New-AzureRmApplicationGatewayBackendAddressPool -Name "dummyBackendPool" -BackendFqdns "dummybackend.com"
```

Créer une règle de définition que hello passerelle d’Application utilisera par défaut qui pointe toohello inexistant principal **dummybackend.com** Bonjour réseau virtuel.

```powershell
$dummyPathRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "nonexistentapis" -Paths "/*" -BackendAddressPool $dummyBackendPool -BackendHttpSettings $dummyBackendSetting
```

### <a name="step-11"></a>Étape 11

Configurer les chemins d’accès de la règle URL pour les pools principaux hello. Cela permet de sélectionner uniquement certaines des hello API de gestion des API pour pouvoir être exposés toohello public. (Par exemple, pour `Echo API` (/echo/), `Calculator API` (/calc/), etc., rendez uniquement `Echo API` accessible à partir d’Internet). 

Hello exemple suivant crée une règle simple pour hello « / echo / » chemin d’accès routage du trafic toohello principal « apimProxyBackendPool ».

```powershell
$echoapiRule = New-AzureRmApplicationGatewayPathRuleConfig -Name "externalapis" -Paths "/echo/*" -BackendAddressPool $apimProxyBackendPool -BackendHttpSettings $apimPoolSetting
```

Si le chemin d’accès hello ne correspond pas à les règles de chemin d’accès hello nous souhaitons tooenable à partir de la gestion des API, règle hello configuration de mappage de chemin d’accès configure également un pool d’adresses principal par défaut nommé **dummyBackendPool**. Par exemple, http://api.contoso.net/calc/ * devient trop**dummyBackendPool** telle qu’elle est définie en tant que pool par défaut de hello pour le trafic sans correspondance.

```powershell
$urlPathMap = New-AzureRmApplicationGatewayUrlPathMapConfig -Name "urlpathmap" -PathRules $echoapiRule, $dummyPathRule -DefaultBackendAddressPool $dummyBackendPool -DefaultBackendHttpSettings $dummyBackendSetting
```

Hello ci-dessus étape garantit que les demandes uniquement pour le chemin d’accès hello « / echo » sont autorisés via hello passerelle d’Application. Tooother demandes Qu'api configurés dans la gestion des API lève des 404 erreurs à partir de la passerelle d’Application à partir de hello Internet. 

### <a name="step-12"></a>Étape 12

Créer un paramètre de règle pour le routage basé sur le chemin d’accès hello Application Gateway toouse URL.

```powershell
$rule01 = New-AzureRmApplicationGatewayRequestRoutingRule -Name "rule1" -RuleType PathBasedRouting -HttpListener $listener -UrlPathMap $urlPathMap
```

### <a name="step-13"></a>Étape 13

Configurer hello instances et de la taille de hello passerelle d’Application. Ici, nous utilisons hello [WAF SKU](../application-gateway/application-gateway-webapplicationfirewall-overview.md) pour renforcer la sécurité de hello ressource de gestion des API.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name "WAF_Medium" -Tier "WAF" -Capacity 2
```

### <a name="step-14"></a>Étape 14

Configurer WAF toobe en mode de « Prévention ».
```powershell
$config = New-AzureRmApplicationGatewayWebApplicationFirewallConfiguration -Enabled $true -FirewallMode "Prevention"
```

## <a name="create-application-gateway"></a>Créer une passerelle Application Gateway

Créer une passerelle d’Application avec tous les objets de configuration de hello de hello étapes précédentes.

```powershell
$appgw = New-AzureRmApplicationGateway -Name $applicationGatewayName -ResourceGroupName $resourceGroupName  -Location $location -BackendAddressPools $apimProxyBackendPool, $dummyBackendPool -BackendHttpSettingsCollection $apimPoolSetting, $dummyBackendSetting  -FrontendIpConfigurations $fipconfig01 -GatewayIpConfigurations $gipconfig -FrontendPorts $fp01 -HttpListeners $listener -UrlPathMaps $urlPathMap -RequestRoutingRules $rule01 -Sku $sku -WebApplicationFirewallConfig $config -SslCertificates $cert -AuthenticationCertificates $authcert -Probes $apimprobe
```

## <a name="cname-hello-api-management-proxy-hostname-toohello-public-dns-name-of-hello-application-gateway-resource"></a>CNAME hello gestion des API proxy nom d’hôte toohello nom DNS public du hello ressource de la passerelle d’Application

Après la création de la passerelle de hello, hello prochaine étape consiste tooconfigure hello frontal pour la communication. Lorsque vous utilisez une adresse IP publique, passerelle d’Application requiert un nom DNS affecté dynamiquement, ce qui ne peut pas être facilement toouse. 

Hello nom DNS de la passerelle d’Application doit être utilisé toocreate un enregistrement CNAME qui pointe le nom d’hôte proxy hello APIM (par exemple, `api.contoso.net` dans les exemples hello ci-dessus) nom DNS toothis. tooconfigure hello frontal enregistrement IP CNAME, récupérer les détails hello Hello passerelle d’Application et son nom IP/DNS associé à l’aide d’élément d’adresse IP publique hello. les utilisation de Hello d’enregistrements d’un n’est pas recommandée étant donné que l’adresse IP virtuelle hello peut changer lors du redémarrage de la passerelle.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName "apim-appGw-RG" -Name "publicIP01"
```

##<a name="summary"></a> Résumé
Gestion des API Azure configuré dans un réseau virtuel fournit une interface de passerelle unique pour toutes les API configurés, qu’ils soient hébergé localement ou dans le cloud de hello. Intégration de passerelle d’Application avec gestion des API souplesse hello d’activer de manière sélective particulier toobe API accessible sur Internet de hello, mais aussi en fournissant un pare-feu d’applications Web comme une instance de gestion des API de serveur frontal tooyour.

##<a name="next-steps"></a> Étapes suivantes
* En savoir plus sur Azure Application Gateway
  * [Vue d’ensemble d’Application Gateway](../application-gateway/application-gateway-introduction.md)
  * [Pare-feu d’applications web sur Application Gateway](../application-gateway/application-gateway-webapplicationfirewall-overview.md)
  * [Application Gateway à l’aide du routage basé sur le chemin](../application-gateway/application-gateway-create-url-route-arm-ps.md)
* En savoir plus sur le service Gestion des API et les réseaux virtuels
  * [À l’aide de la gestion des API disponible uniquement dans hello réseau virtuel](api-management-using-with-internal-vnet.md)
  * [Avec la gestion des API dans le réseau virtuel](api-management-using-with-vnet.md)
