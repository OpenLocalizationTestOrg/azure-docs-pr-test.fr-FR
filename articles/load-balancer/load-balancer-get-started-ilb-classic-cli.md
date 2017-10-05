---
title: "Créer un équilibrage de charge interne à l’aide de la CLI Azure dans le modèle de déploiement classique | Microsoft Docs"
description: "Découvrez comment créer un équilibreur de charge interne à l'aide de l’interface de ligne de commande Azure (CLI) dans le modèle de déploiement classique"
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
ms.openlocfilehash: d24b95f75b5ffd1116b07cf9f8bac33767a9c835
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-the-azure-cli"></a><span data-ttu-id="c61d7-103">Créer un équilibreur de charge interne (classique) à l’aide de l’interface de ligne de commande (CLI) Azure</span><span class="sxs-lookup"><span data-stu-id="c61d7-103">Get started creating an internal load balancer (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c61d7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c61d7-104">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [<span data-ttu-id="c61d7-105">interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c61d7-105">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [<span data-ttu-id="c61d7-106">Services cloud</span><span class="sxs-lookup"><span data-stu-id="c61d7-106">Cloud services</span></span>](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="c61d7-107">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c61d7-107">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="c61d7-108">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="c61d7-108">This article covers using the classic deployment model.</span></span> <span data-ttu-id="c61d7-109">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c61d7-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c61d7-110">Découvrez comment [effectuer ces étapes à l’aide du modèle Resource Manager](load-balancer-get-started-ilb-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c61d7-110">Learn how to [perform these steps using the Resource Manager model](load-balancer-get-started-ilb-arm-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="to-create-an-internal-load-balancer-set-for-virtual-machines"></a><span data-ttu-id="c61d7-111">Pour créer un jeu d’équilibrage de charge interne pour les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="c61d7-111">To create an internal load balancer set for virtual machines</span></span>

<span data-ttu-id="c61d7-112">Pour créer un jeu d'équilibrage de charge interne et les serveurs qui y enverront leur trafic, vous devez procéder comme suit :</span><span class="sxs-lookup"><span data-stu-id="c61d7-112">To create an internal load balancer set and the servers that will send their traffic to it, you must do the following:</span></span>

1. <span data-ttu-id="c61d7-113">Créez une instance d’équilibrage de charge qui sera le point de terminaison du trafic entrant qui devra être équilibré entre les serveurs d’un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c61d7-113">Create an instance of Internal Load Balancing that will be the endpoint of incoming traffic to be load balanced across the servers of a load-balanced set.</span></span>
2. <span data-ttu-id="c61d7-114">Ajoutez des points de terminaison correspondants aux machines virtuelles qui recevront le trafic entrant.</span><span class="sxs-lookup"><span data-stu-id="c61d7-114">Add endpoints corresponding to the virtual machines that will be receiving the incoming traffic.</span></span>
3. <span data-ttu-id="c61d7-115">Configurez les serveurs qui enverront le trafic avec une charge équilibrée pour envoyer leur trafic à l’adresse IP virtuelle (VIP) de l’instance d’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="c61d7-115">Configure the servers that will be sending the traffic to be load balanced to send their traffic to the virtual IP (VIP) address of the Internal Load Balancing instance.</span></span>

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a><span data-ttu-id="c61d7-116">Créer par étapes un équilibreur de charge interne à l’aide de l’interface de ligne de commande CLI</span><span class="sxs-lookup"><span data-stu-id="c61d7-116">Step by step creating an internal load balancer using CLI</span></span>

<span data-ttu-id="c61d7-117">Ce guide indique comment créer un équilibreur de charge interne selon le scénario ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c61d7-117">This guide shows how to create an internal load balancer based on the scenario above.</span></span>

1. <span data-ttu-id="c61d7-118">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez [Installer et configurer l’interface de ligne de commande Azure](../cli-install-nodejs.md) et suivez les instructions jusqu’à l’étape où vous sélectionnez votre compte et votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="c61d7-118">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="c61d7-119">Exécutez la commande **azure config mode** pour passer en mode classique, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c61d7-119">Run the **azure config mode** command to switch to classic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="c61d7-120">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="c61d7-120">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="c61d7-121">Création d'un point de terminaison et d'un jeu d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c61d7-121">Create endpoint and load balancer set</span></span>

<span data-ttu-id="c61d7-122">Le scénario suppose que les machines virtuelles « DB1 » et « DB2 » figurent dans un service cloud appelé « mytestcloud ».</span><span class="sxs-lookup"><span data-stu-id="c61d7-122">The scenario assumes the virtual machines "DB1" and "DB2" in a cloud service called "mytestcloud".</span></span> <span data-ttu-id="c61d7-123">Ces deux machines virtuelles utilisent un réseau virtuel appelé mon « testvnet » avec un sous-réseau « sous-réseau-1 ».</span><span class="sxs-lookup"><span data-stu-id="c61d7-123">Both virtual machines are using a virtual network called my "testvnet" with subnet "subnet-1".</span></span>

<span data-ttu-id="c61d7-124">Ce guide créera un jeu d'équilibrage de charge en utilisant le port 1433 comme port privé et 1433 comme port local.</span><span class="sxs-lookup"><span data-stu-id="c61d7-124">This guide will create an internal load balancer set using port 1433 as private port and 1433 as local port.</span></span>

<span data-ttu-id="c61d7-125">Il s'agit d'un scénario courant dans lequel vous utilisez des machines virtuelles SQL sur le serveur principal avec un équilibreur de charge interne afin de garantir que les serveurs de base de données ne soient pas exposés directement à l'aide d'une adresse IP publique.</span><span class="sxs-lookup"><span data-stu-id="c61d7-125">This is a common scenario where you have SQL virtual machines on the back end using an internal load balancer to guarantee the database servers won't be exposed directly using a public IP address.</span></span>

### <a name="step-1"></a><span data-ttu-id="c61d7-126">Étape 1</span><span class="sxs-lookup"><span data-stu-id="c61d7-126">Step 1</span></span>

<span data-ttu-id="c61d7-127">Créer un jeu d’équilibrage de charge interne avec `azure network service internal-load-balancer add`.</span><span class="sxs-lookup"><span data-stu-id="c61d7-127">Create an internal load balancer set using `azure network service internal-load-balancer add`.</span></span>

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

<span data-ttu-id="c61d7-128">Pour plus d'informations, consultez `azure service internal-load-balancer --help` .</span><span class="sxs-lookup"><span data-stu-id="c61d7-128">Check out `azure service internal-load-balancer --help` for more information.</span></span>

<span data-ttu-id="c61d7-129">Vous pouvez vérifier les propriétés de l’équilibreur de charge interne à l'aide de la commande `azure service internal-load-balancer list` *nom du service cloud*.</span><span class="sxs-lookup"><span data-stu-id="c61d7-129">You can check the internal load balancer properties using the command `azure service internal-load-balancer list` *cloud service name*.</span></span>

<span data-ttu-id="c61d7-130">Voici un exemple de sortie :</span><span class="sxs-lookup"><span data-stu-id="c61d7-130">Here follows an example of the output:</span></span>

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a><span data-ttu-id="c61d7-131">Étape 2</span><span class="sxs-lookup"><span data-stu-id="c61d7-131">Step 2</span></span>

<span data-ttu-id="c61d7-132">Vous configurez le jeu d'équilibrage de charge interne lorsque vous ajoutez le premier point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="c61d7-132">You configure the internal load balancer set when you add the first endpoint.</span></span> <span data-ttu-id="c61d7-133">Vous associerez le point de terminaison, la machine virtuelle et le port de sonde au jeu d'équilibrage de charge interne au cours de cette étape.</span><span class="sxs-lookup"><span data-stu-id="c61d7-133">You will associate the endpoint, virtual machine and probe port to the internal load balancer set in this step.</span></span>

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a><span data-ttu-id="c61d7-134">Étape 3</span><span class="sxs-lookup"><span data-stu-id="c61d7-134">Step 3</span></span>

<span data-ttu-id="c61d7-135">Vérifier la configuration de l’équilibreur de charge avec `azure vm show` *nom de la machine virtuelle*</span><span class="sxs-lookup"><span data-stu-id="c61d7-135">Verify the load balancer configuration using `azure vm show` *virtual machine name*</span></span>

```azurecli
azure vm show DB1
```

<span data-ttu-id="c61d7-136">La sortie se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="c61d7-136">The output will be:</span></span>

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

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="c61d7-137">Création d'un point de terminaison de Bureau à distance pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="c61d7-137">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="c61d7-138">Vous pouvez créer un point de terminaison de Bureau à distance pour transférer le trafic réseau à partir d’un port public vers un port local pour une machine virtuelle spécifique à l’aide d’ `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="c61d7-138">You can create a remote desktop endpoint to forward network traffic from a public port to a local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="c61d7-139">Suppression d’une machine virtuelle de l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="c61d7-139">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="c61d7-140">Vous pouvez supprimer une machine virtuelle d'un jeu d’équilibrage de charge interne en supprimant le point de terminaison associé.</span><span class="sxs-lookup"><span data-stu-id="c61d7-140">You can remove a virtual machine from an internal load balancer set by deleting the associated endpoint.</span></span> <span data-ttu-id="c61d7-141">Une fois le point de terminaison supprimé, la machine virtuelle n'appartient plus au jeu d'équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="c61d7-141">Once the endpoint is removed, the virtual machine won't belong to the load balancer set anymore.</span></span>

<span data-ttu-id="c61d7-142">À l’aide de l’exemple ci-dessus, vous pouvez supprimer le point de terminaison créé pour la machine virtuelle « DB1 » de l’équilibreur de charge interne « ilbset » à l’aide de la commande `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="c61d7-142">Using the example above, you can remove the endpoint created for virtual machine "DB1" from internal load balancer "ilbset" by using the command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

<span data-ttu-id="c61d7-143">Pour plus d'informations, consultez `azure vm endpoint --help` .</span><span class="sxs-lookup"><span data-stu-id="c61d7-143">Check out `azure vm endpoint --help` for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c61d7-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c61d7-144">Next steps</span></span>

[<span data-ttu-id="c61d7-145">Configurer le mode de distribution d’équilibreur de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="c61d7-145">Configure a load balancer distribution mode using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="c61d7-146">Configuration des paramètres de délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="c61d7-146">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
