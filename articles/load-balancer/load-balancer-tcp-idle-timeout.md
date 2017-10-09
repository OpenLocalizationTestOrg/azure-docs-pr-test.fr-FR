---
title: "délai d’inactivité de TCP d’équilibrage de charge d’aaaConfigure | Documents Microsoft"
description: "Configuration du délai d’inactivité TCP de l’équilibrage de charge"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 4625c6a8-5725-47ce-81db-4fa3bd055891
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 2bf0704b891f708e0a5bd7aa827441930f51cfaf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a>Configuration des paramètres de délai d’inactivité et d’expiration TCP pour Azure Load Balancer

Dans sa configuration par défaut, l’équilibrage de charge Azure a un paramètre de délai d’inactivité de 4 minutes. Si une période d’inactivité est supérieure à la valeur de délai d’attente hello, il n’existe aucune garantie que hello TCP ou session HTTP est conservée entre le client de hello et votre service cloud.

Lors de la connexion de hello est fermée, votre application cliente peut s’afficher hello message d’erreur suivant : « hello connexion sous-jacente a été fermée : une connexion qui a été prévue toobe maintenus l’activité a été fermée par le serveur de hello. »

Une pratique courante consiste à toouse TCP KeepAlive. Cette pratique maintient la connexion de hello active pour une période plus longue. Pour plus d’informations, consultez ces [exemples .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx). Activé keep-alive, les paquets sont envoyés au cours des périodes d’inactivité sur la connexion de hello. Ces paquets persistants vous assurer que la valeur de délai d’inactivité hello n’est jamais atteint et connexion de hello est conservée pendant une longue période.

Ce paramètre fonctionne uniquement pour les connexions entrantes. tooavoid perdante de la connexion de hello, vous devez configurer hello TCP persistante avec un intervalle inférieur à hello paramètre ou augmentez hello délai d’inactivité délai d’inactivité. toosupport ces scénarios, nous avons ajouté la prise en charge pour un délai d’attente inactif configurable. Vous pouvez maintenant définir pour une durée de 4 minutes too30.

TCP keep-alive fonctionne bien pour les scénarios où l’autonomie de la batterie n’est pas une contrainte. Il n’est pas recommandé de l’utiliser pour les applications mobiles. À l’aide de TCP KeepAlive dans une application mobile peut s’épuise hello périphérique plus rapidement.

![Délai d’expiration TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

Hello les sections suivantes décrire comment les toochange des temps d’inactivité des paramètres de délai d’attente dans des machines virtuelles et services de cloud computing.

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a>Configurer le délai d’expiration TCP de hello pour les minutes too15 IP publiques de niveau de l’instance

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

`IdleTimeoutInMinutes` est facultatif. Si elle n’est pas définie, le délai d’attente de hello par défaut est 4 minutes. plage de délai d’attente acceptable Hello est 4 minutes too30.

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a>Définir le délai d’inactivité de hello lors de la création d’un point de terminaison Azure sur un ordinateur virtuel

toochange hello délai d’expiration de la définition pour un point de terminaison, utilisez hello qui suit :

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

tooretrieve votre configuration du délai d’inactivité, hello utilisez commande suivante :

    PS C:\> Get-AzureVM -ServiceName "MyService" -Name "MyVM" | Get-AzureEndpoint
    VERBOSE: 6:43:50 PM - Completed Operation: Get Deployment
    LBSetName : MyLoadBalancedSet
    LocalPort : 80
    Name : HTTP
    Port : 80
    Protocol : tcp
    Vip : 65.52.xxx.xxx
    ProbePath :
    ProbePort : 80
    ProbeProtocol : tcp
    ProbeIntervalInSeconds : 15
    ProbeTimeoutInSeconds : 31
    EnableDirectServerReturn : False
    Acl : {}
    InternalLoadBalancerName :
    IdleTimeoutInMinutes : 15

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a>Définir le délai d’attente de hello TCP sur un ensemble de point de terminaison avec équilibrage de charge

Si les points de terminaison font partie d’un ensemble de point de terminaison avec équilibrage de charge, le délai d’attente de hello TCP doit être défini sur l’ensemble du point de terminaison avec équilibrage de charge hello. Par exemple :

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a>Modifier les paramètres de délai d’expiration pour les services cloud

Vous pouvez utiliser hello Azure SDK tooupdate votre service cloud. Vous apportez des paramètres de point de terminaison pour les services de cloud computing dans le fichier de .csdef hello. Mise à jour le délai d’expiration TCP de hello pour le déploiement d’un service cloud requiert une mise à niveau du déploiement. Une exception est si le délai d’expiration TCP de hello est spécifié uniquement pour une adresse IP publique. Les paramètres IP publics sont dans le fichier .cscfg de hello, et vous pouvez les mettre à jour via la mise à niveau et mise à jour du déploiement.

modifications de .csdef de Hello pour les paramètres de point de terminaison sont :

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

modifications de .cscfg Hello pour le paramètre de délai d’attente hello sur des adresses IP publiques sont :

```xml
<NetworkConfiguration>
    <VirtualNetworkSite name="VNet"/>
    <AddressAssignments>
    <InstanceAddress roleName="VMRolePersisted">
    <PublicIPs>
        <PublicIP name="public-ip-name" idleTimeoutInMinutes="timeout-in-minutes"/>
    </PublicIPs>
    </InstanceAddress>
    </AddressAssignments>
</NetworkConfiguration>
```

## <a name="rest-api-example"></a>Exemple d’API REST

Vous pouvez configurer le délai d’inactivité de hello TCP à l’aide des API de gestion de service hello. Vérifiez que hello `x-ms-version` en-tête a la valeur tooversion `2014-06-01` ou version ultérieure. Mettre à jour les points de terminaison hello configuration Hello spécifié équilibré de la charge d’entrée sur toutes les machines virtuelles dans un déploiement.

### <a name="request"></a>Demande

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a>Réponse

```xml
<LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
    <InputEndpoint>
    <LoadBalancedEndpointSetName>endpoint-set-name</LoadBalancedEndpointSetName>
    <LocalPort>local-port-number</LocalPort>
    <Port>external-port-number</Port>
    <LoadBalancerProbe>
        <Path>path-of-probe</Path>
        <Port>port-assigned-to-probe</Port>
        <Protocol>probe-protocol</Protocol>
        <IntervalInSeconds>interval-of-probe</IntervalInSeconds>
        <TimeoutInSeconds>timeout-for-probe</TimeoutInSeconds>
    </LoadBalancerProbe>
    <LoadBalancerName>name-of-internal-loadbalancer</LoadBalancerName>
    <Protocol>endpoint-protocol</Protocol>
    <IdleTimeoutInMinutes>15</IdleTimeoutInMinutes>
    <EnableDirectServerReturn>enable-direct-server-return</EnableDirectServerReturn>
    <EndpointACL>
        <Rules>
        <Rule>
            <Order>priority-of-the-rule</Order>
            <Action>permit-rule</Action>
            <RemoteSubnet>subnet-of-the-rule</RemoteSubnet>
            <Description>description-of-the-rule</Description>
        </Rule>
        </Rules>
    </EndpointACL>
    </InputEndpoint>
</LoadBalancedEndpointList>
```

## <a name="next-steps"></a>Étapes suivantes

[Présentation de l’équilibrage de charge interne](load-balancer-internal-overview.md)

[Prise en main de la configuration d’un équilibrage de charge accessible sur Internet](load-balancer-get-started-internet-arm-ps.md)

[Configuration d'un mode de distribution d'équilibrage de charge](load-balancer-distribution-mode.md)
