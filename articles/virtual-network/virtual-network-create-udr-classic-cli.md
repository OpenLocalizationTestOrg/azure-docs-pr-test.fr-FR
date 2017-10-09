---
title: "le routage dans un classique de réseau virtuel Azure - CLI - aaaControl | Documents Microsoft"
description: "Découvrez comment toocontrol routage dans des réseaux virtuels à l’aide de hello CLI d’Azure dans le modèle de déploiement classique de hello"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="c722d-103">Routage de contrôle et à l’aide des équipements virtuels (classiques) utilisez hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="c722d-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c722d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c722d-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="c722d-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="c722d-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="c722d-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="c722d-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="c722d-107">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="c722d-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="c722d-108">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="c722d-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="c722d-109">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="c722d-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="c722d-110">Vous pouvez également [contrôler le routage et d’utiliser des équipements virtuels dans le modèle de déploiement du Gestionnaire de ressources hello](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c722d-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="c722d-111">commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="c722d-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="c722d-112">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, créer l’environnement hello [créer un réseau virtuel (classiques) à l’aide de hello CLI d’Azure](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c722d-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="c722d-113">Créer hello UDR pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="c722d-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="c722d-114">table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c722d-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="c722d-115">Exécutez hello suivant le mode de commande tooswitch tooclassic :</span><span class="sxs-lookup"><span data-stu-id="c722d-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="c722d-116">Output:</span><span class="sxs-lookup"><span data-stu-id="c722d-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="c722d-117">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau frontal de hello :</span><span class="sxs-lookup"><span data-stu-id="c722d-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="c722d-118">Output:</span><span class="sxs-lookup"><span data-stu-id="c722d-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="c722d-119">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="c722d-119">Parameters:</span></span>
   
   * <span data-ttu-id="c722d-120">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-120">**-l (or --location)**.</span></span> <span data-ttu-id="c722d-121">Région Azure où hello nouveau groupe de sécurité réseau doit être créé.</span><span class="sxs-lookup"><span data-stu-id="c722d-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="c722d-122">Pour notre scénario, *westus*.</span><span class="sxs-lookup"><span data-stu-id="c722d-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="c722d-123">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-123">**-n (or --name)**.</span></span> <span data-ttu-id="c722d-124">Nom de hello nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c722d-124">Name for hello new NSG.</span></span> <span data-ttu-id="c722d-125">Pour notre scénario, *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="c722d-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="c722d-126">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="c722d-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="c722d-127">Output:</span><span class="sxs-lookup"><span data-stu-id="c722d-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="c722d-128">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="c722d-128">Parameters:</span></span>
   
   * <span data-ttu-id="c722d-129">**-r (ou --route-table-name)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="c722d-130">Nom de la table d’itinéraires hello où itinéraire de hello sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="c722d-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="c722d-131">Pour notre scénario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="c722d-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="c722d-132">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="c722d-133">Préfixe d’adresse de sous-réseau hello où les paquets sont destinés à.</span><span class="sxs-lookup"><span data-stu-id="c722d-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="c722d-134">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="c722d-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="c722d-135">**-t (ou --next-hop-type)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="c722d-136">Type d'objet vers lequel le trafic sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="c722d-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="c722d-137">Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="c722d-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="c722d-138">**-p (ou --next-hop-ip-address**).</span><span class="sxs-lookup"><span data-stu-id="c722d-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="c722d-139">Adresse IP de saut suivant.</span><span class="sxs-lookup"><span data-stu-id="c722d-139">IP address for next hop.</span></span> <span data-ttu-id="c722d-140">Pour notre scénario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="c722d-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="c722d-141">Suivante d’exécution hello commande table d’itinéraires hello tooassociate créé par hello **frontal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="c722d-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="c722d-142">Output:</span><span class="sxs-lookup"><span data-stu-id="c722d-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="c722d-143">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="c722d-143">Parameters:</span></span>
   
   * <span data-ttu-id="c722d-144">**-t (ou --vnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="c722d-145">Nom de réseau virtuel où se trouve le sous-réseau de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="c722d-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="c722d-146">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="c722d-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="c722d-147">**-n (ou --subnet-name)**.</span><span class="sxs-lookup"><span data-stu-id="c722d-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="c722d-148">Nom de table d’itinéraires hello hello sous-réseau sera ajouté à.</span><span class="sxs-lookup"><span data-stu-id="c722d-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="c722d-149">Pour notre scénario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="c722d-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="c722d-150">Créer hello UDR pour le sous-réseau principal de hello</span><span class="sxs-lookup"><span data-stu-id="c722d-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="c722d-151">table d’itinéraires toocreate hello et itinéraire nécessaires pour le sous-réseau principal de hello selon le scénario hello, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="c722d-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="c722d-152">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :</span><span class="sxs-lookup"><span data-stu-id="c722d-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="c722d-153">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="c722d-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="c722d-154">Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="c722d-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

