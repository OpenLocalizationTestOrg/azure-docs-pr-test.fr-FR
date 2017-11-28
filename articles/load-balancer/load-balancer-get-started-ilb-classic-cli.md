---
title: "aaaCreate un interne l’équilibrage de charge - CLI d’Azure classic | Documents Microsoft"
description: "Découvrez comment un équilibreur de charge interne à l’aide de toocreate hello CLI d’Azure dans le modèle de déploiement classique de hello"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a><span data-ttu-id="43ce8-103">Prise en main la création d’un équilibreur de charge interne (classique) à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="43ce8-103">Get started creating an internal load balancer (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="43ce8-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="43ce8-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="43ce8-105">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="43ce8-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="43ce8-106">Services cloud</span><span class="sxs-lookup"><span data-stu-id="43ce8-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="43ce8-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="43ce8-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="43ce8-108">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="43ce8-108">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="43ce8-109">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="43ce8-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="43ce8-110">Découvrez comment trop[effectuer ces étapes à l’aide du modèle de gestionnaire de ressources hello](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="43ce8-110">Learn how too[perform these steps using hello Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="43ce8-111">toocreate un équilibreur de charge interne défini pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="43ce8-111">toocreate an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="43ce8-112">toocreate un équilibreur de charge interne défini et hello serveurs qui y enverront leur tooit le trafic, vous devez procéder comme suit de hello :</span><span class="sxs-lookup"><span data-stu-id="43ce8-112">toocreate an internal load balancer set and hello servers that will send their traffic tooit, you must do hello following:</span></span>

1. <span data-ttu-id="43ce8-113">Créer une instance d’interne l’équilibrage de charge qui sera le point de terminaison hello d’entrant trafic toobe équilibrée entre les serveurs hello d’un jeu d’équilibrage de la charge.</span><span class="sxs-lookup"><span data-stu-id="43ce8-113">Create an instance of Internal Load Balancing that will be hello endpoint of incoming traffic toobe load balanced across hello servers of a load-balanced set.</span></span>
2. <span data-ttu-id="43ce8-114">Ajoutez les machines virtuelles toohello qui recevront le trafic entrant de hello correspondantes des points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="43ce8-114">Add endpoints corresponding toohello virtual machines that will be receiving hello incoming traffic.</span></span>
3. <span data-ttu-id="43ce8-115">Configurez les serveurs hello qui enverront hello trafic toobe à charge équilibrée toosend leur trafic toohello adresse IP virtuelle (VIP) de l’instance d’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="43ce8-115">Configure hello servers that will be sending hello traffic toobe load balanced toosend their traffic toohello virtual IP (VIP) address of hello Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="43ce8-116">Créer par étapes un équilibreur de charge interne à l’aide de l’interface de ligne de commande CLI</span><span class="sxs-lookup"><span data-stu-id="43ce8-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="43ce8-117">Ce guide montre comment toocreate un équilibreur de charge interne selon hello scénario ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="43ce8-117">This guide shows how toocreate an internal load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="43ce8-118">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="43ce8-118">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="43ce8-119">Exécutez hello **configuration azure mode** mode commande tooswitch tooclassic, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="43ce8-119">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="43ce8-120">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="43ce8-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="43ce8-121">Création d'un point de terminaison et d'un jeu d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="43ce8-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="43ce8-122">scénario de Hello suppose hello des machines virtuelles « DB1 » et « DB2 » dans un service cloud appelé « mytestcloud ».</span><span class="sxs-lookup"><span data-stu-id="43ce8-122">hello scenario assumes hello virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="43ce8-123">Ces deux machines virtuelles utilisent un réseau virtuel appelé mon « testvnet » avec un sous-réseau « sous-réseau-1 ».</span><span class="sxs-lookup"><span data-stu-id="43ce8-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="43ce8-124">Ce guide créera un jeu d'équilibrage de charge en utilisant le port 1433 comme port privé et 1433 comme port local.</span><span class="sxs-lookup"><span data-stu-id="43ce8-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="43ce8-125">Il s’agit d’un scénario courant où vous avez des machines virtuelles SQL sur l’utilisation de back-end hello que ne sera pas exposé un serveurs de base de données de charge interne équilibrage tooguarantee hello directement à l’aide d’une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="43ce8-125">This is a common scenario where you have SQL virtual machines on hello back end using an internal load balancer tooguarantee hello database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="43ce8-126">Étape 1</span><span class="sxs-lookup"><span data-stu-id="43ce8-126">Step 1</span></span>

<span data-ttu-id="43ce8-127">Créer un jeu d’équilibrage de charge interne avec `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="43ce8-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="43ce8-128">Pour plus d'informations, consultez `azure service internal-load-balancer --help` .</span><span class="sxs-lookup"><span data-stu-id="43ce8-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="43ce8-129">Vous pouvez vérifier les propriétés de l’équilibrage de charge interne hello à l’aide de la commande hello `azure service internal-load-balancer list` *nom du service cloud*.</span><span class="sxs-lookup"><span data-stu-id="43ce8-129">You can check hello internal load balancer properties using hello command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="43ce8-130">Cet exemple suit un exemple de sortie de hello :</span><span class="sxs-lookup"><span data-stu-id="43ce8-130">Here follows an example of hello output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="43ce8-131">Étape 2</span><span class="sxs-lookup"><span data-stu-id="43ce8-131">Step 2</span></span>

<span data-ttu-id="43ce8-132">Vous configurez équilibreur de charge interne hello définir lorsque vous ajoutez le premier point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="43ce8-132">You configure hello internal load balancer set when you add hello first endpoint.</span></span> <span data-ttu-id="43ce8-133">Vous allez associer hello point de terminaison, de machines virtuelles et de sonde port toohello équilibreur de charge interne défini dans cette étape.</span><span class="sxs-lookup"><span data-stu-id="43ce8-133">You will associate hello endpoint, virtual machine and probe port toohello internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="43ce8-134">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="43ce8-134">Step 3</span></span>

<span data-ttu-id="43ce8-135">Vérifiez la configuration de hello d’équilibrage de charge avec `azure vm show` *nom d’ordinateur virtuel*</span><span class="sxs-lookup"><span data-stu-id="43ce8-135">Verify hello load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="43ce8-136">résultat de Hello sera :</span><span class="sxs-lookup"><span data-stu-id="43ce8-136">hello output will be:</span></span>

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="43ce8-137">Création d'un point de terminaison de Bureau à distance pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="43ce8-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="43ce8-138">Vous pouvez créer un trafic réseau de tooforward point de terminaison Bureau à distance à partir d’un port local tooa de port public pour un ordinateur virtuel spécifique à l’aide de `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="43ce8-138">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="43ce8-139">Suppression d’une machine virtuelle de l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="43ce8-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="43ce8-140">Vous pouvez supprimer un ordinateur virtuel à partir d’un équilibreur de charge interne défini par la suppression du point de terminaison hello associé.</span><span class="sxs-lookup"><span data-stu-id="43ce8-140">You can remove a virtual machine from an internal load balancer set by deleting hello associated endpoint.</span></span> <span data-ttu-id="43ce8-141">Une fois que le point de terminaison hello est supprimé, hello virtual machine n’appartiennent à équilibrage de charge toohello définie plus.</span><span class="sxs-lookup"><span data-stu-id="43ce8-141">Once hello endpoint is removed, hello virtual machine won't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="43ce8-142">À l’aide d’exemple hello ci-dessus, vous pouvez supprimer le point de terminaison de hello créé pour l’ordinateur virtuel « DB1 » à partir de l’équilibreur de charge interne « ilbset » en à l’aide de la commande hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="43ce8-142">Using hello example above, you can remove hello endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="43ce8-143">Pour plus d'informations, consultez `azure vm endpoint --help` .</span><span class="sxs-lookup"><span data-stu-id="43ce8-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43ce8-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="43ce8-144">Next steps</span></span>

[<span data-ttu-id="43ce8-145">Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="43ce8-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="43ce8-146">Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="43ce8-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
