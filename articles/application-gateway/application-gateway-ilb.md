---
title: "aaaUsing passerelle d’Application Azure avec équilibrage de charge interne | Documents Microsoft"
description: "Cette page fournit des instructions tooconfigure une passerelle d’Application Azure avec un point de terminaison d’équilibrage de charge interne"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 7403d28e-909f-46a2-b282-43a8e942f53c
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: gwallace
ms.openlocfilehash: 272ef84a02f92a8521c35aad6f1d9f9bf1675718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-gateway-with-an-internal-load-balancer-ilb"></a>Création d'une passerelle Application Gateway avec un équilibrage de charge interne (ILB)

> [!div class="op_single_selector"]
> * [Azure Classic PowerShell](application-gateway-ilb.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-ilb-arm.md)

Passerelle d’application peut être configurée avec un ordinateur à adresse IP virtuelle d’internet ou avec un toohello de point de terminaison internes non exposée internet, également appelé point de terminaison équilibreur de charge interne (ILB). Configuration de passerelle hello avec un équilibrage de charge interne est utile pour des applications line-of-business internes ne pas exposées toointernet. Il est également utile pour les services/niveaux au sein d’une application à plusieurs niveaux, qui se trouve dans un toointernet n'exposée pas de limite de sécurité, mais nécessitent toujours de répartition de charge de tourniquet (Round Robin), caractère collant de session ou l’arrêt de SSL. Cet article vous guide tout au long des étapes de hello tooconfigure une passerelle d’application avec un équilibrage de charge interne.

## <a name="before-you-begin"></a>Avant de commencer

1. Installez la version la plus récente des applets de commande PowerShell Azure hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page de téléchargement](https://azure.microsoft.com/downloads/).
2. Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide.
3. Vérifiez que vous disposez de serveurs principaux dans le réseau virtuel de hello, ou avec une adresse IP publique/VIP attribué.

toocreate une passerelle d’application, effectuez hello comme suit dans l’ordre de hello. 

1. [Créer une passerelle Application Gateway](#create-a-new-application-gateway)
2. [Configurer la passerelle de hello](#configure-the-gateway)
3. [Jeu de configuration de la passerelle hello](#set-the-gateway-configuration)
4. [Démarrer hello passerelle](#start-the-gateway)
5. [Vérifiez que la passerelle de hello](#verify-the-gateway-status)

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway :

**passerelle de hello toocreate**, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres. Notez que la facturation pour la passerelle de hello ne démarre pas à ce stade. La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

```
VERBOSE: 4:31:35 PM - Begin Operation: New-AzureApplicationGateway 
VERBOSE: 4:32:37 PM - Completed Operation: New-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   55ef0460-825d-2981-ad20-b9a8af41b399
```

**toovalidate** que passerelle de hello a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande. 

Dans l’exemple hello, *Description*, *InstanceCount*, et *GatewaySize* sont des paramètres facultatifs. Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10. Hello la valeur par défaut de *GatewaySize* est moyenne. Les autres valeurs disponibles sont Small et Large. *Adresse IP virtuelle* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré. Ceux-ci sont créés une fois la passerelle de hello en hello état en cours d’exécution. 

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 4:39:39 PM - Begin Operation:
Get-AzureApplicationGateway VERBOSE: 4:39:40 PM - Completed 
Operation: Get-AzureApplicationGateway
Name: AppGwTest    
Description: 
VnetName: testvnet1 
Subnets: {Subnet-1} 
InstanceCount: 2 
GatewaySize: Medium 
State: Stopped 
VirtualIPs: 
DnsName:
```

## <a name="configure-hello-gateway"></a>Configurer la passerelle de hello
La configuration d'une passerelle Application Gateway se compose de plusieurs valeurs. les valeurs Hello peuvent être liées configuration de hello tooconstruct ensemble.

les valeurs Hello sont :

* **Pool de serveurs principaux :** liste hello d’adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique. 
* **Paramètres du pool de serveurs principaux** : chaque pool comporte des paramètres comme le port, le protocole et une affinité basée sur les cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port de serveur frontal :** ce port est le port public de hello ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient ensuite redirigé tooone des serveurs principaux de hello.
* **Écouteur :** écouteur de hello possède un port de serveur frontal, un protocole (Http ou Https, ils respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL). 
* **La règle :** règle de hello lie le port d’écoute hello et pool de serveurs principaux hello et définit le principal serveur pool hello le trafic doit être dirigée toowhen il atteint un écouteur particulier. Actuellement, seuls hello *base* règle est pris en charge. Hello *base* règle est la distribution de la charge de tourniquet.

Vous pouvez construire votre configuration en créant un objet de configuration ou en utilisant un fichier XML de configuration. votre configuration à l’aide d’un fichier XML de configuration, l’utilisation hello tooconstruct les exemples ci-dessous.

Notez hello suivantes :

* Hello *configurations IP frontales adresse* élément décrit en détail équilibrage de charge interne hello pour la configuration de passerelle d’Application avec un équilibrage de charge interne. 
* IP de serveur frontal Hello *Type* doit être défini too'Private'
* Hello *StaticIPAddress* doit indiquer l’adresse IP interne toohello souhaitée sur le hello passerelle reçoit le trafic. Notez que hello *StaticIPAddress* élément est facultatif. Si ce n’est pas le cas, ensemble, une adresse IP interne disponible à partir du sous-réseau de hello déployé est choisie. 
* Hello valeur Hello *nom* élément spécifié dans *configuration IP frontale* doit être utilisé dans hello HTTPListener *FrontendIP* élément toorefer toohello Configuration IP frontale.
  
  **Exemple de configuration XML**
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendIPConfigurations>
        <FrontendIPConfiguration>
            <Name>fip1</Name> 
            <Type>Private</Type> 
            <StaticIPAddress>10.0.0.10</StaticIPAddress> 
        </FrontendIPConfiguration>
    </FrontendIPConfigurations>
    <FrontendPorts>
        <FrontendPort>
            <Name>FrontendPort1</Name>
            <Port>80</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>BackendPool1</Name>
            <IPAddresses>
                <IPAddress>10.0.0.1</IPAddress>
                <IPAddress>10.0.0.2</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>BackendSetting1</Name>
            <Port>80</Port>
            <Protocol>Http</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>HTTPListener1</Name>
            <FrontendIP>fip1</FrontendIP>
            <FrontendPort>FrontendPort1</FrontendPort>
            <Protocol>Http</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>HttpLBRule1</Name>
            <Type>basic</Type>
            <BackendHttpSettings>BackendSetting1</BackendHttpSettings>
            <Listener>HTTPListener1</Listener>
            <BackendAddressPool>BackendPool1</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```


## <a name="set-hello-gateway-configuration"></a>Jeu de configuration de la passerelle hello
Ensuite, vous allez définir la passerelle d’application hello. Vous pouvez utiliser hello `Set-AzureApplicationGatewayConfig` applet de commande avec un objet de configuration, ou avec un fichier XML de configuration. 

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile D:\config.xml
```

```
VERBOSE: 7:54:59 PM - Begin Operation: Set-AzureApplicationGatewayConfig 
VERBOSE: 7:55:32 PM - Completed Operation: Set-AzureApplicationGatewayConfig
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   9b995a09-66fe-2944-8b67-9bb04fcccb9d
```

## <a name="start-hello-gateway"></a>Démarrer hello passerelle

Une fois que la passerelle de hello a été configurée, utilisez hello `Start-AzureApplicationGateway` passerelle de hello toostart applet de commande. Le coût d’une passerelle d’application commence une fois la passerelle de hello a démarré. 

> [!NOTE]
> Hello `Start-AzureApplicationGateway` applet de commande peut prendre les toocomplete too15 à 20 minutes. 
> 
> 

```powershell
Start-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 7:59:16 PM - Begin Operation: Start-AzureApplicationGateway 
VERBOSE: 8:05:52 PM - Completed Operation: Start-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error 
----       ----------------     ------------                             ----
Successful OK                   fc592db8-4c58-2c8e-9a1d-1c97880f0b9b
```

## <a name="verify-hello-gateway-status"></a>Vérifiez l’état de la passerelle hello

Hello d’utilisation `Get-AzureApplicationGateway` état de hello toocheck applet de commande de la passerelle. Si `Start-AzureApplicationGateway` a réussi à l’étape précédente de hello, hello état doit être *en cours d’exécution*, hello Vip et DnsName doit avoir des entrées valides. Cet exemple montre l’applet de commande hello sur la première ligne de hello, suivi par la sortie hello. Dans cet exemple, la passerelle de hello est en cours d’exécution et correspond au trafic tootake prêt. 

> [!NOTE]
> configuration de la passerelle application Hello trafic tooaccept à hello configuré le point de terminaison d’équilibrage de charge interne de 10.0.0.10 dans cet exemple.

```powershell
Get-AzureApplicationGateway AppGwTest 
```

```
VERBOSE: 8:09:28 PM - Begin Operation: Get-AzureApplicationGateway 
VERBOSE: 8:09:30 PM - Completed Operation: Get-AzureApplicationGateway
Name          : AppGwTest
Description   : 
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Running
VirtualIPs    : {10.0.0.10}
DnsName       : appgw-b2a11563-2b3a-4172-a4aa-226ee4c23eed.cloudapp.net
```

## <a name="next-steps"></a>Étapes suivantes
Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

