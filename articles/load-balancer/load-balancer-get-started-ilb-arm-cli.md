---
title: "aaaCreate un interne l’équilibrage de charge - CLI d’Azure | Documents Microsoft"
description: "Découvrez comment toocreate un équilibreur de charge interne à l’aide de hello CLI d’Azure dans le Gestionnaire de ressources"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a><span data-ttu-id="965d9-103">Créer un équilibreur de charge interne à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="965d9-103">Create an internal load balancer by using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="965d9-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="965d9-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="965d9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="965d9-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="965d9-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="965d9-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="965d9-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="965d9-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="965d9-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="965d9-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="965d9-109">Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="965d9-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a><span data-ttu-id="965d9-110">Déployer des solutions de hello à l’aide de hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="965d9-110">Deploy hello solution by using hello Azure CLI</span></span>

<span data-ttu-id="965d9-111">Hello suit montrent comment toocreate une côté Internet l’équilibrage de charge à l’aide du Gestionnaire de ressources Azure avec l’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="965d9-111">hello following steps show how toocreate an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="965d9-112">Avec Azure Resource Manager, chaque ressource est créé et configuré individuellement et puis rassembler toocreate une ressource.</span><span class="sxs-lookup"><span data-stu-id="965d9-112">With Azure Resource Manager, each resource is created and configured individually, and then put together toocreate a resource.</span></span>

<span data-ttu-id="965d9-113">Vous devez toocreate et que vous configurez hello suivant objets toodeploy un équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="965d9-113">You need toocreate and configure hello following objects toodeploy a load balancer:</span></span>

* <span data-ttu-id="965d9-114">**Configuration d’adresses IP frontales**: contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="965d9-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="965d9-115">**Pool d’adresses de serveur principal**: contient des interfaces réseau (NIC) qui autorisent le trafic réseau tooreceive du hello machines virtuelles à partir de l’équilibrage de charge hello</span><span class="sxs-lookup"><span data-stu-id="965d9-115">**Back-end address pool**: contains network interfaces (NICs) that enable hello virtual machines tooreceive network traffic from hello load balancer</span></span>
* <span data-ttu-id="965d9-116">**Règles d’équilibrage de charge**: contient des règles pour mappent un port public sur tooport d’équilibrage de charge hello dans un pool d’adresses de serveur principal hello</span><span class="sxs-lookup"><span data-stu-id="965d9-116">**Load-balancing rules**: contains rules that map a public port on hello load balancer tooport in hello back-end address pool</span></span>
* <span data-ttu-id="965d9-117">**Les règles NAT de trafic entrant**: contient des règles pour mappent un port public sur le port de tooa d’équilibrage de charge de hello pour un ordinateur virtuel spécifique dans le pool d’adresses principal hello</span><span class="sxs-lookup"><span data-stu-id="965d9-117">**Inbound NAT rules**: contains rules that map a public port on hello load balancer tooa port for a specific virtual machine in hello back-end address pool</span></span>
* <span data-ttu-id="965d9-118">**Sondes**: contient les sondes d’intégrité qui sont la disponibilité de hello toocheck utilisé d’instances de machines virtuelles dans un pool d’adresses de serveur principal hello</span><span class="sxs-lookup"><span data-stu-id="965d9-118">**Probes**: contains health probes that are used toocheck hello availability of virtual machines instances in hello back-end address pool</span></span>

<span data-ttu-id="965d9-119">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="965d9-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-toouse-resource-manager"></a><span data-ttu-id="965d9-120">Configurer CLI toouse Gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="965d9-120">Set up CLI toouse Resource Manager</span></span>

1. <span data-ttu-id="965d9-121">Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="965d9-121">If you have never used Azure CLI, see [Install and configure hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="965d9-122">Suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.</span><span class="sxs-lookup"><span data-stu-id="965d9-122">Follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="965d9-123">Exécutez hello **mode config azure** commande tooswitch tooResource Manager mode, comme suit :</span><span class="sxs-lookup"><span data-stu-id="965d9-123">Run hello **azure config mode** command tooswitch tooResource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="965d9-124">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="965d9-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="965d9-125">Créer un équilibrage de charge interne, étape par étape</span><span class="sxs-lookup"><span data-stu-id="965d9-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="965d9-126">Connectez-vous tooAzure.</span><span class="sxs-lookup"><span data-stu-id="965d9-126">Sign in tooAzure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="965d9-127">À l’invite, entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="965d9-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="965d9-128">Modifier le mode Gestionnaire de ressources tooAzure hello commande Outils.</span><span class="sxs-lookup"><span data-stu-id="965d9-128">Change hello command tools tooAzure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="965d9-129">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="965d9-129">Create a resource group</span></span>

<span data-ttu-id="965d9-130">Toutes les ressources d’Azure Resource Manager sont associées à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="965d9-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="965d9-131">Le cas échéant, créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="965d9-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="965d9-132">Créer un jeu d’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="965d9-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="965d9-133">Créer un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="965d9-133">Create an internal load balancer</span></span>

    <span data-ttu-id="965d9-134">Bonjour scénario, un groupe de ressources nommé nrprg est créé dans la région est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="965d9-134">In hello following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="965d9-135">Toutes les ressources pour un équilibrage de charge interne, tels que les réseaux virtuels et des sous-réseaux du réseau virtuel, doivent être dans hello du même groupe de ressources et de hello même région.</span><span class="sxs-lookup"><span data-stu-id="965d9-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in hello same resource group and in hello same region.</span></span>

2. <span data-ttu-id="965d9-136">Créer une adresse IP frontale pour l’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="965d9-136">Create a front-end IP address for hello internal load balancer.</span></span>

    <span data-ttu-id="965d9-137">adresse IP Hello que vous utilisez doit être dans la plage de sous-réseau hello de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="965d9-137">hello IP address that you use must be within hello subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="965d9-138">Créer un pool d’adresses de serveur principal hello.</span><span class="sxs-lookup"><span data-stu-id="965d9-138">Create hello back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="965d9-139">Après avoir défini une adresse IP frontale et un pool d’adresses principales, vous pouvez créer des règles d’équilibrage de charge, des règles NAT entrantes et des sondes d’intégrité personnalisées.</span><span class="sxs-lookup"><span data-stu-id="965d9-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="965d9-140">Créer une règle d’équilibreur de charge pour l’équilibrage de charge interne hello.</span><span class="sxs-lookup"><span data-stu-id="965d9-140">Create a load balancer rule for hello internal load balancer.</span></span>

    <span data-ttu-id="965d9-141">Lorsque vous suivez les étapes précédentes hello, commande hello crée une règle d’équilibrage de charge pour l’écoute tooport 1433 dans le pool frontal de hello et envoi équilibrage de la charge du trafic toohello principal pool d’adresses réseau, via le port 1433.</span><span class="sxs-lookup"><span data-stu-id="965d9-141">When you follow hello previous steps, hello command creates a load-balancer rule for listening tooport 1433 in hello front-end pool and sending load-balanced network traffic toohello back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="965d9-142">Créez des règles NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="965d9-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="965d9-143">Les règles NAT entrantes sont les extrémités de toocreate utilisé dans un équilibreur de charge qui vont l’instance de machine virtuelle spécifique tooa.</span><span class="sxs-lookup"><span data-stu-id="965d9-143">Inbound NAT rules are used toocreate endpoints in a load balancer that go tooa specific virtual machine instance.</span></span> <span data-ttu-id="965d9-144">les étapes précédentes Hello créé deux règles NAT pour le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="965d9-144">hello previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="965d9-145">Créer des sondes d’intégrité pour l’équilibrage de charge hello.</span><span class="sxs-lookup"><span data-stu-id="965d9-145">Create health probes for hello load balancer.</span></span>

    <span data-ttu-id="965d9-146">Une sonde d’intégrité vérifie tous les toomake des instances de machine virtuelle qu’ils peuvent envoyer le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="965d9-146">A health probe checks all virtual machine instances toomake sure they can send network traffic.</span></span> <span data-ttu-id="965d9-147">instance de machine virtuelle Hello avec les vérifications de sonde ayant échoué est supprimé à partir de l’équilibrage de charge hello jusqu'à ce qu’il est en ligne et une vérification de la sonde détermine qu’elle est saine.</span><span class="sxs-lookup"><span data-stu-id="965d9-147">hello virtual machine instance with failed probe checks is removed from hello load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="965d9-148">plateforme de Microsoft Azure Hello utilise une adresse IPv4 statique routable publiquement pour un éventail de scénarios d’administration.</span><span class="sxs-lookup"><span data-stu-id="965d9-148">hello Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="965d9-149">adresse IP de Hello est 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="965d9-149">hello IP address is 168.63.129.16.</span></span> <span data-ttu-id="965d9-150">Cette adresse IP ne doit pas être bloquée par les pare-feu, car cela peut entraîner un comportement inattendu.</span><span class="sxs-lookup"><span data-stu-id="965d9-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="965d9-151">En ce qui concerne tooAzure équilibrage de charge interne, cette adresse IP est utilisée par l’analyse des sondes de l’état d’intégrité de hello charge équilibrage toodetermine hello pour les ordinateurs virtuels dans un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="965d9-151">With respect tooAzure internal load balancing, this IP address is used by monitoring probes from hello load balancer toodetermine hello health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="965d9-152">Si un groupe de sécurité réseau est utilisé toorestrict virtuels trafic tooAzure dans un jeu d’équilibrage de charge en interne ou sous-réseau de réseau virtuel tooa appliqués, vérifiez qu’une règle de sécurité réseau est ajoutée tooallow trafic à partir de 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="965d9-152">If a network security group is used toorestrict traffic tooAzure virtual machines in an internally load-balanced set or is applied tooa virtual network subnet, ensure that a network security rule is added tooallow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="965d9-153">Créer des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="965d9-153">Create NICs</span></span>

<span data-ttu-id="965d9-154">Vous devez toocreate NIC (ou modifier des modèles existants) et les associer à des règles de tooNAT, des règles d’équilibrage de charge et des sondes.</span><span class="sxs-lookup"><span data-stu-id="965d9-154">You need toocreate NICs (or modify existing ones) and associate them tooNAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="965d9-155">Créez une carte réseau nommée *être lb-nic1*et l’associer à hello *rdp1* NAT règle et hello *beilb* pool d’adresses du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="965d9-155">Create an NIC named *lb-nic1-be*, and then associate it with hello *rdp1* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="965d9-156">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="965d9-156">Expected output:</span></span>

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

2. <span data-ttu-id="965d9-157">Créez une carte réseau nommée *être lb-nic2*et l’associer à hello *rdp2* NAT règle et hello *beilb* pool d’adresses du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="965d9-157">Create an NIC named *lb-nic2-be*, and then associate it with hello *rdp2* NAT rule and hello *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="965d9-158">Créer un ordinateur virtuel nommé *DB1*et associez-le ensuite hello carte réseau nommée *être lb-nic1*.</span><span class="sxs-lookup"><span data-stu-id="965d9-158">Create a virtual machine named *DB1*, and then associate it with hello NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="965d9-159">Un compte de stockage appelée *web1nrp* est créé avant hello après l’exécution de la commande :</span><span class="sxs-lookup"><span data-stu-id="965d9-159">A storage account called *web1nrp* is created before hello following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="965d9-160">Machines virtuelles dans un toobe de nécessité d’équilibrage de charge dans hello même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="965d9-160">VMs in a load balancer need toobe in hello same availability set.</span></span> <span data-ttu-id="965d9-161">Utilisez `azure availset create` toocreate un ensemble de disponibilité.</span><span class="sxs-lookup"><span data-stu-id="965d9-161">Use `azure availset create` toocreate an availability set.</span></span>

4. <span data-ttu-id="965d9-162">Créer un ordinateur virtuel (VM) nommé *DB2*et associez-le ensuite hello carte réseau nommée *être lb-nic2*.</span><span class="sxs-lookup"><span data-stu-id="965d9-162">Create a virtual machine (VM) named *DB2*, and then associate it with hello NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="965d9-163">Un compte de stockage appelée *web1nrp* a été créé avant d’exécuter hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="965d9-163">A storage account called *web1nrp* was created before running hello following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="965d9-164">Suppression d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="965d9-164">Delete a load balancer</span></span>

<span data-ttu-id="965d9-165">tooremove un équilibreur de charge, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="965d9-165">tooremove a load balancer, use hello following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="965d9-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="965d9-166">Next steps</span></span>

[<span data-ttu-id="965d9-167">Configurer le mode de distribution d’équilibrage de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="965d9-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="965d9-168">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="965d9-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

