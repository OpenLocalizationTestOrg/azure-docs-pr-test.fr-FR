---
title: "le routage dans un classique de réseau virtuel Azure - PowerShell - aaaControl | Documents Microsoft"
description: "Découvrez comment toocontrol routage dans des réseaux virtuels à l’aide de PowerShell | Classique"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="411fd-103">Contrôle du routage et utilisation des appliances virtuelles (classiques) à l'aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="411fd-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="411fd-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="411fd-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="411fd-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="411fd-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="411fd-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="411fd-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="411fd-107">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="411fd-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="411fd-108">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="411fd-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="411fd-109">Avant d’utiliser des ressources Azure, il est important toounderstand que Azure dispose actuellement de deux modèles de déploiement : le Gestionnaire de ressources Azure et classique.</span><span class="sxs-lookup"><span data-stu-id="411fd-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="411fd-110">Veillez à bien comprendre les [modèles et outils de déploiement](../azure-resource-manager/resource-manager-deployment-model.md) avant d’utiliser une ressource Azure.</span><span class="sxs-lookup"><span data-stu-id="411fd-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="411fd-111">Vous pouvez afficher la documentation hello pour différents outils en sélectionnant une option haut hello de cet article.</span><span class="sxs-lookup"><span data-stu-id="411fd-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="411fd-112">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="411fd-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="411fd-113">l’exemple Hello Azure PowerShell commandes ci-dessous attendent un simple environnement déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="411fd-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="411fd-114">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, créer l’environnement hello [créer un réseau virtuel (classiques) à l’aide de PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="411fd-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="411fd-115">Créer hello UDR pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="411fd-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="411fd-116">table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="411fd-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="411fd-117">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau frontal de hello :</span><span class="sxs-lookup"><span data-stu-id="411fd-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="411fd-118">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="411fd-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="411fd-119">Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **frontal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="411fd-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="411fd-120">Créer hello UDR pour le sous-réseau principal de hello</span><span class="sxs-lookup"><span data-stu-id="411fd-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="411fd-121">table d’itinéraires toocreate hello et d’itinéraire si nécessaire pour la sauvegarde de hello fin sous-réseau selon le scénario de hello, terminer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="411fd-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="411fd-122">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :</span><span class="sxs-lookup"><span data-stu-id="411fd-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="411fd-123">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="411fd-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="411fd-124">Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="411fd-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="411fd-125">Activer le transfert IP sur hello FW1 VM</span><span class="sxs-lookup"><span data-stu-id="411fd-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="411fd-126">transfert IP tooenable Bonjour FW1 VM, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="411fd-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="411fd-127">Exécutez hello suivant l’état du transfert IP hello de toocheck la commande :</span><span class="sxs-lookup"><span data-stu-id="411fd-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="411fd-128">Suivante d’exécution hello commande tooenable le transfert IP pour hello *FW1* machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="411fd-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
