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
# <a name="configure-hello-distribution-mode-for-load-balancer"></a><span data-ttu-id="6c79e-103">Configurer le mode de distribution de hello pour l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6c79e-103">Configure hello distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="6c79e-104">Mode de distribution basé sur le hachage</span><span class="sxs-lookup"><span data-stu-id="6c79e-104">Hash-based distribution mode</span></span>

<span data-ttu-id="6c79e-105">algorithme de distribution par défaut Hello est un 5-tuple (IP, port source, source destination IP, port de destination, type de protocole) des serveurs toomap trafic tooavailable de hachage.</span><span class="sxs-lookup"><span data-stu-id="6c79e-105">hello default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash toomap traffic tooavailable servers.</span></span> <span data-ttu-id="6c79e-106">Il fournit l’adhérence uniquement dans une session de transport.</span><span class="sxs-lookup"><span data-stu-id="6c79e-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="6c79e-107">Les paquets hello même session sera dirigé toohello même centre de données IP (DIP) de l’instance derrière le point de terminaison à charge équilibrée hello.</span><span class="sxs-lookup"><span data-stu-id="6c79e-107">Packets in hello same session will be directed toohello same datacenter IP (DIP) instance behind hello load balanced endpoint.</span></span> <span data-ttu-id="6c79e-108">Lorsque hello client démarre une nouvelle session de hello la même adresse IP source, port source de hello change et provoque l’hello trafic toogo tooa DIP point de terminaison différent.</span><span class="sxs-lookup"><span data-stu-id="6c79e-108">When hello client starts a new session from hello same source IP, hello source port changes and causes hello traffic toogo tooa different DIP endpoint.</span></span>

![équilibrage de charge basé sur le hachage](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="6c79e-110">Figure 1 : distribution 5 tuples</span><span class="sxs-lookup"><span data-stu-id="6c79e-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="6c79e-111">Mode d’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="6c79e-111">Source IP affinity mode</span></span>

<span data-ttu-id="6c79e-112">Nous vous avons un autre mode de distribution appelé « affinité d’IP source » (également connu sous le nom d’« affinité de session » ou d’« affinité d’IP client »).</span><span class="sxs-lookup"><span data-stu-id="6c79e-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="6c79e-113">Équilibrage de charge Azure peut être toouse configuré un objet de 2 tuples (adresse IP Source, adresse IP de Destination) ou 3-tuple (IP Source, adresse IP de Destination, protocole) toomap trafic toohello des serveurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="6c79e-113">Azure Load Balancer can be configured toouse a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) toomap traffic toohello available servers.</span></span> <span data-ttu-id="6c79e-114">À l’aide d’affinité de l’adresse IP Source, les connexions initiées à partir de hello même ordinateur client passe toohello même point de terminaison DIP.</span><span class="sxs-lookup"><span data-stu-id="6c79e-114">By using Source IP affinity, connections initiated from hello same client computer goes toohello same DIP endpoint.</span></span>

<span data-ttu-id="6c79e-115">Hello suivant schéma illustre une configuration de l’objet de 2 tuples.</span><span class="sxs-lookup"><span data-stu-id="6c79e-115">hello following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="6c79e-116">Notez que l’exécution de 2 tuples hello via hello charge équilibrage toovirtual machine 1 (VM1) qui est ensuite sauvegardé par VM2 et VM3.</span><span class="sxs-lookup"><span data-stu-id="6c79e-116">Notice how hello 2-tuple runs through hello load balancer toovirtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![affinité de session](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="6c79e-118">Figure 2 : distribution 2 tuples</span><span class="sxs-lookup"><span data-stu-id="6c79e-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="6c79e-119">Affinité d’IP source a résolu une incompatibilité entre hello équilibrage de charge Azure et de passerelle de bureau à distance (RD).</span><span class="sxs-lookup"><span data-stu-id="6c79e-119">Source IP affinity solves an incompatibility between hello Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="6c79e-120">Vous pouvez maintenant générer une batterie de passerelles des services Bureau à distance dans un seul service cloud.</span><span class="sxs-lookup"><span data-stu-id="6c79e-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="6c79e-121">Un autre scénario d’utilisation est un téléchargement de média où le téléchargement des données hello s’effectue via UDP mais plan du contrôle hello s’effectue via TCP :</span><span class="sxs-lookup"><span data-stu-id="6c79e-121">Another use case scenario is media upload where hello data upload happens through UDP but hello control plane is achieved through TCP:</span></span>

* <span data-ttu-id="6c79e-122">Tout d’abord, un client lance une session TCP toohello équilibrage adresse publique, obtient tooa dirigée DIP spécifique, ce canal est intégrité de connexion hello gauche toomonitor active</span><span class="sxs-lookup"><span data-stu-id="6c79e-122">A client first initiates a TCP session toohello load balanced public address, gets directed tooa specific DIP, this channel is left active toomonitor hello connection health</span></span>
* <span data-ttu-id="6c79e-123">Une nouvelle session UDP de hello même ordinateur client est initiée toohello équilibrage même point de terminaison public, attente hello ici est que cette connexion est également toohello dirigée même point de terminaison DIP en tant que connexion TCP de la précédente hello afin que le téléchargement du support peut être exécuté à haut débit tout en conservant un canal de contrôle via TCP.</span><span class="sxs-lookup"><span data-stu-id="6c79e-123">A new UDP session from hello same client computer is initiated toohello same load balanced public endpoint, hello expectation here is that this connection is also directed toohello same DIP endpoint as hello previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="6c79e-124">Lorsqu’un jeu d’équilibrage de charge est modifiée (suppression ou ajout d’une machine virtuelle), la distribution hello de demandes de client est recalculée.</span><span class="sxs-lookup"><span data-stu-id="6c79e-124">When a load-balanced set changes (removing or adding a virtual machine), hello distribution of client requests is recomputed.</span></span> <span data-ttu-id="6c79e-125">Vous ne peuvent pas dépendre de nouvelles connexions à partir de clients existants retrouvent à hello même serveur.</span><span class="sxs-lookup"><span data-stu-id="6c79e-125">You cannot depend on new connections from existing clients ending up at hello same server.</span></span> <span data-ttu-id="6c79e-126">En outre, le mode de distribution d'affinité d’IP source peut entraîner une distribution inégale du trafic.</span><span class="sxs-lookup"><span data-stu-id="6c79e-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="6c79e-127">Les clients qui s’exécutent derrière des serveurs proxy peuvent être vu comme une application cliente unique.</span><span class="sxs-lookup"><span data-stu-id="6c79e-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="6c79e-128">Configuration des paramètres d'affinité d’IP source pour l'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6c79e-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="6c79e-129">Pour les ordinateurs virtuels, vous pouvez utiliser les paramètres de délai d’attente toochange PowerShell :</span><span class="sxs-lookup"><span data-stu-id="6c79e-129">For virtual machines, you can use PowerShell toochange timeout settings:</span></span>

<span data-ttu-id="6c79e-130">Ajouter un tooa de point de terminaison Azure Machine virtuelle et de définir le mode de distribution d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6c79e-130">Add an Azure endpoint tooa Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="6c79e-131">LoadBalancerDistribution peut être définie toosourceIP pour un objet de 2 tuples (adresse IP Source, adresse IP de Destination) d’équilibrage de charge, sourceIPProtocol pour l’équilibrage de charge (protocole IP Source, adresse IP de Destination) à 3 tuples, ou aucun si vous souhaitez que le comportement par défaut de hello d’équilibrage de charge de 5-tuple.</span><span class="sxs-lookup"><span data-stu-id="6c79e-131">LoadBalancerDistribution can be set toosourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want hello default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="6c79e-132">Utilisez hello suivant tooretrieve une configuration en mode de distribution d’équilibrage de point de terminaison charge :</span><span class="sxs-lookup"><span data-stu-id="6c79e-132">Use hello following tooretrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="6c79e-133">Si l’élément de LoadBalancerDistribution hello n’est pas présent équilibreur de charge Azure hello utilise algorithme de 5-tuple hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="6c79e-133">If hello LoadBalancerDistribution element is not present then hello Azure Load balancer uses hello default 5-tuple algorithm.</span></span>

### <a name="set-hello-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="6c79e-134">Définir le mode de Distribution hello sur un ensemble de point de terminaison à charge équilibrée</span><span class="sxs-lookup"><span data-stu-id="6c79e-134">Set hello Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="6c79e-135">Si les points de terminaison font partie d’un ensemble de point de terminaison à charge équilibrée, mode de distribution hello doit être défini sur le jeu de point de terminaison d’équilibrage hello :</span><span class="sxs-lookup"><span data-stu-id="6c79e-135">If endpoints are part of a load balanced endpoint set, hello distribution mode must be set on hello load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-toochange-distribution-mode"></a><span data-ttu-id="6c79e-136">Mode de distribution cloud Service configuration toochange</span><span class="sxs-lookup"><span data-stu-id="6c79e-136">Cloud Service configuration toochange distribution mode</span></span>

<span data-ttu-id="6c79e-137">Vous pouvez tirer parti de hello Azure SDK pour .NET 2.5 (toobe publiée en novembre) tooupdate votre Service Cloud.</span><span class="sxs-lookup"><span data-stu-id="6c79e-137">You can leverage hello Azure SDK for .NET 2.5 (toobe released in November) tooupdate your Cloud Service.</span></span> <span data-ttu-id="6c79e-138">Paramètres de point de terminaison pour les Services Cloud sont effectuées dans hello .csdef.</span><span class="sxs-lookup"><span data-stu-id="6c79e-138">Endpoint settings for Cloud Services are made in hello .csdef.</span></span> <span data-ttu-id="6c79e-139">Dans l’ordre tooupdate hello charge équilibrage mode de distribution pour un déploiement de Services de cloud computing, une mise à niveau du déploiement est requis.</span><span class="sxs-lookup"><span data-stu-id="6c79e-139">In order tooupdate hello load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="6c79e-140">Voici un exemple de modifications apportées aux paramètres de point de terminaison dans .csdef :</span><span class="sxs-lookup"><span data-stu-id="6c79e-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="6c79e-141">Exemple d’API</span><span class="sxs-lookup"><span data-stu-id="6c79e-141">API example</span></span>

<span data-ttu-id="6c79e-142">Vous pouvez configurer la distribution d’équilibrage de charge hello à l’aide des API de gestion de service hello.</span><span class="sxs-lookup"><span data-stu-id="6c79e-142">You can configure hello load balancer distribution using hello service management API.</span></span> <span data-ttu-id="6c79e-143">Assurez-vous que tooadd hello `x-ms-version` en-tête a la valeur tooversion `2014-09-01` ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6c79e-143">Make sure tooadd hello `x-ms-version` header is set tooversion `2014-09-01` or higher.</span></span>

### <a name="update-hello-configuration-of-hello-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="6c79e-144">Configuration de hello de mise à jour de hello spécifiée d’un équilibrage de charge dans un déploiement</span><span class="sxs-lookup"><span data-stu-id="6c79e-144">Update hello configuration of hello specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="6c79e-145">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="6c79e-145">Request example</span></span>

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

<span data-ttu-id="6c79e-146">valeur Hello LoadBalancerDistribution peut être sourceIP pour l’affinité de l’objet de 2 tuples, sourceIPProtocol pour l’affinité de l’objet de 3 tuples ou none (pour aucune affinité.</span><span class="sxs-lookup"><span data-stu-id="6c79e-146">hello value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="6c79e-147">par exemple 5 tuples)</span><span class="sxs-lookup"><span data-stu-id="6c79e-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="6c79e-148">Réponse</span><span class="sxs-lookup"><span data-stu-id="6c79e-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="6c79e-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6c79e-149">Next Steps</span></span>

[<span data-ttu-id="6c79e-150">Présentation de l’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="6c79e-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="6c79e-151">Prise en main de la configuration d’un équilibrage de charge sur Internet</span><span class="sxs-lookup"><span data-stu-id="6c79e-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6c79e-152">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6c79e-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
