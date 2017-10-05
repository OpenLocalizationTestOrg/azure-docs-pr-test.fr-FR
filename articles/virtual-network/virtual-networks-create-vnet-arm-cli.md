---
title: "Création d’un réseau virtuel - Azure CLI 2.0 | Microsoft Docs"
description: "Découvrez comment créer un réseau virtuel à l’aide de l’interface Azure CLI 2.0."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="0a6a5-103">Créer un réseau virtuel à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="0a6a5-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="0a6a5-104">Azure propose deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="0a6a5-105">Microsoft recommande la création de ressources via le modèle de déploiement Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="0a6a5-106">Pour en savoir plus sur les différences entre deux modèles, lisez l’article [Comprendre les modèles de déploiement Azure](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0a6a5-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="0a6a5-107">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="0a6a5-107">CLI versions to complete the task</span></span>
<span data-ttu-id="0a6a5-108">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="0a6a5-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager</span><span class="sxs-lookup"><span data-stu-id="0a6a5-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="0a6a5-110">[Azure CLI 2.0 ](#create-a-virtual-network) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="0a6a5-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="0a6a5-111">Vous pouvez également créer un réseau virtuel via Resource Manager à l’aide d’autres outils ou créer un réseau virtuel via le modèle de déploiement classique en sélectionnant une option différente dans la liste suivante :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0a6a5-112">Portail</span><span class="sxs-lookup"><span data-stu-id="0a6a5-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="0a6a5-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a6a5-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="0a6a5-114">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="0a6a5-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="0a6a5-115">Modèle</span><span class="sxs-lookup"><span data-stu-id="0a6a5-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="0a6a5-116">Portail (classique)</span><span class="sxs-lookup"><span data-stu-id="0a6a5-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="0a6a5-117">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="0a6a5-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="0a6a5-118">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="0a6a5-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="0a6a5-119">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="0a6a5-119">Create a virtual network</span></span>

<span data-ttu-id="0a6a5-120">Pour créer un réseau virtuel à l’aide d’Azure CLI 2.0, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="0a6a5-121">Installez et configurez la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à un compte Azure avec la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0a6a5-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="0a6a5-122">Créez un groupe de ressources pour votre réseau virtuel à l’aide de commande [az group create](/cli/azure/group#create) avec les arguments `--name` et `--location` :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="0a6a5-123">Créez un réseau virtuel et un sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="0a6a5-124">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="0a6a5-125">Paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-125">Parameters used:</span></span>

    - <span data-ttu-id="0a6a5-126">`--name TestVNet` : Nom du réseau virtuel à créer.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="0a6a5-127">`--resource-group TestRG` : # Nom du groupe de ressources qui contrôle la ressource.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="0a6a5-128">`--location centralus` : l’emplacement vers lequel effectuer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="0a6a5-129">`--address-prefix 192.168.0.0/16` : préfixe et bloc d’adresse source.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="0a6a5-130">`--subnet-name FrontEnd` : nom du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="0a6a5-131">`--subnet-prefix 192.168.1.0/24` : préfixe et bloc d’adresse source.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="0a6a5-132">Pour répertorier les informations de base à utiliser dans la commande suivante, vous pouvez interroger le réseau virtuel à l’aide un [filtre de requête](/cli/azure/query-az-cli2) :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="0a6a5-133">Ce qui génère la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="0a6a5-134">Créez un sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="0a6a5-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="0a6a5-136">Paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-136">Parameters used:</span></span>

    - <span data-ttu-id="0a6a5-137">`--address-prefix 192.168.2.0/24` : bloc CIDR de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="0a6a5-138">`--name BackEnd` : nom du nouveau sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="0a6a5-139">`--resource-group TestRG` : le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="0a6a5-140">`--vnet-name TestVNet` : le nom du réseau virtuel propriétaire.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="0a6a5-141">Interrogez les propriétés du nouveau réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="0a6a5-142">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="0a6a5-143">Interrogez les propriétés des sous-réseaux :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="0a6a5-144">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="0a6a5-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0a6a5-145">Next steps</span></span>

<span data-ttu-id="0a6a5-146">Apprenez à connecter :</span><span class="sxs-lookup"><span data-stu-id="0a6a5-146">Learn how to connect:</span></span>

- <span data-ttu-id="0a6a5-147">Une machine virtuelle à un réseau virtuel en lisant l’article [Création d’une machine virtuelle Linux](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0a6a5-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="0a6a5-148">Au lieu de créer un réseau virtuel et un sous-réseau comme indiqué dans les procédures de ces articles, vous pouvez sélectionner un réseau virtuel et un sous-réseau existants pour établir la connexion à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="0a6a5-149">Le réseau virtuel à d’autres réseaux virtuels en lisant l’article sur la [connexion des réseaux virtuels](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a6a5-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="0a6a5-150">Le réseau virtuel à un réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou d’un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="0a6a5-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="0a6a5-151">Découvrez comment en lisant [Connecter un réseau virtuel à un réseau local à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [Lier un réseau virtuel à un circuit ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0a6a5-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>