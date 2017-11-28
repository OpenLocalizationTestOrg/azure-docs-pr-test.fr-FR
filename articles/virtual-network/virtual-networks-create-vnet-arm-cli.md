---
title: "aaaCreate un réseau virtuel - Azure CLI 2.0 | Documents Microsoft"
description: "Découvrez comment un réseau virtuel à l’aide de toocreate hello Azure CLI 2.0."
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
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="f82ff-103">Créer un réseau virtuel à l’aide de hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f82ff-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="f82ff-104">Azure propose deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="f82ff-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="f82ff-105">Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f82ff-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="f82ff-106">toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f82ff-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f82ff-107">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="f82ff-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="f82ff-108">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="f82ff-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="f82ff-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – notre CLI pour les modèles de déploiement gestion classique et les ressources des hello</span><span class="sxs-lookup"><span data-stu-id="f82ff-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="f82ff-110">[Azure CLI 2.0](#create-a-virtual-network) -notre prochaine génération CLI pour le modèle de déploiement de gestion hello de ressource (cet article)'</span><span class="sxs-lookup"><span data-stu-id="f82ff-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="f82ff-111">Vous pouvez également créer un réseau virtuel via le Gestionnaire de ressources à l’aide d’autres outils ou créer un réseau virtuel via le modèle de déploiement classique hello en sélectionnant une option différente de hello suivant liste :</span><span class="sxs-lookup"><span data-stu-id="f82ff-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f82ff-112">Portail</span><span class="sxs-lookup"><span data-stu-id="f82ff-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="f82ff-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f82ff-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="f82ff-114">INTERFACE DE LIGNE DE COMMANDE</span><span class="sxs-lookup"><span data-stu-id="f82ff-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="f82ff-115">Modèle</span><span class="sxs-lookup"><span data-stu-id="f82ff-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="f82ff-116">Portail (classique)</span><span class="sxs-lookup"><span data-stu-id="f82ff-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="f82ff-117">PowerShell (classique)</span><span class="sxs-lookup"><span data-stu-id="f82ff-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="f82ff-118">Interface de ligne de commande (classique)</span><span class="sxs-lookup"><span data-stu-id="f82ff-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="f82ff-119">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="f82ff-119">Create a virtual network</span></span>

<span data-ttu-id="f82ff-120">un réseau virtuel à l’aide de toocreate hello Azure CLI 2.0, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="f82ff-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="f82ff-121">Installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="f82ff-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="f82ff-122">Créer un groupe de ressources pour votre réseau virtuel à l’aide de hello [création de groupe de az](/cli/azure/group#create) avec hello `--name` et `--location` arguments :</span><span class="sxs-lookup"><span data-stu-id="f82ff-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="f82ff-123">Créez un réseau virtuel et un sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="f82ff-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="f82ff-124">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f82ff-124">Expected output:</span></span>
    
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

    <span data-ttu-id="f82ff-125">Paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="f82ff-125">Parameters used:</span></span>

    - <span data-ttu-id="f82ff-126">`--name TestVNet`: Nom de hello toobe de réseau virtuel créé.</span><span class="sxs-lookup"><span data-stu-id="f82ff-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="f82ff-127">`--resource-group TestRG`: # hello nom groupe de ressources qui contrôle les ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f82ff-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="f82ff-128">`--location centralus`: hello emplacement dans le toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f82ff-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="f82ff-129">`--address-prefix 192.168.0.0/16`: hello préfixe d’adresse et de bloc.</span><span class="sxs-lookup"><span data-stu-id="f82ff-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="f82ff-130">`--subnet-name FrontEnd`: nom hello du sous-réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="f82ff-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="f82ff-131">`--subnet-prefix 192.168.1.0/24`: hello préfixe d’adresse et de bloc.</span><span class="sxs-lookup"><span data-stu-id="f82ff-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="f82ff-132">toolist hello des informations de base toouse Bonjour suivant de commande, vous pouvez interroger à l’aide du réseau virtuel hello un [filtre de requête](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="f82ff-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="f82ff-133">Ce qui donne hello suivant de sortie :</span><span class="sxs-lookup"><span data-stu-id="f82ff-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="f82ff-134">Créez un sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="f82ff-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="f82ff-135">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f82ff-135">Expected output:</span></span>

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

    <span data-ttu-id="f82ff-136">Paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="f82ff-136">Parameters used:</span></span>

    - <span data-ttu-id="f82ff-137">`--address-prefix 192.168.2.0/24` : bloc CIDR de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f82ff-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="f82ff-138">`--name BackEnd`: Nom de sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="f82ff-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="f82ff-139">`--resource-group TestRG`: groupe de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f82ff-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="f82ff-140">`--vnet-name TestVNet`: nom hello Hello propriétaire du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="f82ff-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="f82ff-141">Propriétés de la requête hello de hello nouveau réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="f82ff-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="f82ff-142">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f82ff-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="f82ff-143">Interroger les propriétés de hello de sous-réseaux de hello :</span><span class="sxs-lookup"><span data-stu-id="f82ff-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="f82ff-144">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f82ff-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="f82ff-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f82ff-145">Next steps</span></span>

<span data-ttu-id="f82ff-146">Découvrez comment tooconnect :</span><span class="sxs-lookup"><span data-stu-id="f82ff-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="f82ff-147">Un réseau virtuel tooa de machine virtuelle (VM) en lisant hello [créer un VM Linux](../virtual-machines/linux/quick-create-cli.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f82ff-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="f82ff-148">Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f82ff-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="f82ff-149">Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="f82ff-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="f82ff-150">Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="f82ff-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="f82ff-151">Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f82ff-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
