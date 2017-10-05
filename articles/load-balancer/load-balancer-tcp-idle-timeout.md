---
title: "Configuration du délai d’inactivité TCP de l’équilibrage de charge | Microsoft Docs"
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
ms.openlocfilehash: d040fe6580b8ae777aecc9dd385ed33861530c38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-tcp-idle-timeout-settings-for-azure-load-balancer"></a><span data-ttu-id="6a1a5-103">Configuration des paramètres de délai d’inactivité et d’expiration TCP pour Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="6a1a5-103">Configure TCP idle timeout settings for Azure Load Balancer</span></span>

<span data-ttu-id="6a1a5-104">Dans sa configuration par défaut, l’équilibrage de charge Azure a un paramètre de délai d’inactivité de 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-104">In its default configuration, Azure Load Balancer has an idle timeout setting of 4 minutes.</span></span> <span data-ttu-id="6a1a5-105">Si une période d’inactivité est supérieure à la valeur de délai d’expiration, il n’est pas garanti que la session TCP ou HTTP est maintenue entre le client et votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-105">If a period of inactivity is longer than the timeout value, there's no guarantee that the TCP or HTTP session is maintained between the client and your cloud service.</span></span>

<span data-ttu-id="6a1a5-106">Lorsque la connexion est fermée, votre application cliente peut obtenir un message d’erreur de ce type : « La connexion sous-jacente a été fermée : le serveur a fermé une connexion qui devait être maintenue active ».</span><span class="sxs-lookup"><span data-stu-id="6a1a5-106">When the connection is closed, your client application may receive the following error message: "The underlying connection was closed: A connection that was expected to be kept alive was closed by the server."</span></span>

<span data-ttu-id="6a1a5-107">Une pratique courante consiste à utiliser TCP keep-alive.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-107">A common practice is to use a TCP keep-alive.</span></span> <span data-ttu-id="6a1a5-108">Cela permet de maintenir la connexion active pendant une période plus longue.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-108">This practice keeps the connection active for a longer period.</span></span> <span data-ttu-id="6a1a5-109">Pour plus d’informations, consultez ces [exemples .NET](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a1a5-109">For more information, see these [.NET examples](https://msdn.microsoft.com/library/system.net.servicepoint.settcpkeepalive.aspx).</span></span> <span data-ttu-id="6a1a5-110">avec keep-alive activé, les paquets sont envoyés au cours des périodes d’inactivité sur la connexion.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-110">With keep-alive enabled, packets are sent during periods of inactivity on the connection.</span></span> <span data-ttu-id="6a1a5-111">Ces paquets keep-alive garantissent que la valeur de délai d’inactivité n’est jamais atteinte et que la connexion est maintenue pendant une longue période.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-111">These keep-alive packets ensure that the idle timeout value is never reached and the connection is maintained for a long period.</span></span>

<span data-ttu-id="6a1a5-112">Ce paramètre fonctionne uniquement pour les connexions entrantes.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-112">This setting works for inbound connections only.</span></span> <span data-ttu-id="6a1a5-113">Pour éviter la perte de la connexion, vous devez configurer TCP keep-alive sur un intervalle inférieur au paramètre de délai d’inactivité ou augmentez la valeur du délai d’inactivité.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-113">To avoid losing the connection, you must configure the TCP keep-alive with an interval less than the idle timeout setting or increase the idle timeout value.</span></span> <span data-ttu-id="6a1a5-114">Pour prendre en charge ces scénarios, nous avons ajouté la prise en charge d’un délai d’inactivité configurable.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-114">To support such scenarios, we've added support for a configurable idle timeout.</span></span> <span data-ttu-id="6a1a5-115">Vous pouvez maintenant le définir sur une durée comprise entre 4 et 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-115">You can now set it for a duration of 4 to 30 minutes.</span></span>

<span data-ttu-id="6a1a5-116">TCP keep-alive fonctionne bien pour les scénarios où l’autonomie de la batterie n’est pas une contrainte.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-116">TCP keep-alive works well for scenarios where battery life is not a constraint.</span></span> <span data-ttu-id="6a1a5-117">Il n’est pas recommandé de l’utiliser pour les applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-117">It is not recommended for mobile applications.</span></span> <span data-ttu-id="6a1a5-118">L’utilisation de TCP keep-alive depuis une application mobile peut décharger la batterie de l’appareil plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-118">Using a TCP keep-alive in a mobile application can drain the device battery faster.</span></span>

![Délai d’expiration TCP](./media/load-balancer-tcp-idle-timeout/image1.png)

<span data-ttu-id="6a1a5-120">Les sections suivantes décrivent comment modifier les paramètres de délai d’inactivité dans les machines virtuelles et les services cloud.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-120">The following sections describe how to change idle timeout settings in virtual machines and cloud services.</span></span>

## <a name="configure-the-tcp-timeout-for-your-instance-level-public-ip-to-15-minutes"></a><span data-ttu-id="6a1a5-121">Configurer le délai d’expiration TCP pour votre adresse IP publique de niveau instance à 15 minutes</span><span class="sxs-lookup"><span data-stu-id="6a1a5-121">Configure the TCP timeout for your instance-level public IP to 15 minutes</span></span>

```powershell
Set-AzurePublicIP -PublicIPName webip -VM MyVM -IdleTimeoutInMinutes 15
```

<span data-ttu-id="6a1a5-122">`IdleTimeoutInMinutes` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-122">`IdleTimeoutInMinutes` is optional.</span></span> <span data-ttu-id="6a1a5-123">Si cela n'est pas défini, le délai d'expiration par défaut est de 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-123">If it is not set, the default timeout is 4 minutes.</span></span> <span data-ttu-id="6a1a5-124">La plage de délai d’expiration acceptable est comprise entre 4 et 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-124">The acceptable timeout range is 4 to 30 minutes.</span></span>

## <a name="set-the-idle-timeout-when-creating-an-azure-endpoint-on-a-virtual-machine"></a><span data-ttu-id="6a1a5-125">Définir le délai d’inactivité pendant la création d’un point de terminaison Azure sur une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="6a1a5-125">Set the idle timeout when creating an Azure endpoint on a virtual machine</span></span>

<span data-ttu-id="6a1a5-126">Pour modifier le paramètre de délai d’attente pour un point de terminaison, utilisez ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="6a1a5-126">To change the timeout setting for an endpoint, use the following:</span></span>

```powershell
Get-AzureVM -ServiceName "mySvc" -Name "MyVM1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 8080 -IdleTimeoutInMinutes 15| Update-AzureVM
```

<span data-ttu-id="6a1a5-127">Pour récupérer votre configuration du délai d’inactivité, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="6a1a5-127">To retrieve your idle timeout configuration, use the following command:</span></span>

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

## <a name="set-the-tcp-timeout-on-a-load-balanced-endpoint-set"></a><span data-ttu-id="6a1a5-128">Définir le délai d’expiration TCP sur un jeu de points de terminaison d’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a1a5-128">Set the TCP timeout on a load-balanced endpoint set</span></span>

<span data-ttu-id="6a1a5-129">Si les points de terminaison font partie d'un jeu de points de terminaison d'équilibrage de charge, le délai d'expiration TCP doit être défini sur le jeu de points de terminaison d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-129">If endpoints are part of a load-balanced endpoint set, the TCP timeout must be set on the load-balanced endpoint set.</span></span> <span data-ttu-id="6a1a5-130">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6a1a5-130">For example:</span></span>

```powershell
Set-AzureLoadBalancedEndpoint -ServiceName "MyService" -LBSetName "LBSet1" -Protocol tcp -LocalPort 80 -ProbeProtocolTCP -ProbePort 8080 -IdleTimeoutInMinutes 15
```

## <a name="change-timeout-settings-for-cloud-services"></a><span data-ttu-id="6a1a5-131">Modifier les paramètres de délai d’expiration pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="6a1a5-131">Change timeout settings for cloud services</span></span>

<span data-ttu-id="6a1a5-132">Vous pouvez utiliser le Kit de développement logiciel (SDK) Azure pour mettre à jour votre service cloud.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-132">You can use the Azure SDK to update your cloud service.</span></span> <span data-ttu-id="6a1a5-133">Les paramètres de point de terminaison des services cloud sont définis dans le fichier .csdef.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-133">You make endpoint settings for cloud services in the .csdef file.</span></span> <span data-ttu-id="6a1a5-134">La mise à jour du délai d’expiration TCP pour le déploiement d’un service cloud requiert une mise à niveau du déploiement.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-134">Updating the TCP timeout for deployment of a cloud service requires a deployment upgrade.</span></span> <span data-ttu-id="6a1a5-135">L’exception est si le délai d’expiration TCP n’est spécifié que pour une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-135">An exception is if the TCP timeout is specified only for a public IP.</span></span> <span data-ttu-id="6a1a5-136">Les paramètres d’adresse IP publique sont définis dans le fichier .cscfg et peuvent être mis à jour via une mise à jour et une mise à niveau du déploiement.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-136">Public IP settings are in the .cscfg file, and you can update them through deployment update and upgrade.</span></span>

<span data-ttu-id="6a1a5-137">Les modifications apportées aux paramètres de point de terminaison dans .csdef sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6a1a5-137">The .csdef changes for endpoint settings are:</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" idleTimeoutInMinutes="tcp-timeout" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="6a1a5-138">Les modifications de .cscfg pour le paramètre de délai d’expiration sur des adresses IP publiques sont :</span><span class="sxs-lookup"><span data-stu-id="6a1a5-138">The .cscfg changes for the timeout setting on public IPs are:</span></span>

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

## <a name="rest-api-example"></a><span data-ttu-id="6a1a5-139">Exemple d’API REST</span><span class="sxs-lookup"><span data-stu-id="6a1a5-139">REST API example</span></span>

<span data-ttu-id="6a1a5-140">Vous pouvez configurer le délai d’inactivité TCP à l’aide de l’API Gestion des services.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-140">You can configure the TCP idle timeout by using the service management API.</span></span> <span data-ttu-id="6a1a5-141">Assurez-vous que l’en-tête `x-ms-version` est défini sur la version `2014-06-01` ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-141">Make sure that the `x-ms-version` header is set to version `2014-06-01` or later.</span></span> <span data-ttu-id="6a1a5-142">Mettre à jour la configuration des points de terminaison d’entrée d’équilibrage de charge spécifiés sur toutes les machines virtuelles d’un déploiement.</span><span class="sxs-lookup"><span data-stu-id="6a1a5-142">Update the configuration of the specified load-balanced input endpoints on all virtual machines in a deployment.</span></span>

### <a name="request"></a><span data-ttu-id="6a1a5-143">Demande</span><span class="sxs-lookup"><span data-stu-id="6a1a5-143">Request</span></span>

    POST https://management.core.windows.net/<subscription-id>/services/hostedservices/<cloudservice-name>/deployments/<deployment-name>

### <a name="response"></a><span data-ttu-id="6a1a5-144">Réponse</span><span class="sxs-lookup"><span data-stu-id="6a1a5-144">Response</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6a1a5-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a1a5-145">Next steps</span></span>

[<span data-ttu-id="6a1a5-146">Présentation de l’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="6a1a5-146">Internal load balancer overview</span></span>](load-balancer-internal-overview.md)

[<span data-ttu-id="6a1a5-147">Prise en main de la configuration d’un équilibrage de charge accessible sur Internet</span><span class="sxs-lookup"><span data-stu-id="6a1a5-147">Get started configuring an Internet-facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="6a1a5-148">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="6a1a5-148">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)
