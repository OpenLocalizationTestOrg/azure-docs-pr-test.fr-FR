---
title: "aaaCreate, de démarrer ou de supprimer une passerelle d’application | Documents Microsoft"
description: "Cette page fournit des instructions toocreate, configurer, démarrer et supprimer une passerelle d’application Windows Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: 577054ca-8368-4fbf-8d53-a813f29dc3bc
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: 3efef5b49880c9efdafad8b88d4bce5b749b82af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-start-or-delete-an-application-gateway-with-powershell"></a>Création, démarrage ou suppression d’une passerelle Application Gateway avec PowerShell 

> [!div class="op_single_selector"]
> * [portail Azure](application-gateway-create-gateway-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-gateway-arm.md)
> * [Azure Classic PowerShell](application-gateway-create-gateway.md)
> * [Modèle Azure Resource Manager](application-gateway-create-gateway-arm-template.md)
> * [Interface de ligne de commande Azure](application-gateway-create-gateway-cli.md)

La passerelle Azure Application Gateway est un équilibreur de charge de couche 7. Il fournit un basculement, routage des performances des requêtes HTTP entre différents serveurs, qu’ils soient sur le cloud de hello ou localement. Application Gateway offre de nombreuses fonctionnalités de contrôleur de livraison d’applications (ADC) : équilibrage de charge HTTP, affinité de session basée sur les cookies, déchargement SSL (Secure Sockets Layer), sondes d’intégrité personnalisées, prise en charge de plusieurs sites, etc. toofind une liste complète des fonctionnalités prises en charge, visitez [vue d’ensemble de la passerelle Application](application-gateway-introduction.md)

Cet article vous guide tout au long des hello étapes toocreate, configurer, démarrer et supprimer une passerelle d’application.

## <a name="before-you-begin"></a>Avant de commencer

1. Installer version la plus récente des applets de commande PowerShell Azure hello hello à l’aide de hello Web Platform Installer. Vous pouvez télécharger et installer la version la plus récente hello de hello **Windows PowerShell** section Hello [page Téléchargements](https://azure.microsoft.com/downloads/).
2. Si vous avez un réseau virtuel existant, sélectionnez un sous-réseau vide existant ou créer un sous-réseau dans votre réseau virtuel existant uniquement pour une utilisation par la passerelle d’application hello. Vous ne pouvez pas déployer hello application passerelle tooa autre réseau virtuel que les ressources hello vous avez l’intention toodeploy derrière la passerelle d’application hello, sauf si le réseau virtuel d’homologation est utilisé. toolearn visitez plus [d’homologation de réseau virtuel](../virtual-network/virtual-network-peering-overview.md)
3. Vérifiez que vous disposez d'un réseau virtuel qui fonctionne avec un sous-réseau valide. Assurez-vous qu’aucun ordinateur virtuel ou les déploiements de cloud ne sont à l’aide de sous-réseau de hello. passerelle d’application Hello doit être par lui-même dans un sous-réseau de réseau virtuel.
4. serveurs Hello configurer la passerelle d’application hello toouse doivent exister ou aient leurs points de terminaison créés dans le réseau virtuel de hello ou avec une adresse IP publique/VIP affectés.

## <a name="what-is-required-toocreate-an-application-gateway"></a>Qu’est requis toocreate une passerelle d’application ?

Lorsque vous utilisez hello `New-AzureApplicationGateway` passerelle d’application hello commande toocreate, aucune configuration n’est définie à ce stade et ressources de hello nouvellement créé sont configurés à l’aide de XML ou un objet de configuration.

les valeurs Hello sont :

* **Pool de serveur principal :** liste hello des adresses IP des serveurs principaux de hello. adresses IP de Hello répertoriés doivent appartenir soit de sous-réseau de réseau virtuel toohello ou doivent être une adresse IP/VIP publique.
* **Paramètres du pool de serveurs principaux :** chaque pool comporte des paramètres tels que le port, le protocole et une affinité basée sur des cookies. Ces paramètres sont lié tooa pool et sont des serveurs tooall appliqué dans le pool de hello.
* **Port frontal :** ce port est le port public hello qui est ouvert sur la passerelle d’application hello. Le trafic atteint ce port et obtient redirigés tooone de hello sur les serveurs principaux.
* **Écouteur :** hello port d’écoute utilise un port frontal, un protocole (Http ou Https, ces valeurs respectent la casse) et le nom du certificat SSL hello (si le déchargement de la configuration de SSL).
* **La règle :** règle de hello lie le port d’écoute hello et pool de serveur principal hello et définit le trafic de hello de pool de serveur principal doit être dirigée toowhen il atteint un écouteur particulier.

## <a name="create-an-application-gateway"></a>Créer une passerelle Application Gateway

toocreate une passerelle d’application :

1. Créez une ressource Application Gateway.
2. Créez un fichier XML de configuration ou un objet de configuration.
3. Valider hello toohello de configuration qui vient d’être créé ressource passerelle d’application.

> [!NOTE]
> Si vous devez tooconfigure une sonde personnalisée pour votre passerelle d’application, consultez [créer une passerelle d’application en testant personnalisé à l’aide de PowerShell](application-gateway-create-probe-classic-ps.md). Pour plus d’informations, découvrez les [sondes personnalisées et l’analyse du fonctionnement](application-gateway-probe-overview.md) .

![Exemple de scénario][scenario]

### <a name="create-an-application-gateway-resource"></a>Créer une ressource de passerelle d’application

passerelle de hello toocreate, utilisez hello `New-AzureApplicationGateway` applet de commande, en remplaçant les valeurs hello par les vôtres. La facturation pour la passerelle de hello ne démarre pas à ce stade. La facturation commence dans une étape ultérieure, lorsque la passerelle de hello a démarré correctement.

Hello exemple suivant crée une passerelle d’application à l’aide d’un réseau virtuel appelé « testvnet1 » et un sous-réseau nommé « sous-réseau-1 » :

```powershell
New-AzureApplicationGateway -Name AppGwTest -VnetName testvnet1 -Subnets @("Subnet-1")
```

*Description*, *InstanceCount* et *GatewaySize* sont des paramètres facultatifs.

toovalidate qui hello passerelle a été créé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
Name          : AppGwTest
Description   :
VnetName      : testvnet1
Subnets       : {Subnet-1}
InstanceCount : 2
GatewaySize   : Medium
State         : Stopped
VirtualIPs    : {}
DnsName       :
```

> [!NOTE]
> Hello la valeur par défaut de *InstanceCount* est 2, avec une valeur maximale de 10. Hello la valeur par défaut de *GatewaySize* est moyenne. Vous pouvez choisir Small, Medium ou Large.

*Présence* et *DnsName* sont affichés comme vide, car la passerelle de hello n’a pas encore démarré. Ceux-ci sont créés une fois la passerelle de hello en hello état en cours d’exécution.

## <a name="configure-hello-application-gateway"></a>Configurer la passerelle d’application hello

Vous pouvez configurer la passerelle d’application hello à l’aide de XML ou un objet de configuration.

### <a name="configure-hello-application-gateway-by-using-xml"></a>Configurer la passerelle d’application hello à l’aide de XML

Bonjour l’exemple suivant, un tooconfigure de fichier XML tous les paramètres de passerelle d’application et de les valider toohello ressource de passerelle d’application.  

#### <a name="step-1"></a>Étape 1

Copiez hello suivant tooNotepad de texte.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
    <FrontendPorts>
        <FrontendPort>
            <Name>(name-of-your-frontend-port)</Name>
            <Port>(port number)</Port>
        </FrontendPort>
    </FrontendPorts>
    <BackendAddressPools>
        <BackendAddressPool>
            <Name>(name-of-your-backend-pool)</Name>
            <IPAddresses>
                <IPAddress>(your-IP-address-for-backend-pool)</IPAddress>
                <IPAddress>(your-second-IP-address-for-backend-pool)</IPAddress>
            </IPAddresses>
        </BackendAddressPool>
    </BackendAddressPools>
    <BackendHttpSettingsList>
        <BackendHttpSettings>
            <Name>(backend-setting-name-to-configure-rule)</Name>
            <Port>80</Port>
            <Protocol>[Http|Https]</Protocol>
            <CookieBasedAffinity>Enabled</CookieBasedAffinity>
        </BackendHttpSettings>
    </BackendHttpSettingsList>
    <HttpListeners>
        <HttpListener>
            <Name>(name-of-the-listener)</Name>
            <FrontendPort>(name-of-your-frontend-port)</FrontendPort>
            <Protocol>[Http|Https]</Protocol>
        </HttpListener>
    </HttpListeners>
    <HttpLoadBalancingRules>
        <HttpLoadBalancingRule>
            <Name>(name-of-load-balancing-rule)</Name>
            <Type>basic</Type>
            <BackendHttpSettings>(backend-setting-name-to-configure-rule)</BackendHttpSettings>
            <Listener>(name-of-the-listener)</Listener>
            <BackendAddressPool>(name-of-your-backend-pool)</BackendAddressPool>
        </HttpLoadBalancingRule>
    </HttpLoadBalancingRules>
</ApplicationGatewayConfiguration>
```

Modifier les valeurs hello entre parenthèses hello pour les éléments de configuration hello. Hello enregistrez-le avec l’extension .xml.

> [!IMPORTANT]
> l’élément Hello protocole Http ou Https est sensible à la casse.

Bonjour à l’exemple suivant montre comment toouse une configuration de fichier tooset de passerelle d’application hello. charge d’exemple Hello équilibre le trafic HTTP sur le port public 80 et envoie le trafic réseau tooback-end port80 entre deux adresses IP.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationGatewayConfiguration xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/windowsazure">
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

#### <a name="step-2"></a>Étape 2

Définissez ensuite la passerelle d’application hello. Hello d’utilisation `Set-AzureApplicationGatewayConfig` applet de commande avec un fichier XML de configuration.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -ConfigFile "D:\config.xml"
```

### <a name="configure-hello-application-gateway-by-using-a-configuration-object"></a>Configurer la passerelle d’application hello à l’aide d’un objet de configuration

Bonjour à l’exemple suivant montre comment tooconfigure hello passerelle d’application à l’aide d’objets de configuration. Tous les éléments de configuration doivent être configurées individuellement et ensuite ajoutés objet de configuration de passerelle tooan application. Après avoir créé un objet de configuration hello, vous utilisez hello `Set-AzureApplicationGateway` commande toocommit hello configuration toohello créé précédemment des ressources de passerelle d’application.

> [!NOTE]
> Avant d’attribuer un objet de configuration de tooeach de valeur, vous devez toodeclare le type d’objet PowerShell utilise pour le stockage. éléments individuels de Hello première ligne toocreate hello définit ce que `Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model(object name)` sont utilisés.

#### <a name="step-1"></a>Étape 1

Créez tous les éléments de configuration.

Créer un IP frontale de hello comme Bonjour l’exemple suivant.

```powershell
$fip = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration
$fip.Name = "fip1"
$fip.Type = "Private"
$fip.StaticIPAddress = "10.0.0.5"
```

Créer un port frontal de hello comme Bonjour l’exemple suivant.

```powershell
$fep = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort
$fep.Name = "fep1"
$fep.Port = 80
```

Créer un pool de serveur principal hello.

Définir les adresses IP hello ajoutés toohello pool de serveur principal comme indiqué dans l’exemple suivant de hello.

```powershell
$servers = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendServerCollection
$servers.Add("10.0.0.1")
$servers.Add("10.0.0.2")
```

Utilisez hello $server tooadd hello valeurs toohello principal pool d’objet ($pool).

```powershell
$pool = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool
$pool.BackendServers = $servers
$pool.Name = "pool1"
```

Créer un paramètre de pool hello serveur principal.

```powershell
$setting = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings
$setting.Name = "setting1"
$setting.CookieBasedAffinity = "enabled"
$setting.Port = 80
$setting.Protocol = "http"
```

Créer un écouteur de hello.

```powershell
$listener = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener
$listener.Name = "listener1"
$listener.FrontendPort = "fep1"
$listener.FrontendIP = "fip1"
$listener.Protocol = "http"
$listener.SslCert = ""
```

Créer la règle de hello.

```powershell
$rule = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule
$rule.Name = "rule1"
$rule.Type = "basic"
$rule.BackendHttpSettings = "setting1"
$rule.Listener = "listener1"
$rule.BackendAddressPool = "pool1"
```

#### <a name="step-2"></a>Étape 2

Attribuez toutes les configuration individuelle des éléments tooan application passerelle configuration objet ($appgwconfig).

Ajouter hello frontal IP toohello configuration.

```powershell
$appgwconfig = New-Object Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.ApplicationGatewayConfiguration
$appgwconfig.FrontendIPConfigurations = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendIPConfiguration]"
$appgwconfig.FrontendIPConfigurations.Add($fip)
```

Ajouter hello port frontal toohello configuration.

```powershell
$appgwconfig.FrontendPorts = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.FrontendPort]"
$appgwconfig.FrontendPorts.Add($fep)
```
Ajouter hello serveur principal pool toohello configuration.

```powershell
$appgwconfig.BackendAddressPools = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendAddressPool]"
$appgwconfig.BackendAddressPools.Add($pool)
```

Ajoutez toohello configuration de pool de back-end hello.

```powershell
$appgwconfig.BackendHttpSettingsList = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.BackendHttpSettings]"
$appgwconfig.BackendHttpSettingsList.Add($setting)
```

Ajoutez toohello configuration de l’écouteur hello.

```powershell
$appgwconfig.HttpListeners = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpListener]"
$appgwconfig.HttpListeners.Add($listener)
```

Ajouter la configuration des règles de toohello hello.

```powershell
$appgwconfig.HttpLoadBalancingRules = New-Object "System.Collections.Generic.List[Microsoft.WindowsAzure.Commands.ServiceManagement.Network.ApplicationGateway.Model.HttpLoadBalancingRule]"
$appgwconfig.HttpLoadBalancingRules.Add($rule)
```

### <a name="step-3"></a>Étape 3 :
Valider les ressources de passerelle d’application toohello hello configuration objets à l’aide de `Set-AzureApplicationGatewayConfig`.

```powershell
Set-AzureApplicationGatewayConfig -Name AppGwTest -Config $appgwconfig
```

## <a name="start-hello-gateway"></a>Démarrer hello passerelle

Une fois que la passerelle de hello a été configurée, utilisez hello `Start-AzureApplicationGateway` passerelle de hello toostart applet de commande. Le coût d’une passerelle d’application commence une fois la passerelle de hello a démarré.

> [!NOTE]
> Hello `Start-AzureApplicationGateway` applet de commande peut prendre les toofinish too15 à 20 minutes.

```powershell
Start-AzureApplicationGateway AppGwTest
```

## <a name="verify-hello-gateway-status"></a>Vérifiez l’état de la passerelle hello

Hello d’utilisation `Get-AzureApplicationGateway` état de hello toocheck applet de commande de passerelle de hello. Si `Start-AzureApplicationGateway` a réussi à l’étape précédente de hello, *état* doit être en cours d’exécution, et *Vip* et *DnsName* doit avoir des entrées valides.

Hello suivant montre une passerelle d’application qui est en cours d’exécution, vers le haut et le trafic de prêt tootake destinés `http://<generated-dns-name>.cloudapp.net`.

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
Vip           : 138.91.170.26
DnsName       : appgw-1b8402e8-3e0d-428d-b661-289c16c82101.cloudapp.net
```

## <a name="delete-hello-application-gateway"></a>Suppression de la passerelle d’application hello

passerelle d’application toodelete hello :

1. Hello d’utilisation `Stop-AzureApplicationGateway` passerelle de hello toostop applet de commande.
2. Hello d’utilisation `Remove-AzureApplicationGateway` passerelle de hello tooremove applet de commande.
3. Vérifiez cette passerelle hello a été supprimée à l’aide de hello `Get-AzureApplicationGateway` applet de commande.

exemple Hello présente hello `Stop-AzureApplicationGateway` applet de commande sur la première ligne de hello, suivie des hello.

```powershell
Stop-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 9:49:34 PM - Begin Operation: Stop-AzureApplicationGateway
VERBOSE: 10:10:06 PM - Completed Operation: Stop-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   ce6c6c95-77b4-2118-9d65-e29defadffb8
```

Une fois que la passerelle d’application hello est dans un état arrêté, utilisez hello `Remove-AzureApplicationGateway` service de hello tooremove applet de commande.

```powershell
Remove-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:49:34 PM - Begin Operation: Remove-AzureApplicationGateway
VERBOSE: 10:50:36 PM - Completed Operation: Remove-AzureApplicationGateway
Name       HTTP Status Code     Operation ID                             Error
----       ----------------     ------------                             ----
Successful OK                   055f3a96-8681-2094-a304-8d9a11ad8301
```

tooverify qui hello service a été supprimé, vous pouvez utiliser hello `Get-AzureApplicationGateway` applet de commande. Cette étape n'est pas requise.

```powershell
Get-AzureApplicationGateway AppGwTest
```

```
VERBOSE: 10:52:46 PM - Begin Operation: Get-AzureApplicationGateway

Get-AzureApplicationGateway : ResourceNotFound: hello gateway does not exist.
.....
```

## <a name="next-steps"></a>Étapes suivantes

Si vous souhaitez tooconfigure le déchargement SSL, consultez [configurer une passerelle d’application pour le déchargement SSL](application-gateway-ssl.md).

Si vous souhaitez tooconfigure un toouse de passerelle d’application avec un équilibrage de charge interne, consultez [créer une passerelle d’application avec un équilibreur de charge interne (ILB)](application-gateway-ilb.md).

Si vous souhaitez plus d'informations sur les options d'équilibrage de charge en général, consultez :

* [Équilibrage de charge Azure](https://azure.microsoft.com/documentation/services/load-balancer/)
* [Azure Traffic Manager](https://azure.microsoft.com/documentation/services/traffic-manager/)

[scenario]: ./media/application-gateway-create-gateway/scenario.png
