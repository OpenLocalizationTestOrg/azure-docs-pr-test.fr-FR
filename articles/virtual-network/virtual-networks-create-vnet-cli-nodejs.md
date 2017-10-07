---
title: "un réseau virtuel à l’aide d’aaaCreate hello Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment un réseau virtuel à l’aide de toocreate hello Azure CLI 1.0 | Gestionnaire de ressources."
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="6ef65-103">Créer un réseau virtuel à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="6ef65-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="6ef65-104">Azure propose deux modèles de déploiement : Azure Resource Manager et classique.</span><span class="sxs-lookup"><span data-stu-id="6ef65-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6ef65-105">Microsoft recommande de créer des ressources via le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="6ef65-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="6ef65-106">toolearn en savoir plus sur hello différences entre hello deux modèles, lire hello [modèles de déploiement Azure de comprendre](../azure-resource-manager/resource-manager-deployment-model.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ef65-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6ef65-107">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="6ef65-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="6ef65-108">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="6ef65-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="6ef65-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="6ef65-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="6ef65-110">[Azure CLI 1.0](#create-a-virtual-network) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="6ef65-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="6ef65-111">Créez un réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6ef65-111">Create a virtual network</span></span>

<span data-ttu-id="6ef65-112">un réseau virtuel à l’aide de toocreate hello CLI d’Azure, hello complète comme suit :</span><span class="sxs-lookup"><span data-stu-id="6ef65-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="6ef65-113">Installer et configurer hello CLI d’Azure par hello suivant les étapes dans hello [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ef65-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="6ef65-114">Créez un réseau virtuel et un sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="6ef65-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="6ef65-115">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="6ef65-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="6ef65-116">Paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="6ef65-116">Parameters used:</span></span>

   * <span data-ttu-id="6ef65-117">**--vnet**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-117">**--vnet**.</span></span> <span data-ttu-id="6ef65-118">Nom de hello toobe de réseau virtuel créé.</span><span class="sxs-lookup"><span data-stu-id="6ef65-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="6ef65-119">Pour notre scénario, *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="6ef65-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="6ef65-120">**-e (ou --address-space)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="6ef65-121">Espace d'adressage du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6ef65-121">VNet address space.</span></span> <span data-ttu-id="6ef65-122">Pour notre scénario, *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="6ef65-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="6ef65-123">**-i (ou -cidr)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="6ef65-124">Masque de réseau au format CIDR.</span><span class="sxs-lookup"><span data-stu-id="6ef65-124">Network mask in CIDR format.</span></span> <span data-ttu-id="6ef65-125">Pour notre scénario, *16*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="6ef65-126">**-n (ou --subnet-name**).</span><span class="sxs-lookup"><span data-stu-id="6ef65-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="6ef65-127">Nom du sous-réseau de première hello.</span><span class="sxs-lookup"><span data-stu-id="6ef65-127">Name of hello first subnet.</span></span> <span data-ttu-id="6ef65-128">Pour notre scénario, *FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="6ef65-129">**-p (ou --subnet-start-ip)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="6ef65-130">Adresse IP de début pour le sous-réseau, ou espace d'adressage du sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6ef65-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="6ef65-131">Pour notre scénario, *192.168.1.0*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="6ef65-132">**-r (ou --subnet-cidr)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="6ef65-133">Masque de réseau au format CIDR pour le sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6ef65-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="6ef65-134">Pour notre scénario, *24*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="6ef65-135">**-l (ou --location)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-135">**-l (or --location)**.</span></span> <span data-ttu-id="6ef65-136">Région Azure où hello réseau virtuel est créé.</span><span class="sxs-lookup"><span data-stu-id="6ef65-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="6ef65-137">Pour notre scénario, *Centre des États-Unis*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="6ef65-138">Créez un sous-réseau :</span><span class="sxs-lookup"><span data-stu-id="6ef65-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="6ef65-139">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="6ef65-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="6ef65-140">Paramètres utilisés :</span><span class="sxs-lookup"><span data-stu-id="6ef65-140">Parameters used:</span></span>

   * <span data-ttu-id="6ef65-141">**-t (ou --vnet-name**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="6ef65-142">Nom de hello réseau virtuel où le sous-réseau de hello doit être créé.</span><span class="sxs-lookup"><span data-stu-id="6ef65-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="6ef65-143">Pour notre scénario, *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="6ef65-144">**-n (ou --name)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-144">**-n (or --name)**.</span></span> <span data-ttu-id="6ef65-145">Nom du sous-réseau hello.</span><span class="sxs-lookup"><span data-stu-id="6ef65-145">Name of hello new subnet.</span></span> <span data-ttu-id="6ef65-146">Pour notre scénario, *BackEnd*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="6ef65-147">**-a (ou --address-prefix)**.</span><span class="sxs-lookup"><span data-stu-id="6ef65-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="6ef65-148">Bloc CIDR de sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="6ef65-148">Subnet CIDR block.</span></span> <span data-ttu-id="6ef65-149">Pour notre scénario, *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="6ef65-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="6ef65-150">propriétés de hello tooview de hello nouveau réseau virtuel :</span><span class="sxs-lookup"><span data-stu-id="6ef65-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="6ef65-151">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="6ef65-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="6ef65-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6ef65-152">Next steps</span></span>

<span data-ttu-id="6ef65-153">Découvrez comment tooconnect :</span><span class="sxs-lookup"><span data-stu-id="6ef65-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="6ef65-154">Un réseau virtuel tooa de machine virtuelle (VM) en lisant hello [créer un VM Linux](../virtual-machines/linux/quick-create-cli.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ef65-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="6ef65-155">Au lieu de créer un réseau virtuel et un sous-réseau dans les étapes de hello d’articles de hello, vous pouvez sélectionner un réseau virtuel existant et le sous-réseau tooconnect une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6ef65-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="6ef65-156">Hello des réseaux virtuels tooother de réseau virtuel en lisant hello [connecter des réseaux virtuels](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="6ef65-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="6ef65-157">Hello réseau virtuel tooan réseau local à l’aide d’un réseau privé virtuel (VPN) site à site ou un circuit ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="6ef65-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="6ef65-158">Découvrez comment en lecture hello [connecter un réseau local de tooan de réseau virtuel à l’aide d’un VPN de site à site](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) et [lier un circuit ExpressRoute de tooan réseau virtuel](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="6ef65-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
