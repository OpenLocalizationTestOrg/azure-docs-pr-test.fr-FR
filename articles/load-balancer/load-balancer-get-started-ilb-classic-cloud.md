---
title: "aaaCreate un équilibreur de charge interne pour les Services de Cloud Azure | Documents Microsoft"
description: "Découvrez comment toocreate un interne l’équilibrage de charge à l’aide de PowerShell dans le modèle de déploiement classique de hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 57966056-0f46-4f95-a295-483ca1ad135d
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: fe7975bca7bec3248626b0ad0fad6823e278ade2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-for-cloud-services"></a><span data-ttu-id="fe2e4-103">Prise en main de la création d’un équilibreur de charge interne (Classic) pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="fe2e4-103">Get started creating an internal load balancer (classic) for cloud services</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="fe2e4-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fe2e4-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="fe2e4-105">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="fe2e4-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="fe2e4-106">Services cloud</span><span class="sxs-lookup"><span data-stu-id="fe2e4-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

> [!IMPORTANT]
> <span data-ttu-id="fe2e4-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fe2e4-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="fe2e4-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="fe2e4-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fe2e4-110">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](load-balancer-get-started-ilb-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="fe2e4-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-ps.md).</span></span>

## <a name="configure-internal-load-balancer-for-cloud-services"></a><span data-ttu-id="fe2e4-111">Configurer l’équilibreur de charge interne pour les services cloud</span><span class="sxs-lookup"><span data-stu-id="fe2e4-111">Configure internal load balancer for cloud services</span></span>

<span data-ttu-id="fe2e4-112">L’équilibreur de charge interne est pris en charge pour les machines virtuelles et les services cloud.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-112">Internal load balancer is supported for both virtual machines and cloud services.</span></span> <span data-ttu-id="fe2e4-113">Un point de terminaison de programme d’équilibrage de charge interne créé dans un service cloud qui est en dehors d’un réseau virtuel régional est accessibles uniquement dans le service de cloud computing hello.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-113">An internal load balancer endpoint created in a cloud service that is outside a regional virtual network will be accessible only within hello cloud service.</span></span>

<span data-ttu-id="fe2e4-114">configuration d’équilibrage de charge interne Hello a toobe défini pendant la création de hello du premier déploiement de hello dans le service cloud hello, comme indiqué dans l’exemple hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-114">hello internal load balancer configuration has toobe set during hello creation of hello first deployment in hello cloud service, as shown in hello sample below.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe2e4-115">Étapes d’un hello toorun requis ci-dessous est toohave un réseau virtuel déjà créé pour le déploiement de cloud hello.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-115">A prerequisite toorun hello steps below is toohave a virtual network already created for hello cloud deployment.</span></span> <span data-ttu-id="fe2e4-116">Vous devez hello réseau virtuel nom et le sous-réseau nom toocreate hello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-116">You will need hello virtual network name and subnet name toocreate hello Internal Load Balancing.</span></span>

### <a name="step-1"></a><span data-ttu-id="fe2e4-117">Étape 1</span><span class="sxs-lookup"><span data-stu-id="fe2e4-117">Step 1</span></span>

<span data-ttu-id="fe2e4-118">Ouvrez le fichier de configuration de service hello (.cscfg) pour votre déploiement de cloud dans Visual Studio et ajouter hello suivant hello de toocreate section équilibrage de charge interne sous hello dernière »`</Role>`« élément de configuration du réseau hello.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-118">Open hello service configuration file (.cscfg) for your cloud deployment in Visual Studio and add hello following section toocreate hello Internal Load Balancing under hello last "`</Role>`" item for hello network configuration.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="name of hello load balancer">
        <FrontendIPConfiguration type="private" subnet="subnet-name" staticVirtualNetworkIPAddress="static-IP-address"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="fe2e4-119">Vous allez ajouter les valeurs hello pour hello réseau configuration fichier tooshow aspect.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-119">Let's add hello values for hello network configuration file tooshow how it will look.</span></span> <span data-ttu-id="fe2e4-120">Dans l’exemple de hello, supposons que vous avez créé un réseau virtuel appelé « test_vnet » avec un sous-réseau 10.0.0.0/24 appelé test_subnet et une adresse IP statique 10.0.0.4.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-120">In hello example, assume you created a VNet called "test_vnet" with a subnet 10.0.0.0/24 called test_subnet and a static IP 10.0.0.4.</span></span> <span data-ttu-id="fe2e4-121">équilibrage de charge Hello sera nommé testLB.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-121">hello load balancer will be named testLB.</span></span>

```xml
<NetworkConfiguration>
    <LoadBalancers>
    <LoadBalancer name="testLB">
        <FrontendIPConfiguration type="private" subnet="test_subnet" staticVirtualNetworkIPAddress="10.0.0.4"/>
    </LoadBalancer>
    </LoadBalancers>
</NetworkConfiguration>
```

<span data-ttu-id="fe2e4-122">Pour plus d’informations sur le schéma de programme d’équilibrage de charge hello, consultez [équilibrage de charge ajouter](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe2e4-122">For more information about hello load balancer schema, see [Add load balancer](https://msdn.microsoft.com/library/azure/dn722411.aspx).</span></span>

### <a name="step-2"></a><span data-ttu-id="fe2e4-123">Étape 2</span><span class="sxs-lookup"><span data-stu-id="fe2e4-123">Step 2</span></span>

<span data-ttu-id="fe2e4-124">Modifier hello service (.csdef) de définition fichier tooadd points de terminaison toohello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-124">Change hello service definition (.csdef) file tooadd endpoints toohello Internal Load Balancing.</span></span> <span data-ttu-id="fe2e4-125">moment de Hello une instance de rôle est créée, le fichier de définition de service hello ajoute toohello d’instances de rôle hello équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-125">hello moment a role instance is created, hello service definition file will add hello role instances toohello Internal Load Balancing.</span></span>

```xml
<WorkerRole name="worker-role-name" vmsize="worker-role-size" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="input-endpoint-name" protocol="[http|https|tcp|udp]" localPort="local-port-number" port="port-number" certificate="certificate-name" loadBalancerProbe="load-balancer-probe-name" loadBalancer="load-balancer-name" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="fe2e4-126">Suite hello les mêmes valeurs à partir de l’exemple hello ci-dessus, vous allez ajouter le fichier de définition de service hello valeurs toohello.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-126">Following hello same values from hello example above, let's add hello values toohello service definition file.</span></span>

```xml
<WorkerRole name="WorkerRole1" vmsize="A7" enableNativeCodeExecution="[true|false]">
    <Endpoints>
    <InputEndpoint name="endpoint1" protocol="http" localPort="80" port="80" loadBalancer="testLB" />
    </Endpoints>
</WorkerRole>
```

<span data-ttu-id="fe2e4-127">le trafic réseau de Hello sera équilibrée à l’aide d’équilibrage de charge hello testLB utilise le port 80 pour les demandes entrantes, envoi tooworker instances de rôle également sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="fe2e4-127">hello network traffic will be load balanced using hello testLB load balancer using port 80 for incoming requests, sending tooworker role instances also on port 80.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fe2e4-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fe2e4-128">Next steps</span></span>

[<span data-ttu-id="fe2e4-129">Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="fe2e4-129">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="fe2e4-130">Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="fe2e4-130">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

