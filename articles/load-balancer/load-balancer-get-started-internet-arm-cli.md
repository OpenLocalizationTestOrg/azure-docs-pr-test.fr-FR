---
title: "aaaCreate une côté Internet l’équilibrage de charge - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate un équilibrage de charge exposés à Internet à l’aide du Gestionnaire de ressources hello CLI d’Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a><span data-ttu-id="f06ab-103">Création d’un équilibrage de charge d’internet à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="f06ab-103">Creating an internet load balancer using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f06ab-104">Portail</span><span class="sxs-lookup"><span data-stu-id="f06ab-104">Portal</span></span>](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [<span data-ttu-id="f06ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f06ab-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [<span data-ttu-id="f06ab-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="f06ab-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [<span data-ttu-id="f06ab-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="f06ab-107">Template</span></span>](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="f06ab-108">Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="f06ab-109">Vous pouvez également [apprendre comment toocreate une connecté à Internet à l’aide de déploiement classique de l’équilibrage de charge](load-balancer-get-started-internet-classic-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f06ab-109">You can also [Learn how toocreate an Internet facing load balancer using classic deployment](load-balancer-get-started-internet-classic-portal.md)</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a><span data-ttu-id="f06ab-110">Déploiement de solution hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="f06ab-110">Deploying hello solution using hello Azure CLI</span></span>

<span data-ttu-id="f06ab-111">Hello suit montrent comment toocreate une connecté à Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="f06ab-111">hello following steps show how toocreate an Internet facing load balancer using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="f06ab-112">Avec Azure Resource Manager chaque ressource est créé et configuré individuellement, puis mis au point toocreate une ressource.</span><span class="sxs-lookup"><span data-stu-id="f06ab-112">With Azure Resource Manager each resource is created and configured individually, then put together toocreate a resource.</span></span>

<span data-ttu-id="f06ab-113">Vous devez créer et configurer hello suivant objets toodeploy un équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="f06ab-113">You must create and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="f06ab-114">Configuration d’adresses IP frontales : contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="f06ab-114">Front-end IP configuration - contains public IP addresses for incoming network traffic.</span></span>
* <span data-ttu-id="f06ab-115">Pool d’adresses principal - contient des interfaces réseau (NIC) pour le trafic réseau tooreceive de hello machines virtuelles à partir de l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-115">Back-end address pool - contains network interfaces (NICs) for hello virtual machines tooreceive network traffic from hello load balancer.</span></span>
* <span data-ttu-id="f06ab-116">Règles d’équilibrage de charge - contient des règles de mappage d’un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-116">Load balancing rules - contains rules mapping a public port on hello load balancer tooport in hello back-end address pool.</span></span>
* <span data-ttu-id="f06ab-117">Les règles NAT de trafic entrant - contient des règles de mappage d’un port public sur le port de tooa d’équilibrage de charge hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-117">Inbound NAT rules - contains rules mapping a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool.</span></span>
* <span data-ttu-id="f06ab-118">Sondes - contient la disponibilité de toocheck les sondes utilisées de contrôle d’intégrité des instances de machines virtuelles dans un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-118">Probes - contains health probes used toocheck availability of virtual machines instances in hello back-end address pool.</span></span>

<span data-ttu-id="f06ab-119">Pour plus d’informations, consultez [Prise en charge d’un équilibrage de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f06ab-119">For more information see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="f06ab-120">Configurer CLI toouse Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="f06ab-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="f06ab-121">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="f06ab-121">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="f06ab-122">Exécutez hello **configuration azure mode** mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f06ab-122">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>

    ```azurecli
        azure config mode arm
    ```

    <span data-ttu-id="f06ab-123">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f06ab-123">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a><span data-ttu-id="f06ab-124">Créer un réseau virtuel et une adresse IP publique hello frontal pool d’adresses IP</span><span class="sxs-lookup"><span data-stu-id="f06ab-124">Create a virtual network and a public IP address for hello front-end IP pool</span></span>

1. <span data-ttu-id="f06ab-125">Créer un réseau virtuel (VNet) nommé *NRPVnet* dans l’emplacement d’États-Unis hello à l’aide d’un groupe de ressources nommé *NRPRG*.</span><span class="sxs-lookup"><span data-stu-id="f06ab-125">Create a virtual network (VNet) named *NRPVnet* in hello East US location using a resource group named *NRPRG*.</span></span>

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    <span data-ttu-id="f06ab-126">Créez un sous-réseau nommé *NRPVnetSubnet* avec un bloc CIDR 10.0.0.0/24 dans *NRPVnet*.</span><span class="sxs-lookup"><span data-stu-id="f06ab-126">Create a subnet named *NRPVnetSubnet* with a CIDR block of 10.0.0.0/24 in *NRPVnet*.</span></span>

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. <span data-ttu-id="f06ab-127">Créer une adresse IP publique nommée *NRPPublicIP* toobe utilisé par un pool IP frontal portant le nom DNS *loadbalancernrp.eastus.cloudapp.azure.com*. commande hello ci-dessous utilise le type d’allocation statique hello et délai d’inactivité de 4 minutes.</span><span class="sxs-lookup"><span data-stu-id="f06ab-127">Create a public IP address named *NRPPublicIP* toobe used by a front-end IP pool with DNS name *loadbalancernrp.eastus.cloudapp.azure.com*. hello command below uses hello static allocation type and idle timeout of 4 minutes.</span></span>

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="f06ab-128">équilibrage de charge Hello utilisera le nom de domaine hello de l’adresse IP publique hello en tant que son nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="f06ab-128">hello load balancer will use hello domain label of hello public IP as its FQDN.</span></span> <span data-ttu-id="f06ab-129">Cette une modification à partir d’un déploiement classique, ce qui utilise le service de cloud computing hello comme hello d’équilibrage de charge nom de domaine complet (FQDN).</span><span class="sxs-lookup"><span data-stu-id="f06ab-129">This a change from classic deployment, which uses hello cloud service as hello load balancer Fully Qualified Domain Name (FQDN).</span></span>
   > <span data-ttu-id="f06ab-130">Dans cet exemple, hello nom de domaine complet est *loadbalancernrp.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="f06ab-130">In this example, hello FQDN is *loadbalancernrp.eastus.cloudapp.azure.com*.</span></span>

## <a name="create-a-load-balancer"></a><span data-ttu-id="f06ab-131">Créer un équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="f06ab-131">Create a load balancer</span></span>

<span data-ttu-id="f06ab-132">Hello de commande suivant crée un équilibreur de charge nommé *NRPlb* Bonjour *NRPRG* groupe de ressources dans hello *États-Unis* emplacement Azure.</span><span class="sxs-lookup"><span data-stu-id="f06ab-132">hello following command creates a load balancer named *NRPlb* in hello *NRPRG* resource group in hello *East US* Azure location.</span></span>

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a><span data-ttu-id="f06ab-133">Création d’un pool d’adresses IP frontales et d’un pool d’adresses principales</span><span class="sxs-lookup"><span data-stu-id="f06ab-133">Create a front-end IP pool and a backend address pool</span></span>
<span data-ttu-id="f06ab-134">Cet exemple montre comment les toocreate hello IP pool frontal qui reçoit le trafic réseau entrant du hello sur hello l’équilibrage de charge et hello du pool d’adresses IP de serveur principal où pool frontal de hello envoie le trafic à charge équilibrée hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-134">This example demonstrates how toocreate hello front-end IP pool that receives hello incoming network traffic on hello load balancer and hello backend IP pool where hello front-end pool sends hello load balanced network traffic.</span></span>

1. <span data-ttu-id="f06ab-135">Créez un pool IP frontal association d’adresse IP publique hello créé dans l’étape précédente de hello et équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-135">Create a front-end IP pool associating hello public IP created in hello previous step and hello load balancer.</span></span>

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. <span data-ttu-id="f06ab-136">Configurer un pool d’adresses de serveur principal utilisé tooreceive du trafic entrant à partir du pool d’adresses IP frontal hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-136">Set up a back-end address pool used tooreceive incoming traffic from hello front-end IP pool.</span></span>

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a><span data-ttu-id="f06ab-137">Créer des règles LB, des règles NAT et de sonde</span><span class="sxs-lookup"><span data-stu-id="f06ab-137">Create LB rules, NAT rules, and probe</span></span>

<span data-ttu-id="f06ab-138">Cet exemple crée hello éléments suivants.</span><span class="sxs-lookup"><span data-stu-id="f06ab-138">This example creates hello following items.</span></span>

* <span data-ttu-id="f06ab-139">la règle NAT tootranslate tout le trafic entrant sur le port 21 tooport 22<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f06ab-139">a NAT rule tootranslate all incoming traffic on port 21 tooport 22<sup>1</sup></span></span>
* <span data-ttu-id="f06ab-140">la règle NAT tootranslate tout le trafic entrant sur le port 23 tooport 22</span><span class="sxs-lookup"><span data-stu-id="f06ab-140">a NAT rule tootranslate all incoming traffic on port 23 tooport 22</span></span>
* <span data-ttu-id="f06ab-141">un toobalance de règle d’équilibrage de charge tout le trafic entrant sur le port 80 tooport 80 sur hello adresses dans le pool principal d’hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-141">a load balancer rule toobalance all incoming traffic on port 80 tooport 80 on hello addresses in hello back-end pool.</span></span>
* <span data-ttu-id="f06ab-142">un état d’intégrité sonde règle toocheck hello, dans une page nommée *HealthProbe.aspx*.</span><span class="sxs-lookup"><span data-stu-id="f06ab-142">a probe rule toocheck hello health status on a page named *HealthProbe.aspx*.</span></span>

<span data-ttu-id="f06ab-143"><sup>1</sup> les règles NAT sont instance de machine virtuelle spécifique associé tooa derrière un équilibreur de charge hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-143"><sup>1</sup> NAT rules are associated tooa specific virtual machine instance behind hello load balancer.</span></span> <span data-ttu-id="f06ab-144">le trafic réseau de Hello arrivant sur le port 21 est envoyé tooa les ordinateur virtuel spécifique sur le port 22 associé à cette règle NAT.</span><span class="sxs-lookup"><span data-stu-id="f06ab-144">hello network traffic arriving on port 21 is sent tooa specific virtual machine on port 22 associated with this NAT rule.</span></span> <span data-ttu-id="f06ab-145">Vous devez spécifier un protocole (TCP ou UDP) pour une règle NAT.</span><span class="sxs-lookup"><span data-stu-id="f06ab-145">You must specify a protocol (UDP or TCP) for a NAT rule.</span></span> <span data-ttu-id="f06ab-146">Les deux protocoles ne peut pas être assigné toohello même port.</span><span class="sxs-lookup"><span data-stu-id="f06ab-146">Both protocols can't be assigned toohello same port.</span></span>

1. <span data-ttu-id="f06ab-147">Créer des règles NAT hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-147">Create hello NAT rules.</span></span>

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. <span data-ttu-id="f06ab-148">Créez une règle d’équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="f06ab-148">Create a load balancer rule.</span></span>

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. <span data-ttu-id="f06ab-149">Créer une sonde d’intégrité.</span><span class="sxs-lookup"><span data-stu-id="f06ab-149">Create a health probe.</span></span>

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. <span data-ttu-id="f06ab-150">Enregistrer vos paramètres.</span><span class="sxs-lookup"><span data-stu-id="f06ab-150">Check your settings.</span></span>

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    <span data-ttu-id="f06ab-151">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f06ab-151">Expected output:</span></span>

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a><span data-ttu-id="f06ab-152">Créer des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="f06ab-152">Create NICs</span></span>

<span data-ttu-id="f06ab-153">Vous devez toocreate NIC (ou modifier des modèles existants) et les associer à des règles de tooNAT, des règles d’équilibrage de charge et des sondes.</span><span class="sxs-lookup"><span data-stu-id="f06ab-153">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="f06ab-154">Créez une carte réseau nommée *être lb-nic1*et l’associer à hello *rdp1* NAT règle et hello *NRPbackendpool* pool d’adresses du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="f06ab-154">Create a NIC named *lb-nic1-be*, and associate it with hello *rdp1* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    <span data-ttu-id="f06ab-155">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="f06ab-155">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. <span data-ttu-id="f06ab-156">Créez une carte réseau nommée *être lb-nic2*et l’associer à hello *rdp2* NAT règle et hello *NRPbackendpool* pool d’adresses du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="f06ab-156">Create a NIC named *lb-nic2-be*, and associate it with hello *rdp2* NAT rule, and hello *NRPbackendpool* back-end address pool.</span></span>

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. <span data-ttu-id="f06ab-157">Créer un ordinateur virtuel (VM) nommé *web1*et l’associer à hello carte réseau nommée *être lb-nic1*.</span><span class="sxs-lookup"><span data-stu-id="f06ab-157">Create a virtual machine (VM) named *web1*, and associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="f06ab-158">Un compte de stockage appelée *web1nrp* a été créé avant d’exécuter la commande hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f06ab-158">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="f06ab-159">Machines virtuelles dans un toobe de nécessité d’équilibrage de charge dans hello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="f06ab-159">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="f06ab-160">Utilisez `azure availset create` toocreate un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="f06ab-160">Use `azure availset create` toocreate an availability set.</span></span>

    <span data-ttu-id="f06ab-161">sortie de Hello sont similaires toohello suivants :</span><span class="sxs-lookup"><span data-stu-id="f06ab-161">hello output should be similar toohello following:</span></span>

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > <span data-ttu-id="f06ab-162">message d’information de type Hello **il s’agit d’une carte réseau sans adresse IP publique configurée** est attendu dans la mesure où hello NIC créée pour l’équilibrage de charge hello connexion tooInternet à l’aide de l’adresse publique IP hello charge équilibrage.</span><span class="sxs-lookup"><span data-stu-id="f06ab-162">hello informational message **This is a NIC without publicIP configured** is expected since hello NIC created for hello load balancer connecting tooInternet using hello load balancer public IP address.</span></span>

    <span data-ttu-id="f06ab-163">Depuis hello *être lb-nic1* carte réseau est associé à hello *rdp1* de règle NAT, vous pouvez vous connecter trop*web1* utilisant le protocole RDP via le port 3441 sur l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="f06ab-163">Since hello *lb-nic1-be* NIC is associated with hello *rdp1* NAT rule, you can connect too*web1* using RDP through port 3441 on hello load balancer.</span></span>

4. <span data-ttu-id="f06ab-164">Créer un ordinateur virtuel (VM) nommé *web2*et l’associer à hello carte réseau nommée *être lb-nic2*.</span><span class="sxs-lookup"><span data-stu-id="f06ab-164">Create a virtual machine (VM) named *web2*, and associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="f06ab-165">Un compte de stockage appelée *web1nrp* a été créé avant d’exécuter la commande hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f06ab-165">A storage account called *web1nrp* was created before running hello command below.</span></span>

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a><span data-ttu-id="f06ab-166">Mettre à jour un équilibreur de charge existant</span><span class="sxs-lookup"><span data-stu-id="f06ab-166">Update an existing load balancer</span></span>
<span data-ttu-id="f06ab-167">Vous pouvez ajouter des règles faisant référence à l’équilibrage de charge existant.</span><span class="sxs-lookup"><span data-stu-id="f06ab-167">You can add rules referencing an existing load balancer.</span></span> <span data-ttu-id="f06ab-168">Dans l’exemple suivant de hello, une nouvelle règle d’équilibreur de charge est ajoutée à équilibrage de charge existant tooan **NRPlb**</span><span class="sxs-lookup"><span data-stu-id="f06ab-168">In hello next example, a new load balancer rule is added tooan existing load balancer **NRPlb**</span></span>

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="f06ab-169">Suppression d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="f06ab-169">Delete a load balancer</span></span>
<span data-ttu-id="f06ab-170">Utilisez hello suivant commande tooremove un équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="f06ab-170">Use hello following command tooremove a load balancer:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a><span data-ttu-id="f06ab-171">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f06ab-171">Next steps</span></span>
[<span data-ttu-id="f06ab-172">Prise en main de la configuration d’un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="f06ab-172">Get started configuring an internal load balancer</span></span>](load-balancer-get-started-ilb-arm-cli.md)

[<span data-ttu-id="f06ab-173">Configuration d'un mode de distribution d'équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="f06ab-173">Configure a load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="f06ab-174">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="f06ab-174">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)
