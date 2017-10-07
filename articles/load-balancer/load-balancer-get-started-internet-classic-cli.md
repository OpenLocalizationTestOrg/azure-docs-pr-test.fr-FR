---
title: "aaaCreate une côté Internet l’équilibrage de charge - CLI d’Azure classic | Documents Microsoft"
description: "Découvrez comment toocreate un équilibrage de charge exposés à Internet à l’aide de modèle de déploiement classique hello CLI d’Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: e433a824-4a8a-44d2-8765-a74f52d4e584
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: e6070cbc574f74bca0cccb960ff192847d6511bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-hello-azure-cli"></a><span data-ttu-id="38ea0-103">Commencer à créer un Internet faisant face à l’équilibrage de charge (classiques) Bonjour CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="38ea0-103">Get started creating an Internet facing load balancer (classic) in hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="38ea0-104">portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="38ea0-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="38ea0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="38ea0-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="38ea0-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="38ea0-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="38ea0-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="38ea0-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="38ea0-108">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique.</span><span class="sxs-lookup"><span data-stu-id="38ea0-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="38ea0-109">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-classic-rm.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="38ea0-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="38ea0-110">Vous pouvez afficher la documentation hello pour différents outils en cliquant sur les onglets hello haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="38ea0-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="38ea0-111">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="38ea0-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="38ea0-112">Vous pouvez également [apprendre comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="38ea0-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="step-by-step-creating-an-internet-facing-load-balancer-using-cli"></a><span data-ttu-id="38ea0-113">Création par étapes d’un équilibreur de charge accessible sur Internet à l’aide de l’interface de ligne de commande CLI</span><span class="sxs-lookup"><span data-stu-id="38ea0-113">Step by step creating an Internet facing load balancer using CLI</span></span>

<span data-ttu-id="38ea0-114">Ce guide montre comment toocreate un équilibrage de charge d’Internet selon hello scénario ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="38ea0-114">This guide shows how toocreate an Internet load balancer based on hello scenario above.</span></span>

1. <span data-ttu-id="38ea0-115">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="38ea0-115">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="38ea0-116">Exécutez hello **configuration azure mode** mode commande tooswitch tooclassic, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="38ea0-116">Run hello **azure config mode** command tooswitch tooclassic mode, as shown below.</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="38ea0-117">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="38ea0-117">Expected output:</span></span>

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a><span data-ttu-id="38ea0-118">Création d'un point de terminaison et d'un jeu d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="38ea0-118">Create endpoint and load balancer set</span></span>

<span data-ttu-id="38ea0-119">scénario de Hello suppose que les ordinateurs virtuels hello « web1 » et « web2 » ont été créés.</span><span class="sxs-lookup"><span data-stu-id="38ea0-119">hello scenario assumes hello virtual machines "web1" and "web2" were created.</span></span>
<span data-ttu-id="38ea0-120">Ce guide crée un ensemble d’équilibreurs de charge à l’aide du port 80 comme port public et du port 80 comme port local.</span><span class="sxs-lookup"><span data-stu-id="38ea0-120">This guide will create a load balancer set using port 80 as public port and port 80 as local port.</span></span> <span data-ttu-id="38ea0-121">Un port de la sonde est également configuré sur le port 80 et équilibrage de charge nommé hello définie « lbset ».</span><span class="sxs-lookup"><span data-stu-id="38ea0-121">A probe port is also configured on port 80 and named hello load balancer set "lbset".</span></span>

### <a name="step-1"></a><span data-ttu-id="38ea0-122">Étape 1</span><span class="sxs-lookup"><span data-stu-id="38ea0-122">Step 1</span></span>

<span data-ttu-id="38ea0-123">Créer le premier point de terminaison hello et à l’aide de l’équilibrage de charge `azure network vm endpoint create` pour l’ordinateur virtuel « web1 ».</span><span class="sxs-lookup"><span data-stu-id="38ea0-123">Create hello first endpoint and load balancer set using `azure network vm endpoint create` for virtual machine "web1".</span></span>

```azurecli
azure vm endpoint create web1 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-2"></a><span data-ttu-id="38ea0-124">Étape 2</span><span class="sxs-lookup"><span data-stu-id="38ea0-124">Step 2</span></span>

<span data-ttu-id="38ea0-125">Ajoutez un deuxième ensemble d’équilibrage de charge de l’ordinateur virtuel « web2 » toohello.</span><span class="sxs-lookup"><span data-stu-id="38ea0-125">Add a second virtual machine "web2" toohello load balancer set.</span></span>

```azurecli
azure vm endpoint create web2 80 --local-port 80 --protocol tcp --probe-port 80 --load-balanced-set-name lbset
```

## <a name="step-3"></a><span data-ttu-id="38ea0-126">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="38ea0-126">Step 3</span></span>

<span data-ttu-id="38ea0-127">Vérifiez la configuration de hello d’équilibrage de charge avec `azure vm show` .</span><span class="sxs-lookup"><span data-stu-id="38ea0-127">Verify hello load balancer configuration using `azure vm show` .</span></span>

```azurecli
azure vm show web1
```

<span data-ttu-id="38ea0-128">résultat de Hello sera :</span><span class="sxs-lookup"><span data-stu-id="38ea0-128">hello output will be:</span></span>

    data:    DNSName "contoso.cloudapp.net"
    data:    Location "East US"
    data:    VMName "web1"
    data:    IPAddress "10.0.0.5"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-2015
    6-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "joaoma-1-web1-0-201509251804250879"
    data:    OSDisk mediaLink "https://XXXXXXXXXXXXXXX.blob.core.windows.
    /vhds/joaomatest-web1-2015-09-25.vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Se
    r-2012-R2-20150916-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "XXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 name "XXXXXXXXXXXXXXXXXXXX"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    Network Endpoints 0 loadBalancedEndpointSetName "lbset"
    data:    Network Endpoints 0 localPort 80
    data:    Network Endpoints 0 name "tcp-80-80"
    data:    Network Endpoints 0 port 80
    data:    Network Endpoints 0 loadBalancerProbe port 80
    data:    Network Endpoints 0 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 0 loadBalancerProbe intervalInSeconds 15
    data:    Network Endpoints 0 loadBalancerProbe timeoutInSeconds 31
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 5986
    data:    Network Endpoints 1 name "PowerShell"
    data:    Network Endpoints 1 port 5986
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "XXXXXXXXXXXX"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 3389
    data:    Network Endpoints 2 name "Remote Desktop"
    data:    Network Endpoints 2 port 58081
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a><span data-ttu-id="38ea0-129">Création d'un point de terminaison de Bureau à distance pour une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="38ea0-129">Create a remote desktop endpoint for a virtual machine</span></span>

<span data-ttu-id="38ea0-130">Vous pouvez créer un trafic réseau de tooforward point de terminaison Bureau à distance à partir d’un port local tooa de port public pour un ordinateur virtuel spécifique à l’aide de `azure vm endpoint create`.</span><span class="sxs-lookup"><span data-stu-id="38ea0-130">You can create a remote desktop endpoint tooforward network traffic from a public port tooa local port for a specific virtual machine using `azure vm endpoint create`.</span></span>

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a><span data-ttu-id="38ea0-131">Suppression d’une machine virtuelle de l’équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="38ea0-131">Remove virtual machine from load balancer</span></span>

<span data-ttu-id="38ea0-132">Vous avez toohello de point de terminaison associé toodelete hello jeu d’équilibrage de charge de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="38ea0-132">You have toodelete hello endpoint associated toohello load balancer set from hello virtual machine.</span></span> <span data-ttu-id="38ea0-133">Une fois que le point de terminaison hello est supprimé, équilibrage de charge toohello définie plus n’appartient pas hello virtual machine.</span><span class="sxs-lookup"><span data-stu-id="38ea0-133">Once hello endpoint is removed, hello virtual machine doesn't belong toohello load balancer set anymore.</span></span>

<span data-ttu-id="38ea0-134">Avec exemple hello ci-dessus, vous pouvez supprimer le point de terminaison hello créé pour l’ordinateur virtuel « web1 » à partir de l’équilibrage de charge « lbset » à l’aide de la commande hello `azure vm endpoint delete`.</span><span class="sxs-lookup"><span data-stu-id="38ea0-134">Using hello example above, you can remove hello endpoint created for virtual machine "web1" from load balancer "lbset" using hello command `azure vm endpoint delete`.</span></span>

```azurecli
azure vm endpoint delete web1 tcp-80-80
```

> [!NOTE]
> <span data-ttu-id="38ea0-135">Vous pouvez Explorer plusieurs options toomanage points de terminaison à l’aide de la commande hello`azure vm endpoint --help`</span><span class="sxs-lookup"><span data-stu-id="38ea0-135">You can explore more options toomanage endpoints using hello command `azure vm endpoint --help`</span></span>

## <a name="next-steps"></a><span data-ttu-id="38ea0-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="38ea0-136">Next steps</span></span>

[<span data-ttu-id="38ea0-137">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="38ea0-137">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="38ea0-138">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="38ea0-138">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="38ea0-139">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="38ea0-139">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
