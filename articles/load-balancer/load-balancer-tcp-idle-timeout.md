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
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="49125-103">Configuration des paramètres de délai d’inactivité et d’expiration TCP pour Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="49125-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="49125-104">Dans sa configuration par défaut, l’équilibrage de charge Azure a un paramètre de délai d’inactivité de 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="49125-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="49125-105">Si une période d’inactivité est supérieure à la valeur de délai d’attente hello, il n’existe aucune garantie que hello TCP ou session HTTP est conservée entre le client de hello et votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="49125-105">If a period of inactivity is longer than hello timeout value, there's no guarantee that hello TCP or HTTP session is maintained between hello client and your cloud service.</span></span>

<span data-ttu-id="49125-106">Lors de la connexion de hello est fermée, votre application cliente peut s’afficher hello message d’erreur suivant : « hello connexion sous-jacente a été fermée : une connexion qui a été prévue toobe maintenus l’activité a été fermée par le serveur de hello. »</span><span class="sxs-lookup"><span data-stu-id="49125-106">When hello connection is closed, your client application may receive hello following error message: "hello underlying connection was closed: A connection that was expected toobe kept alive was closed by hello server."</span></span>

<span data-ttu-id="49125-107">Une pratique courante consiste à toouse TCP KeepAlive.</span><span class="sxs-lookup"><span data-stu-id="49125-107">A common practice is toouse a TCP keep-alive.</span></span> <span data-ttu-id="49125-108">Cette pratique maintient la connexion de hello active pour une période plus longue.</span><span class="sxs-lookup"><span data-stu-id="49125-108">This practice keeps hello connection active for a longer period.</span></span> <span data-ttu-id="49125-109">Pour plus d’informations, consultez ces [exemples .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="49125-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="49125-110">Activé keep-alive, les paquets sont envoyés au cours des périodes d’inactivité sur la connexion de hello.</span><span class="sxs-lookup"><span data-stu-id="49125-110">With keep-alive enabled, packets are sent during periods of inactivity on hello connection.</span></span> <span data-ttu-id="49125-111">Ces paquets persistants vous assurer que la valeur de délai d’inactivité hello n’est jamais atteint et connexion de hello est conservée pendant une longue période.</span><span class="sxs-lookup"><span data-stu-id="49125-111">These keep-alive packets ensure that hello idle timeout value is never reached and hello connection is maintained for a long period.</span></span>

<span data-ttu-id="49125-112">Ce paramètre fonctionne uniquement pour les connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="49125-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="49125-113">tooavoid perdante de la connexion de hello, vous devez configurer hello TCP persistante avec un intervalle inférieur à hello paramètre ou augmentez hello délai d’inactivité délai d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="49125-113">tooavoid losing hello connection, you must configure hello TCP keep-alive with an interval less than hello idle timeout setting or increase hello idle timeout value.</span></span> <span data-ttu-id="49125-114">toosupport ces scénarios, nous avons ajouté la prise en charge pour un délai d’attente inactif configurable.</span><span class="sxs-lookup"><span data-stu-id="49125-114">toosupport such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="49125-115">Vous pouvez maintenant définir pour une durée de 4 minutes too30.</span><span class="sxs-lookup"><span data-stu-id="49125-115">You can now set it for a duration of 4 too30 minutes.</span></span>

<span data-ttu-id="49125-116">TCP keep-alive fonctionne bien pour les scénarios où l’autonomie de la batterie n’est pas une contrainte.</span><span class="sxs-lookup"><span data-stu-id="49125-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="49125-117">Il n’est pas recommandé de l’utiliser pour les applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="49125-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="49125-118">À l’aide de TCP KeepAlive dans une application mobile peut s’épuise hello périphérique plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="49125-118">Using a TCP keep-alive in a mobile application can drain hello device battery faster.</span></span>

![Délai d’expiration TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="49125-120">Hello les sections suivantes décrire comment les toochange des temps d’inactivité des paramètres de délai d’attente dans des machines virtuelles et services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="49125-120">hello following sections describe how toochange idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-hello-tcp-timeout-for-your-instance-level-public-ip-too15-minutes"></a><span data-ttu-id="49125-121">Configurer le délai d’expiration TCP de hello pour les minutes too15 IP publiques de niveau de l’instance</span><span class="sxs-lookup"><span data-stu-id="49125-121">Configure hello TCP timeout for your instance-level public IP too15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="49125-122">`IdleTimeoutInMinutes` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="49125-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="49125-123">Si elle n’est pas définie, le délai d’attente de hello par défaut est 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="49125-123">If it is not set, hello default timeout is 4 minutes.</span></span> <span data-ttu-id="49125-124">plage de délai d’attente acceptable Hello est 4 minutes too30.</span><span class="sxs-lookup"><span data-stu-id="49125-124">hello acceptable timeout range is 4 too30 minutes.</span></span>

## <a name="set-hello-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="49125-125">Définir le délai d’inactivité de hello lors de la création d’un point de terminaison Azure sur un ordinateur virtuel</span><span class="sxs-lookup"><span data-stu-id="49125-125">Set hello idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="49125-126">toochange hello délai d’expiration de la définition pour un point de terminaison, utilisez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="49125-126">toochange hello timeout setting for an endpoint, use hello following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="49125-127">tooretrieve votre configuration du délai d’inactivité, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="49125-127">tooretrieve your idle timeout configuration, use hello following command:</span></span>

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

## <a name="set-hello-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="49125-128">Définir le délai d’attente de hello TCP sur un ensemble de point de terminaison avec équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="49125-128">Set hello TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="49125-129">Si les points de terminaison font partie d’un ensemble de point de terminaison avec équilibrage de charge, le délai d’attente de hello TCP doit être défini sur l’ensemble du point de terminaison avec équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="49125-129">If endpoints are part of a load-balanced endpoint set, hello TCP timeout must be set on hello load-balanced endpoint set.</span></span> <span data-ttu-id="49125-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="49125-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="49125-131">Modifier les paramètres de délai d’expiration pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="49125-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="49125-132">Vous pouvez utiliser hello Azure SDK tooupdate votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="49125-132">You can use hello Azure SDK tooupdate your cloud service.</span></span> <span data-ttu-id="49125-133">Vous apportez des paramètres de point de terminaison pour les services de cloud computing dans le fichier de .csdef hello.</span><span class="sxs-lookup"><span data-stu-id="49125-133">You make endpoint settings for cloud services in hello .csdef file.</span></span> <span data-ttu-id="49125-134">Mise à jour le délai d’expiration TCP de hello pour le déploiement d’un service cloud requiert une mise à niveau du déploiement.</span><span class="sxs-lookup"><span data-stu-id="49125-134">Updating hello TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="49125-135">Une exception est si le délai d’expiration TCP de hello est spécifié uniquement pour une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="49125-135">An exception is if hello TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="49125-136">Les paramètres IP publics sont dans le fichier .cscfg de hello, et vous pouvez les mettre à jour via la mise à niveau et mise à jour du déploiement.</span><span class="sxs-lookup"><span data-stu-id="49125-136">Public IP settings are in hello .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="49125-137">modifications de .csdef de Hello pour les paramètres de point de terminaison sont :</span><span class="sxs-lookup"><span data-stu-id="49125-137">hello .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="49125-138">modifications de .cscfg Hello pour le paramètre de délai d’attente hello sur des adresses IP publiques sont :</span><span class="sxs-lookup"><span data-stu-id="49125-138">hello .cscfg changes for hello timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="49125-139">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="49125-139">REST API example</span></span>

<span data-ttu-id="49125-140">Vous pouvez configurer le délai d’inactivité de hello TCP à l’aide des API de gestion de service hello.</span><span class="sxs-lookup"><span data-stu-id="49125-140">You can configure hello TCP idle timeout by using hello service management API.</span></span> <span data-ttu-id="49125-141">Vérifiez que hello `x-ms-version` en-tête a la valeur tooversion `2014-06-01` ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="49125-141">Make sure that hello `x-ms-version` header is set tooversion `2014-06-01` or later.</span></span> <span data-ttu-id="49125-142">Mettre à jour les points de terminaison hello configuration Hello spécifié équilibré de la charge d’entrée sur toutes les machines virtuelles dans un déploiement.</span><span class="sxs-lookup"><span data-stu-id="49125-142">Update hello configuration of hello specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="49125-143">Demande</span><span class="sxs-lookup"><span data-stu-id="49125-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="49125-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="49125-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="49125-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="49125-145">Next steps</span></span>

[<span data-ttu-id="49125-146">Présentation de l’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="49125-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="49125-147">Prise en main de la configuration d’un équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="49125-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="49125-148">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="49125-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
