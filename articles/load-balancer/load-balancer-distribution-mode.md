---
title: "Configuration d’un mode de distribution d’équilibrage de charge | Microsoft Docs"
description: "Procédure de configuration du mode de distribution d’équilibrage de charge Azure pour prendre en charge l'affinité d’IP source"
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
ms.openlocfilehash: 4cb000c8ee1bb2e267dc0813dab23a77a46080ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-distribution-mode-for-load-balancer"></a><span data-ttu-id="d4cec-103">Configuration du mode de distribution de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d4cec-103">Configure the distribution mode for load balancer</span></span>

## <a name="hash-based-distribution-mode"></a><span data-ttu-id="d4cec-104">Mode de distribution basé sur le hachage</span><span class="sxs-lookup"><span data-stu-id="d4cec-104">Hash-based distribution mode</span></span>

<span data-ttu-id="d4cec-105">L’algorithme de distribution par défaut est un hachage à 5 tuples (IP source, port source, IP de destination, port de destination, type de protocole) pour mapper le trafic vers des serveurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="d4cec-105">The default distribution algorithm is a 5-tuple (source IP, source port, destination IP, destination port, protocol type) hash to map traffic to available servers.</span></span> <span data-ttu-id="d4cec-106">Il fournit l’adhérence uniquement dans une session de transport.</span><span class="sxs-lookup"><span data-stu-id="d4cec-106">It provides stickiness only within a transport session.</span></span> <span data-ttu-id="d4cec-107">Les paquets de la même session sont dirigés vers la même instance IP (DIP) de centre de données derrière le point de terminaison d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="d4cec-107">Packets in the same session will be directed to the same datacenter IP (DIP) instance behind the load balanced endpoint.</span></span> <span data-ttu-id="d4cec-108">Lorsque le client démarre une nouvelle session à partir du même IP source, le port source change et contraint le trafic à se diriger vers un autre point de terminaison DIP.</span><span class="sxs-lookup"><span data-stu-id="d4cec-108">When the client starts a new session from the same source IP, the source port changes and causes the traffic to go to a different DIP endpoint.</span></span>

![équilibrage de charge basé sur le hachage](./media/load-balancer-distribution-mode/load-balancer-distribution.png)

<span data-ttu-id="d4cec-110">Figure 1 : distribution 5 tuples</span><span class="sxs-lookup"><span data-stu-id="d4cec-110">Figure 1 - 5-tuple distribution</span></span>

## <a name="source-ip-affinity-mode"></a><span data-ttu-id="d4cec-111">Mode d’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="d4cec-111">Source IP affinity mode</span></span>

<span data-ttu-id="d4cec-112">Nous vous avons un autre mode de distribution appelé « affinité d’IP source » (également connu sous le nom d’« affinité de session » ou d’« affinité d’IP client »).</span><span class="sxs-lookup"><span data-stu-id="d4cec-112">We have another distribution mode called Source IP Affinity (also known as session affinity or client IP affinity).</span></span> <span data-ttu-id="d4cec-113">L’équilibrage de charge Azure peut être configuré pour utiliser 2 tuples (IP source, IP de destination) ou 3 tuples (IP Source, adresse de destination, protocole) pour mapper le trafic vers les serveurs disponibles.</span><span class="sxs-lookup"><span data-stu-id="d4cec-113">Azure Load Balancer can be configured to use a 2-tuple (Source IP, Destination IP) or 3-tuple (Source IP, Destination IP, Protocol) to map traffic to the available servers.</span></span> <span data-ttu-id="d4cec-114">En utilisant l'affinité d’IP Source, les connexions établies à partir du même ordinateur client vont au même point de terminaison DIP.</span><span class="sxs-lookup"><span data-stu-id="d4cec-114">By using Source IP affinity, connections initiated from the same client computer goes to the same DIP endpoint.</span></span>

<span data-ttu-id="d4cec-115">Le schéma suivant illustre une configuration à 2 tuples.</span><span class="sxs-lookup"><span data-stu-id="d4cec-115">The following diagram illustrates a 2-tuple configuration.</span></span> <span data-ttu-id="d4cec-116">Notez comment la distribution 2 tuples passe de l’équilibrage de charge à la machine virtuelle 1 (VM1), puis est sauvegardée par VM2 et VM3.</span><span class="sxs-lookup"><span data-stu-id="d4cec-116">Notice how the 2-tuple runs through the load balancer to virtual machine 1 (VM1) which is then backed up by VM2 and VM3.</span></span>

![affinité de session](./media/load-balancer-distribution-mode/load-balancer-session-affinity.png)

<span data-ttu-id="d4cec-118">Figure 2 : distribution 2 tuples</span><span class="sxs-lookup"><span data-stu-id="d4cec-118">Figure 2 - 2-tuple distribution</span></span>

<span data-ttu-id="d4cec-119">L’affinité d’IP source permet de résoudre une incompatibilité entre l’équilibrage de charge Azure et la passerelle du Bureau à distance (RD).</span><span class="sxs-lookup"><span data-stu-id="d4cec-119">Source IP affinity solves an incompatibility between the Azure Load Balancer and Remote Desktop (RD) Gateway.</span></span> <span data-ttu-id="d4cec-120">Vous pouvez maintenant générer une batterie de passerelles des services Bureau à distance dans un seul service cloud.</span><span class="sxs-lookup"><span data-stu-id="d4cec-120">Now you can build an RD gateway farm in a single cloud service.</span></span>

<span data-ttu-id="d4cec-121">Le chargement de médias constitue un autre cas d’utilisation où le chargement des données se produit via UDP, mais le plan de contrôle via TCP :</span><span class="sxs-lookup"><span data-stu-id="d4cec-121">Another use case scenario is media upload where the data upload happens through UDP but the control plane is achieved through TCP:</span></span>

* <span data-ttu-id="d4cec-122">Un client établit d’abord une session TCP avec l'adresse publique d'équilibrage de charge et est ensuite dirigé vers une adresse DIP spécifique. Ce canal est laissé actif pour surveiller l'état de connexion</span><span class="sxs-lookup"><span data-stu-id="d4cec-122">A client first initiates a TCP session to the load balanced public address, gets directed to a specific DIP, this channel is left active to monitor the connection health</span></span>
* <span data-ttu-id="d4cec-123">Une nouvelle session UDP à partir du même ordinateur client est initialisée au niveau du même point de terminaison public de l’équilibrage de charge, le but ici étant que cette connexion soit également dirigée vers le même point de terminaison DIP que la connexion TCP précédente afin que le téléchargement de média puisse être exécuté à haut débit tout en conservant un canal de contrôle via le TCP.</span><span class="sxs-lookup"><span data-stu-id="d4cec-123">A new UDP session from the same client computer is initiated to the same load balanced public endpoint, the expectation here is that this connection is also directed to the same DIP endpoint as the previous TCP connection so that media upload can be executed at high throughput while also maintaining a control channel through TCP.</span></span>

> [!NOTE]
> <span data-ttu-id="d4cec-124">Lorsqu’un jeu d'équilibrage de charge (suppression ou ajout d'une machine virtuelle) est modifié, la distribution des demandes du client est recalculée.</span><span class="sxs-lookup"><span data-stu-id="d4cec-124">When a load-balanced set changes (removing or adding a virtual machine), the distribution of client requests is recomputed.</span></span> <span data-ttu-id="d4cec-125">Vous ne pouvez pas dépendre de nouvelles connexions à partir de clients existants qui se retrouvent sur le même serveur.</span><span class="sxs-lookup"><span data-stu-id="d4cec-125">You cannot depend on new connections from existing clients ending up at the same server.</span></span> <span data-ttu-id="d4cec-126">En outre, le mode de distribution d'affinité d’IP source peut entraîner une distribution inégale du trafic.</span><span class="sxs-lookup"><span data-stu-id="d4cec-126">Additionally, using source IP affinity distribution mode may cause an unequal distribution of traffic.</span></span> <span data-ttu-id="d4cec-127">Les clients qui s’exécutent derrière des serveurs proxy peuvent être vu comme une application cliente unique.</span><span class="sxs-lookup"><span data-stu-id="d4cec-127">Clients running behind proxies may be seen as one unique client application.</span></span>

## <a name="configuring-source-ip-affinity-settings-for-load-balancer"></a><span data-ttu-id="d4cec-128">Configuration des paramètres d'affinité d’IP source pour l'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d4cec-128">Configuring Source IP affinity settings for load balancer</span></span>

<span data-ttu-id="d4cec-129">Pour les machines virtuelles, vous pouvez utiliser PowerShell pour modifier les paramètres de délai d'attente :</span><span class="sxs-lookup"><span data-stu-id="d4cec-129">For virtual machines, you can use PowerShell to change timeout settings:</span></span>

<span data-ttu-id="d4cec-130">Ajouter un point de terminaison Azure à une machine virtuelle et définir le mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d4cec-130">Add an Azure endpoint to a Virtual Machine and set load balancer distribution mode</span></span>

```powershell
Get-AzureVM -ServiceName mySvc -Name MyVM1 | Add-AzureEndpoint -Name HttpIn -Protocol TCP -PublicPort 80 -LocalPort 8080 –LoadBalancerDistribution sourceIP | Update-AzureVM
```

<span data-ttu-id="d4cec-131">LoadBalancerDistribution peut être défini avec la valeur sourceIP pour un équilibrage de charge à 2 tuples (IP source, IP de destination), sourceIPProtocol pour un équilibrage de charge à 3 tuples (IP source, IP de destination, protocole) ou none si vous préférez le comportement par défaut de l’équilibrage de charge à 5 tuples.</span><span class="sxs-lookup"><span data-stu-id="d4cec-131">LoadBalancerDistribution can be set to sourceIP for 2-tuple (Source IP, Destination IP) load balancing, sourceIPProtocol for 3-tuple (Source IP, Destination IP, protocol) load balancing, or none if you want the default behavior of 5-tuple load balancing.</span></span>

<span data-ttu-id="d4cec-132">Utilisez ce qui suit pour récupérer la configuration du mode de distribution d'équilibrage de charge d'un point de terminaison :</span><span class="sxs-lookup"><span data-stu-id="d4cec-132">Use the following to retrieve an endpoint load balancer distribution mode configuration:</span></span>

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

<span data-ttu-id="d4cec-133">Si l'élément LoadBalancerDistribution n'est pas présent, l'équilibrage de charge Azure utilise alors l'algorithme par défaut à 5 tuples.</span><span class="sxs-lookup"><span data-stu-id="d4cec-133">If the LoadBalancerDistribution element is not present then the Azure Load balancer uses the default 5-tuple algorithm.</span></span>

### <a name="set-the-distribution-mode-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="d4cec-134">Définir le mode de distribution sur un jeu de points de terminaison d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d4cec-134">Set the Distribution mode on a load balanced endpoint set</span></span>

<span data-ttu-id="d4cec-135">Si les points de terminaison font partie d'un jeu de points de terminaison d'équilibrage de charge, le mode de distribution doit être défini sur le jeu de points de terminaison d'équilibrage de charge :</span><span class="sxs-lookup"><span data-stu-id="d4cec-135">If endpoints are part of a load balanced endpoint set, the distribution mode must be set on the load balanced endpoint set:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName MyService -LBSetName LBSet1 -Protocol TCP -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 –LoadBalancerDistribution sourceIP
```

### <a name="cloud-service-configuration-to-change-distribution-mode"></a><span data-ttu-id="d4cec-136">Configuration du service cloud pour modifier le mode de distribution</span><span class="sxs-lookup"><span data-stu-id="d4cec-136">Cloud Service configuration to change distribution mode</span></span>

<span data-ttu-id="d4cec-137">Vous pouvez utiliser le Kit de développement logiciel (SDK) Azure pour .NET 2.5 (qui sera publié en novembre) pour mettre à jour votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="d4cec-137">You can leverage the Azure SDK for .NET 2.5 (to be released in November) to update your Cloud Service.</span></span> <span data-ttu-id="d4cec-138">Les paramètres de point de terminaison des services cloud sont définis dans .csdef.</span><span class="sxs-lookup"><span data-stu-id="d4cec-138">Endpoint settings for Cloud Services are made in the .csdef.</span></span> <span data-ttu-id="d4cec-139">Pour mettre à jour le mode de distribution d'équilibrage de charge pour un déploiement de services cloud, une mise à niveau du déploiement s'impose.</span><span class="sxs-lookup"><span data-stu-id="d4cec-139">In order to update the load balancer distribution mode for a Cloud Services deployment, a deployment upgrade is required.</span></span>
<span data-ttu-id="d4cec-140">Voici un exemple de modifications apportées aux paramètres de point de terminaison dans .csdef :</span><span class="sxs-lookup"><span data-stu-id="d4cec-140">Here is an example of .csdef changes for endpoint settings:</span></span>

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

## <a name="api-example"></a><span data-ttu-id="d4cec-141">Exemple d’API</span><span class="sxs-lookup"><span data-stu-id="d4cec-141">API example</span></span>

<span data-ttu-id="d4cec-142">Vous pouvez configurer la distribution d’équilibrage de charge à l’aide de l’API Gestion des services.</span><span class="sxs-lookup"><span data-stu-id="d4cec-142">You can configure the load balancer distribution using the service management API.</span></span> <span data-ttu-id="d4cec-143">Veillez à ajouter l’en-tête `x-ms-version` et à le définir sur la version `2014-09-01` ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d4cec-143">Make sure to add the `x-ms-version` header is set to version `2014-09-01` or higher.</span></span>

### <a name="update-the-configuration-of-the-specified-load-balanced-set-in-a-deployment"></a><span data-ttu-id="d4cec-144">Mettre à jour la configuration du jeu d'équilibrage de la charge spécifié dans un déploiement</span><span class="sxs-lookup"><span data-stu-id="d4cec-144">Update the configuration of the specified load-balanced set in a deployment</span></span>

#### <a name="request-example"></a><span data-ttu-id="d4cec-145">Exemple de demande</span><span class="sxs-lookup"><span data-stu-id="d4cec-145">Request example</span></span>

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

<span data-ttu-id="d4cec-146">La valeur de LoadBalancerDistribution peut être sourceIP pour une affinité à 2 tuples, sourceIPProtocol pour une affinité à 3 tuples ou none (aucune affinité.</span><span class="sxs-lookup"><span data-stu-id="d4cec-146">The value of LoadBalancerDistribution can be sourceIP for 2-tuple affinity, sourceIPProtocol for 3-tuple affinity or none (for no affinity.</span></span> <span data-ttu-id="d4cec-147">par exemple 5 tuples)</span><span class="sxs-lookup"><span data-stu-id="d4cec-147">i.e. 5-tuple)</span></span>

#### <a name="response"></a><span data-ttu-id="d4cec-148">Réponse</span><span class="sxs-lookup"><span data-stu-id="d4cec-148">Response</span></span>

    HTTP/1.1 202 Accepted
    Cache-Control: no-cache
    Content-Length: 0
    Server: 1.0.6198.146 (rd_rdfe_stable.141015-1306) Microsoft-HTTPAPI/2.0
    x-ms-servedbyregion: ussouth2
    x-ms-request-id: 9c7bda3e67c621a6b57096323069f7af
    Date: Thu, 16 Oct 2014 22:49:21 GMT

## <a name="next-steps"></a><span data-ttu-id="d4cec-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d4cec-149">Next Steps</span></span>

[<span data-ttu-id="d4cec-150">Présentation de l’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="d4cec-150">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="d4cec-151">Prise en main de la configuration d’un équilibrage de charge sur Internet</span><span class="sxs-lookup"><span data-stu-id="d4cec-151">Get started Configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="d4cec-152">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="d4cec-152">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
