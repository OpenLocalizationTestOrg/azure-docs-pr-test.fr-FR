---
title: "aaaConfigure fin tooend SSL avec la passerelle d’Application Azure | Documents Microsoft"
description: "Cet article décrit comment tooconfigure fin tooend SSL avec la passerelle d’Application à l’aide de PowerShell du Gestionnaire de ressources Azure"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: e6d80a33-4047-4538-8c83-e88876c8834e
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: 7c280478e143d309e7665219441cbee8c81d9a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-end-tooend-ssl-with-application-gateway-using-powershell"></a>Configurer fin tooend SSL avec la passerelle d’Application à l’aide de PowerShell

## <a name="overview"></a>Vue d'ensemble

Prend en charge l’application passerelle fin tooend le chiffrement du trafic. Pour cela, passerelle d’application termine la connexion SSL de hello au niveau de la passerelle d’application hello. passerelle de Hello applique ensuite des règles de routage hello toohello trafic, rechiffre les paquets hello et transfère hello principal paquet toohello approprié en fonction des règles de routage hello définis. Une réponse de serveur web de hello traverse hello même processus utilisateur toohello précédent.

La passerelle Application Gateway prend également en charge la définition d’options SSL personnalisées. Passerelle d’application prend en charge la désactivation hello suivant la version de protocole ; **TLSv1.0**, **TLSv1.1**, et **TLSv1.2** ainsi définir hello suites toouse et hello l’ordre de préférence de chiffrement.  toolearn savoir plus sur les options SSL configurables, visitez [vue d’ensemble de la stratégie SSL](application-gateway-SSL-policy-overview.md).

> [!NOTE]
> SSL 2.0 et SSL 3.0 sont désactivés par défaut et ne peuvent pas être activés. Ils sont considérés comme non sécurisées et ne sont pas en mesure de toobe utilisé avec la passerelle d’Application.

![image du scénario][scenario]

## <a name="scenario"></a>Scénario

Dans ce scénario, vous apprendrez comment toocreate une passerelle d’application à l’aide de fin tooend SSL à l’aide de PowerShell.

Ce scénario va :

* créer un groupe de ressources nommé **appgw-rg** ;
* créer un réseau virtuel nommé **appgwvnet** avec un espace d’adresse de 10.0.0.0/16 ;
* créer deux sous-réseaux appelés **appgwsubnet** et **appsubnet** ;
* Créer un petite application passerelle prise en charge fin tooend le chiffrement SSL qui limite les versions de protocoles SSL et des suites de chiffrement.

## <a name="before-you-begin"></a>Avant de commencer

tooconfigure fin tooend SSL avec une passerelle d’application, un certificat est requis pour la passerelle de hello et les certificats sont requis pour les serveurs principaux de hello. certificat de passerelle Hello est utilisé tooencrypt et decrypt hello le trafic envoyé tooit à l’aide de SSL. certificat de passerelle Hello doit toobe au format d’échange d’informations personnelles (pfx). Ce format de fichier permet hello privé toobe clé exporté requis par hello application passerelle tooperform hello chiffrement et de déchiffrement du trafic.

Pour l’end tooend SSL chiffrement hello principal doit être dans la liste approuvée avec la passerelle d’application. Pour cela, vous devez téléchargement hello le certificat public de la passerelle d’application toohello hello les serveurs principaux. Cela garantit que cette passerelle d’application hello communique uniquement avec des instances de principal connu. Cela permet de sécuriser davantage hello fin tooend de communication.

Ce processus est décrit dans hello comme suit :

## <a name="create-hello-resource-group"></a>Créer hello groupe de ressources

Cette section vous guide tout au long de la création d’un groupe de ressources, qui contient la passerelle d’application hello.

### <a name="step-1"></a>Étape 1

Ouvrez une session dans tooyour compte Azure.

```powershell
Login-AzureRmAccount
```

### <a name="step-2"></a>Étape 2

Sélectionnez toouse d’abonnement hello pour ce scénario.

```powershell
Select-AzureRmsubscription -SubscriptionName "<Subscription name>"
```

### <a name="step-3"></a>Étape 3 :

Créez un groupe de ressources (ignorez cette étape si vous utilisez un groupe de ressources existant).

```powershell
New-AzureRmResourceGroup -Name appgw-rg -Location "West US"
```

## <a name="create-a-virtual-network-and-a-subnet-for-hello-application-gateway"></a>Créer un réseau virtuel et un sous-réseau pour la passerelle d’application hello

Hello exemple suivant crée un réseau virtuel et deux sous-réseaux. Un sous-réseau est la passerelle d’application hello toohold utilisé. Hello autre sous-réseau est utilisé pour hello les serveurs principaux hello web l’application d’hébergement.

### <a name="step-1"></a>Étape 1

Affecter une plage d’adresses pour les sous-réseaux hello être utilisé pour hello passerelle d’Application lui-même.

```powershell
$gwSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -AddressPrefix 10.0.0.0/24
```

> [!NOTE]
> Les sous-réseaux configurés pour la passerelle d’application doivent être correctement dimensionnés. Une passerelle d’application peut être configurée pour des instances de too10. Chaque instance est une adresse IP du sous-réseau de hello. Un sous-réseau trop petit peut nuire à la montée en charge d’une passerelle d’application.
> 
> 

### <a name="step-2"></a>Étape 2

Affecter un toobe de plage d’adresse utilisé pour hello pool d’adresses principales.

```powershell
$nicSubnet = New-AzureRmVirtualNetworkSubnetConfig  -Name 'appsubnet' -AddressPrefix 10.0.2.0/24
```

### <a name="step-3"></a>Étape 3 :

Créez un réseau virtuel avec les sous-réseaux hello définis dans les étapes précédentes de hello.

```powershell
$vnet = New-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg -Location "West US" -AddressPrefix 10.0.0.0/16 -Subnet $gwSubnet, $nicSubnet
```

### <a name="step-4"></a>Étape 4

Récupérer hello réseau virtuel ressource et le sous-réseau ressources toobe utilisé Bonjour comme suit :

```powershell
$vnet = Get-AzureRmvirtualNetwork -Name 'appgwvnet' -ResourceGroupName appgw-rg
$gwSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appgwsubnet' -VirtualNetwork $vnet
$nicSubnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'appsubnet' -VirtualNetwork $vnet
```

## <a name="create-a-public-ip-address-for-hello-front-end-configuration"></a>Créer une adresse IP publique pour la configuration frontale de hello

Créer un toobe de ressource IP publique utilisée pour la passerelle d’application hello. Cette adresse IP publique est utilisée dans une prochaine étape.

```powershell
$publicip = New-AzureRmPublicIpAddress -ResourceGroupName appgw-rg -Name 'publicIP01' -Location "West US" -AllocationMethod Dynamic
```

> [!IMPORTANT]
> Passerelle d’application ne prend pas en charge hello une adresse IP publique créée avec un nom de domaine défini. Seule une adresse IP publique avec un nom de domaine créé dynamiquement est prise en charge. Si vous avez besoin d’un nom convivial dns pour la passerelle d’application hello, il est recommandé de toouse un enregistrement CNAME enregistrer en tant qu’alias.

## <a name="create-an-application-gateway-configuration-object"></a>Créer un objet de configuration de passerelle Application Gateway

Tous les éléments de configuration sont définies avant de créer la passerelle d’application hello. Hello étapes suivantes créent hello des éléments de configuration qui sont nécessaires pour une ressource de passerelle d’application.

### <a name="step-1"></a>Étape 1

Créer une configuration IP de passerelle l’application, ce paramètre détermine quel sous-réseau hello application passerelle utilise. Au démarrage de la passerelle d’application, il récupère une adresse IP du sous-réseau hello configuré et achemine les adresses IP de réseau du trafic toohello dans le pool d’adresses IP hello back-end. Gardez à l’esprit que chaque instance utilise une adresse IP unique.

```powershell
$gipconfig = New-AzureRmApplicationGatewayIPConfiguration -Name 'gwconfig' -Subnet $gwSubnet
```

### <a name="step-2"></a>Étape 2

Créer une configuration IP frontale, ce paramètre est mappé à un ip privé ou public adresse toohello frontal de la passerelle d’application hello. Hello suivant l’étape associe l’adresse IP publique de hello Bonjour précédant l’étape de configuration IP frontale de hello.

```powershell
$fipconfig = New-AzureRmApplicationGatewayFrontendIPConfig -Name 'fip01' -PublicIPAddress $publicip
```

### <a name="step-3"></a>Étape 3 :

Configurer un pool d’adresses IP hello principal avec des adresses IP hello des serveurs web de principaux hello. Ces adresses IP sont des adresses IP hello qui reçoivent le trafic réseau hello qui provient d’un point de terminaison IP frontale hello. Vous remplacez hello suivant tooadd d’adresses IP de vos propres points de terminaison application IP adresse.

```powershell
$pool = New-AzureRmApplicationGatewayBackendAddressPool -Name 'pool01' -BackendIPAddresses 1.1.1.1, 2.2.2.2, 3.3.3.3
```

> [!NOTE]
> Un nom de domaine complet (FQDN) est également une valeur valide à la place d’une adresse ip pour les serveurs principaux de hello à l’aide du commutateur - BackendFqdns de hello. 

### <a name="step-4"></a>Étape 4

Configurer les ports IP front-end hello pour le point de terminaison IP public hello. Ce port est le port hello qui les utilisateurs finaux se connectent à.

```powershell
$fp = New-AzureRmApplicationGatewayFrontendPort -Name 'port01'  -Port 443
```

### <a name="step-5"></a>Étape 5

Configurer le certificat hello pour la passerelle d’application hello. Ce certificat est utilisé toodecrypt et rechiffrez le trafic sur la passerelle d’application hello hello.

```powershell
$cert = New-AzureRmApplicationGatewaySSLCertificate -Name cert01 -CertificateFile <full path too.pfx file> -Password <password for certificate file>
```

> [!NOTE]
> Cet exemple configure un certificat hello utilisée pour la connexion SSL. certificat de Hello doit toobe au format .pfx et hello le mot de passe doit être comprise entre 4 too12 caractères.

### <a name="step-6"></a>Étape 6

Créer l’écouteur HTTP pour la passerelle d’application hello hello. Affecter la configuration ip frontale de hello, le port et toouse du certificat SSL.

```powershell
$listener = New-AzureRmApplicationGatewayHttpListener -Name listener01 -Protocol Https -FrontendIPConfiguration $fipconfig -FrontendPort $fp -SSLCertificate $cert
```

### <a name="step-7"></a>Étape 7

Téléchargez le certificat hello toobe utilisé sur hello SSL activé principal des ressources.

> [!NOTE]
> Sonde Hello Obtient la clé publique de hello de hello **par défaut** liaison SSL sur hello d’adresse IP de fin-back et compare hello valeur de clé publique qu’il reçoit la valeur de clé publique de toohello vous fournissez ici. Hello récupérées de clé publique peut ne pas être flux de trafic hello destiné site toowhich **si** vous utilisez SNI et les en-têtes d’hôtes sur hello back-end. En cas de doute, visitez https://127.0.0.1/ sur tooconfirm de back end hello quel certificat est utilisé pour hello **par défaut** liaison SSL. Utilisez la clé publique de hello à partir de cette demande dans cette section. Si vous utilisez des en-têtes d’hôte et SNI sur les liaisons HTTPS et vous ne recevez pas une réponse et un certificat à partir d’un navigateur manuel demande toohttps://127.0.0.1/ sur hello principaux, vous devez configurer une liaison SSL de valeur par défaut sur les systèmes principaux hello. Si vous ne le faites pas, l’échec de sondes et hello principal n’est pas dans la liste approuvée.

```powershell
$authcert = New-AzureRmApplicationGatewayAuthenticationCertificate -Name 'whitelistcert1' -CertificateFile C:\users\gwallace\Desktop\cert.cer
```

> [!NOTE]
> certificat de Hello fourni dans cette étape doit être hello de clé publique cert de pfx hello présent sur hello principal. Exporter hello certificat (pas hello racine) installé sur le serveur principal de hello dans. CER mettre en forme et l’utiliser dans cette étape. Cette étape de blocage hello principal avec la passerelle d’application hello.

### <a name="step-8"></a>Étape 8

Configurer les paramètres de hello application passerelle http du serveur principal. Attribuer certificat hello téléchargé Bonjour précédant les paramètres d’étape toohello http.

```powershell
$poolSetting = New-AzureRmApplicationGatewayBackendHttpSettings -Name 'setting01' -Port 443 -Protocol Https -CookieBasedAffinity Enabled -AuthenticationCertificates $authcert
```

### <a name="step-9"></a>Étape 9

Créer une règle de routage de l’équilibreur de charge qui configure le comportement de programme d’équilibrage de charge hello. Dans cet exemple, une simple règle de type tourniquet (round robin) est créée.

```powershell
$rule = New-AzureRmApplicationGatewayRequestRoutingRule -Name 'rule01' -RuleType basic -BackendHttpSettings $poolSetting -HttpListener $listener -BackendAddressPool $pool
```

### <a name="step-10"></a>Étape 10

Configurer la taille de l’instance de la passerelle d’application hello hello.  les tailles disponibles Hello sont **Standard\_petit**, **Standard\_support**, et **Standard\_grande**.  De la capacité, les valeurs disponibles hello vont de 1 à 10.

```powershell
$sku = New-AzureRmApplicationGatewaySku -Name Standard_Small -Tier Standard -Capacity 2
```

> [!NOTE]
> Vous pouvez choisir un nombre d’instances de 1 à des fins de test. Il est important que n’importe quelle instance compte dans les deux instances de tooknow n’est pas couverte par un contrat SLA de hello et ne sont donc pas recommandée. Les passerelles Small sont toobe utilisé pour le développement de test et non à des fins de production.

### <a name="step-11"></a>Étape 11

Configurer toobe de stratégie SSL hello utilisé sur hello passerelle d’Application. Passerelle d’application prend en charge hello capacité tooset une version minimale pour les versions du protocole SSL.

Hello les valeurs suivantes sont une liste des versions de protocole qui peuvent être définis.

* **TLSv1_0**
* **TLSv1_1**
* **TLSv1_2**

Jeux hello version du protocole minimale trop**TLSv1_2** et **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_ SHA256**, **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**et **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** uniquement.

```powershell
$SSLPolicy = New-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion TLSv1_2 -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256"
```

## <a name="create-hello-application-gateway"></a>Créer hello Application Gateway

Hello toutes les étapes précédentes, créez hello passerelle d’Application. Création de Hello de passerelle de hello est un processus à long terme.

```powershell
$appgw = New-AzureRmApplicationGateway -Name appgateway -SSLCertificates $cert -ResourceGroupName "appgw-rg" -Location "West US" -BackendAddressPools $pool -BackendHttpSettingsCollection $poolSetting -FrontendIpConfigurations $fipconfig -GatewayIpConfigurations $gipconfig -FrontendPorts $fp -HttpListeners $listener -RequestRoutingRules $rule -Sku $sku -SSLPolicy $SSLPolicy -AuthenticationCertificates $authcert -Verbose
```

## <a name="limit-ssl-protocol-versions-on-an-existing-application-gateway"></a>Limiter les versions du protocole SSL sur une passerelle Application Gateway existante

Hello précédentes étapes vous guide dans la création d’applications à la fin tooend SSL et la désactivation de certaines versions du protocole SSL. Hello exemple suivant désactive certaines stratégies SSL sur une passerelle d’application existant.

### <a name="step-1"></a>Étape 1

Récupérer tooupdate de passerelle d’application hello.

```powershell
$gw = Get-AzureRmApplicationGateway -Name AdatumAppGateway -ResourceGroupName AdatumAppGatewayRG
```

### <a name="step-2"></a>Étape 2

Définissez une stratégie SSL. Dans l’exemple suivant de hello, TLSv1.0 et TLSv1.1 sont désactivées et hello suites de chiffrement **TLS\_ECDHE\_ECDSA\_WITH\_AES\_128\_GCM\_SHA256** , **TLS\_ECDHE\_ECDSA\_WITH\_AES\_256\_GCM\_SHA384**, et  **TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256** est hello seules autorisées.

```powershell
Set-AzureRmApplicationGatewaySSLPolicy -MinProtocolVersion -PolicyType Custom -CipherSuite "TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256", "TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384", "TLS_RSA_WITH_AES_128_GCM_SHA256" -ApplicationGateway $gw

```

### <a name="step-3"></a>Étape 3 :

Enfin, mettre à jour de passerelle de hello. Il est important toonote que cette dernière étape est une tâche de longue durée. Lorsqu’il est terminé, fin tooend SSL est configuré sur la passerelle d’application hello.

```powershell
$gw | Set-AzureRmApplicationGateway
```

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

En savoir plus sur la sécurisation renforcée de sécurité hello de vos applications web avec des pare-feu d’applications Web via la passerelle d’Application en vous rendant sur [vue d’ensemble du pare-feu d’Application Web](application-gateway-webapplicationfirewall-overview.md)

[scenario]: ./media/application-gateway-end-to-end-SSL-powershell/scenario.png
