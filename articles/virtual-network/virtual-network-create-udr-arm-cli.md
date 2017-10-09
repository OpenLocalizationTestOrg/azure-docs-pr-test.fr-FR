---
title: "aaaControl équipements virtuels et de routage à l’aide de hello Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment toocontrol équipements virtuels et de routage à l’aide de hello Azure CLI 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="4011a-103">Créer des itinéraires définis par l’utilisateur (UDR) à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4011a-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4011a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4011a-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="4011a-105">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="4011a-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="4011a-106">Modèle</span><span class="sxs-lookup"><span data-stu-id="4011a-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="4011a-107">PowerShell (déploiement Classic)</span><span class="sxs-lookup"><span data-stu-id="4011a-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="4011a-108">CLI (déploiement Classic)</span><span class="sxs-lookup"><span data-stu-id="4011a-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="4011a-109">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="4011a-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="4011a-110">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="4011a-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="4011a-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="4011a-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="4011a-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)</span><span class="sxs-lookup"><span data-stu-id="4011a-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="4011a-113">commandes de CLI d’Azure Hello exemple ci-dessous s’attendre à un environnement simple déjà créé en fonction de scénario hello ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4011a-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="4011a-114">Si vous souhaitez que les commandes de hello toorun car elles sont affichées dans ce document, tout d’abord créer des environnement de test hello en déployant [ce modèle](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello Si nécessaire et suivez les instructions hello dans hello portal.</span><span class="sxs-lookup"><span data-stu-id="4011a-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="4011a-115">Créer hello UDR pour le sous-réseau frontal de hello</span><span class="sxs-lookup"><span data-stu-id="4011a-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="4011a-116">table d’itinéraires toocreate hello et d’itinéraire nécessaire pour le sous-réseau frontal de hello selon le scénario de hello ci-dessus, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4011a-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="4011a-117">Créer une table d’itinéraires pour le sous-réseau frontal de hello avec hello [créer de table de routage de réseau az](/cli/azure/network/route-table#create) commande :</span><span class="sxs-lookup"><span data-stu-id="4011a-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="4011a-118">Output:</span><span class="sxs-lookup"><span data-stu-id="4011a-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="4011a-119">Créez un itinéraire qui envoie tout le trafic destiné toohello le sous-réseau principal (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) à l’aide de hello [itinéraire de table d’itinéraires réseau az créer](/cli/azure/network/route-table/route#create) commande :</span><span class="sxs-lookup"><span data-stu-id="4011a-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="4011a-120">Output:</span><span class="sxs-lookup"><span data-stu-id="4011a-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="4011a-121">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="4011a-121">Parameters:</span></span>

    * <span data-ttu-id="4011a-122">**--route-table-name**.</span><span class="sxs-lookup"><span data-stu-id="4011a-122">**--route-table-name**.</span></span> <span data-ttu-id="4011a-123">Nom de la table d’itinéraires hello où itinéraire de hello sera ajouté.</span><span class="sxs-lookup"><span data-stu-id="4011a-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="4011a-124">Pour notre scénario, *UDR-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="4011a-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="4011a-125">**--address-prefix**.</span><span class="sxs-lookup"><span data-stu-id="4011a-125">**--address-prefix**.</span></span> <span data-ttu-id="4011a-126">Préfixe d’adresse de sous-réseau hello où les paquets sont destinés à.</span><span class="sxs-lookup"><span data-stu-id="4011a-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="4011a-127">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="4011a-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="4011a-128">**--next-hop-type**.</span><span class="sxs-lookup"><span data-stu-id="4011a-128">**--next-hop-type**.</span></span> <span data-ttu-id="4011a-129">Type d'objet vers lequel le trafic sera envoyé.</span><span class="sxs-lookup"><span data-stu-id="4011a-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="4011a-130">Les valeurs possibles sont *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet* ou *None*.</span><span class="sxs-lookup"><span data-stu-id="4011a-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="4011a-131">**--next-hop-ip-address**.</span><span class="sxs-lookup"><span data-stu-id="4011a-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="4011a-132">Adresse IP de saut suivant.</span><span class="sxs-lookup"><span data-stu-id="4011a-132">IP address for next hop.</span></span> <span data-ttu-id="4011a-133">Pour notre scénario, *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="4011a-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="4011a-134">Exécutez hello [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update) table d’itinéraires commande tooassociate hello créé ci-dessus hello **frontal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="4011a-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="4011a-135">Output:</span><span class="sxs-lookup"><span data-stu-id="4011a-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="4011a-136">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="4011a-136">Parameters:</span></span>
    
    * <span data-ttu-id="4011a-137">**--vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="4011a-137">**--vnet-name**.</span></span> <span data-ttu-id="4011a-138">Nom de réseau virtuel où se trouve le sous-réseau de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="4011a-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="4011a-139">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="4011a-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="4011a-140">Créer hello UDR pour le sous-réseau principal de hello</span><span class="sxs-lookup"><span data-stu-id="4011a-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="4011a-141">toocreate hello table d’itinéraires et Router nécessaires pour le sous-réseau principal de hello selon le scénario hello ci-dessus, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="4011a-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="4011a-142">Exécutez hello suivant commande toocreate une table d’itinéraires pour le sous-réseau principal de hello :</span><span class="sxs-lookup"><span data-stu-id="4011a-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="4011a-143">Exécutez hello suivant commande toocreate un itinéraire dans hello itinéraire table toosend tout le trafic destiné toohello sous-réseau frontal (192.168.1.0/24) toohello **FW1** VM (192.168.0.4) :</span><span class="sxs-lookup"><span data-stu-id="4011a-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="4011a-144">Exécution hello suivant tooassociate commande hello une table d’itinéraires par hello **principal** sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="4011a-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="4011a-145">Activer le transfert IP sur FW1</span><span class="sxs-lookup"><span data-stu-id="4011a-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="4011a-146">le transfert IP tooenable Bonjour carte réseau utilisée par **FW1**complète hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4011a-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="4011a-147">Exécutez hello [az réseau nic afficher](/cli/azure/network/nic#show) avec un Bonjour de toodisplay JMESPATH filtre actuel **-ip-activer le transfert** valeur **transfert activer une IP**.</span><span class="sxs-lookup"><span data-stu-id="4011a-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="4011a-148">Il doit être défini trop*false*.</span><span class="sxs-lookup"><span data-stu-id="4011a-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="4011a-149">Output:</span><span class="sxs-lookup"><span data-stu-id="4011a-149">Output:</span></span>

        false

2. <span data-ttu-id="4011a-150">Exécutez hello après le transfert IP commande tooenable :</span><span class="sxs-lookup"><span data-stu-id="4011a-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="4011a-151">Vous pouvez examiner la console de toohello en flux continu de sortie hello ou simplement retester pour hello spécifique **enableIpForwarding** valeur :</span><span class="sxs-lookup"><span data-stu-id="4011a-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="4011a-152">Output:</span><span class="sxs-lookup"><span data-stu-id="4011a-152">Output:</span></span>

        true

    <span data-ttu-id="4011a-153">Paramètres :</span><span class="sxs-lookup"><span data-stu-id="4011a-153">Parameters:</span></span>

    <span data-ttu-id="4011a-154">**--ip-forwarding** : *true* ou *false*.</span><span class="sxs-lookup"><span data-stu-id="4011a-154">**--ip-forwarding**: *true* or *false*.</span></span>

