---
title: "mode de distribution d’équilibrage de charge aaaConfigure | Documents Microsoft"
description: "Comment tooconfigure Azure charge affinité de l’IP équilibrage distribution mode toosupport source"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: 7df27a4d-67a8-47d6-b73e-32c0c6206e6e
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: e745240b733ffc07928d8ed0ae097785ad4f412e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-distribution-mode-for-load-balancer"></a>Configurer le mode de distribution de hello pour l’équilibrage de charge

## <a name="hash-based-distribution-mode"></a>Mode de distribution basé sur le hachage

algorithme de distribution par défaut Hello est un 5-tuple (IP, port source, source destination IP, port de destination, type de protocole) des serveurs toomap trafic tooavailable de hachage. Il fournit l’adhérence uniquement dans une session de transport. Les paquets hello même session sera dirigé toohello même centre de données IP (DIP) de l’instance derrière le point de terminaison à charge équilibrée hello. Lorsque hello client démarre une nouvelle session de hello la même adresse IP source, port source de hello change et provoque l’hello trafic toogo tooa DIP point de terminaison différent.

![équilibrage de charge basé sur le hachage](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

Figure 1 : distribution 5 tuples

## <a name="source-ip-affinity-mode"></a>Mode d’affinité d’IP source

Nous vous avons un autre mode de distribution appelé « affinité d’IP source » (également connu sous le nom d’« affinité de session » ou d’« affinité d’IP client »). Équilibrage de charge Azure peut être toouse configuré un objet de 2 tuples (adresse IP Source, adresse IP de Destination) ou 3-tuple (IP Source, adresse IP de Destination, protocole) toomap trafic toohello des serveurs disponibles. À l’aide d’affinité de l’adresse IP Source, les connexions initiées à partir de hello même ordinateur client passe toohello même point de terminaison DIP.

Hello suivant schéma illustre une configuration de l’objet de 2 tuples. Notez que l’exécution de 2 tuples hello via hello charge équilibrage toovirtual machine 1 (VM1) qui est ensuite sauvegardé par VM2 et VM3.

![affinité de session](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

Figure 2 : distribution 2 tuples

Affinité d’IP source a résolu une incompatibilité entre hello équilibrage de charge Azure et de passerelle de bureau à distance (RD). Vous pouvez maintenant générer une batterie de passerelles des services Bureau à distance dans un seul service cloud.

Un autre scénario d’utilisation est un téléchargement de média où le téléchargement des données hello s’effectue via UDP mais plan du contrôle hello s’effectue via TCP :

* Tout d’abord, un client lance une session TCP toohello équilibrage adresse publique, obtient tooa dirigée DIP spécifique, ce canal est intégrité de connexion hello gauche toomonitor active
* Une nouvelle session UDP de hello même ordinateur client est initiée toohello équilibrage même point de terminaison public, attente hello ici est que cette connexion est également toohello dirigée même point de terminaison DIP en tant que connexion TCP de la précédente hello afin que le téléchargement du support peut être exécuté à haut débit tout en conservant un canal de contrôle via TCP.

> [!NOTE]
> Lorsqu’un jeu d’équilibrage de charge est modifiée (suppression ou ajout d’une machine virtuelle), la distribution hello de demandes de client est recalculée. Vous ne peuvent pas dépendre de nouvelles connexions à partir de clients existants retrouvent à hello même serveur. En outre, le mode de distribution d'affinité d’IP source peut entraîner une distribution inégale du trafic. Les clients qui s’exécutent derrière des serveurs proxy peuvent être vu comme une application cliente unique.

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a>Configuration des paramètres d'affinité d’IP source pour l'équilibrage de charge

Pour les ordinateurs virtuels, vous pouvez utiliser les paramètres de délai d’attente toochange PowerShell :

Ajouter un tooa de point de terminaison Azure Machine virtuelle et de définir le mode de distribution d’équilibrage de charge

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

LoadBalancerDistribution peut être définie toosourceIP pour un objet de 2 tuples (adresse IP Source, adresse IP de Destination) d’équilibrage de charge, sourceIPProtocol pour l’équilibrage de charge (protocole IP Source, adresse IP de Destination) à 3 tuples, ou aucun si vous souhaitez que le comportement par défaut de hello d’équilibrage de charge de 5-tuple.

Utilisez hello suivant tooretrieve une configuration en mode de distribution d’équilibrage de point de terminaison charge :

    PS C:\> Get-AzureVM –ServiceName MyService –Name MyVM | Get-AzureEndpoint

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
    LoadBalancerDistribution : sourceIP

Si l’élément de LoadBalancerDistribution hello n’est pas présent équilibreur de charge Azure hello utilise algorithme de 5-tuple hello par défaut.

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a>Définir le mode de Distribution hello sur un ensemble de point de terminaison à charge équilibrée

Si les points de terminaison font partie d’un ensemble de point de terminaison à charge équilibrée, mode de distribution hello doit être défini sur le jeu de point de terminaison d’équilibrage hello :

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a>Mode de distribution cloud Service configuration toochange

Vous pouvez tirer parti de hello Azure SDK pour .NET 2.5 (toobe publiée en novembre) tooupdate votre Service Cloud. Paramètres de point de terminaison pour les Services Cloud sont effectuées dans hello .csdef. Dans l’ordre tooupdate hello charge équilibrage mode de distribution pour un déploiement de Services de cloud computing, une mise à niveau du déploiement est requis.
Voici un exemple de modifications apportées aux paramètres de point de terminaison dans .csdef :

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancerDistribution="sourceIP" />
    </Endpoints>
</WorkerRole>
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

## <a name="api-example"></a>Exemple d’API

Vous pouvez configurer la distribution d’équilibrage de charge hello à l’aide des API de gestion de service hello. Assurez-vous que tooadd hello `x-ms-version` en-tête a la valeur tooversion `2014-09-01` ou une version ultérieure.

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a>Configuration de hello de mise à jour de hello spécifiée d’un équilibrage de charge dans un déploiement

#### <a name="request-example"></a>Exemple de demande

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>?comp=UpdateLbSet   x-ms-version: 2014-09-01
    Content-Type: application/xml

    <LoadBalancedEndpointList xmlns="http://schemas.microsoft.com/windowsazure" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">
      <InputEndpoint>
        <LoadBalancedEndpointSetName> endpoint-set-name </LoadBalancedEndpointSetName>
        <LocalPort> local-port-number </LocalPort>
        <Port> external-port-number </Port>
        <LoadBalancerProbe>
          <Port> port-assigned-to-probe </Port>
          <Protocol> probe-protocol </Protocol>
          <IntervalInSeconds> interval-of-probe </IntervalInSeconds>
          <TimeoutInSeconds> timeout-for-probe </TimeoutInSeconds>
        </LoadBalancerProbe>
        <Protocol> endpoint-protocol </Protocol>
        <EnableDirectServerReturn> enable-direct-server-return </EnableDirectServerReturn>
        <IdleTimeoutInMinutes>idle-time-out</IdleTimeoutInMinutes>
        <LoadBalancerDistribution>sourceIP</LoadBalancerDistribution>
      </InputEndpoint>
    </LoadBalancedEndpointList>

valeur Hello LoadBalancerDistribution peut être sourceIP pour l’affinité de l’objet de 2 tuples, sourceIPProtocol pour l’affinité de l’objet de 3 tuples ou none (pour aucune affinité. par exemple 5 tuples)

#### <a name="response"></a>Réponse

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a>Étapes suivantes

[Présentation de l’équilibrage de charge interne](load-balancer-internal-overview.md)

[Prise en main de la configuration d’un équilibrage de charge sur Internet](load-balancer-get-started-internet-arm-ps.md)

[Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge](load-balancer-tcp-idle-timeout.md)
