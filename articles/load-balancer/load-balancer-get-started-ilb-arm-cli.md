---
title: "Créer un équilibrage de charge interne à l’aide de la CLI Azure | Microsoft Docs"
description: "Découvrez comment créer un équilibrage de charge interne dans Resource Manager à l’aide de l’interface de ligne de commande Azure"
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
ms.openlocfilehash: 128b91c685b5f7e494a69ca5b04165a0ee7cbb78
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-internal-load-balancer-by-using-the-azure-cli"></a><span data-ttu-id="8509c-103">Créer un équilibreur de charge interne à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8509c-103">Create an internal load balancer by using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8509c-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8509c-104">Azure Portal</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [<span data-ttu-id="8509c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8509c-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [<span data-ttu-id="8509c-106">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8509c-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [<span data-ttu-id="8509c-107">Modèle</span><span class="sxs-lookup"><span data-stu-id="8509c-107">Template</span></span>](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8509c-108">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8509c-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="8509c-109">Cet article traite de l’utilisation du modèle de déploiement Resource Manager que Microsoft recommande pour la plupart des nouveaux déploiements à la place du [modèle de déploiement classique](load-balancer-get-started-ilb-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8509c-109">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](load-balancer-get-started-ilb-classic-cli.md).</span></span>

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-the-solution-by-using-the-azure-cli"></a><span data-ttu-id="8509c-110">Déployer la solution à l’aide de l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="8509c-110">Deploy the solution by using the Azure CLI</span></span>

<span data-ttu-id="8509c-111">Les étapes suivantes expliquent comment créer un équilibrage de charge accessible sur Internet à l’aide d’Azure Resource Manager avec l’interface de ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="8509c-111">The following steps show how to create an Internet-facing load balancer by using Azure Resource Manager with CLI.</span></span> <span data-ttu-id="8509c-112">Avec Azure Resource Manager, toutes les ressources sont créées et configurées individuellement, puis rassemblées pour en créer une unique.</span><span class="sxs-lookup"><span data-stu-id="8509c-112">With Azure Resource Manager, each resource is created and configured individually, and then put together to create a resource.</span></span>

<span data-ttu-id="8509c-113">Vous devez créer et configurer les objets suivants pour déployer un équilibreur de charge :</span><span class="sxs-lookup"><span data-stu-id="8509c-113">You need to create and configure the following objects to deploy a load balancer:</span></span>

* <span data-ttu-id="8509c-114">**Configuration d’adresses IP frontales**: contient les adresses IP publiques pour le trafic réseau entrant.</span><span class="sxs-lookup"><span data-stu-id="8509c-114">**Front-end IP configuration**: contains public IP addresses for incoming network traffic</span></span>
* <span data-ttu-id="8509c-115">**Pool d’adresses principales**: contient des cartes réseau (NIC) pour que les machines virtuelles puissent recevoir le trafic réseau de l’équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="8509c-115">**Back-end address pool**: contains network interfaces (NICs) that enable the virtual machines to receive network traffic from the load balancer</span></span>
* <span data-ttu-id="8509c-116">**Règles d’équilibrage de charge**: contient des règles qui mappent un port public situé sur l’équilibrage de charge à un port du pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="8509c-116">**Load-balancing rules**: contains rules that map a public port on the load balancer to port in the back-end address pool</span></span>
* <span data-ttu-id="8509c-117">**Règles NAT entrantes**: contient des règles qui mappent un port public situé sur l’équilibrage de charge vers le port d’une machine virtuelle spécifique située dans le pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="8509c-117">**Inbound NAT rules**: contains rules that map a public port on the load balancer to a port for a specific virtual machine in the back-end address pool</span></span>
* <span data-ttu-id="8509c-118">**Sondes**: contient les sondes d’intégrité utilisées pour vérifier la disponibilité des instances de machines virtuelles du pool d’adresses principales.</span><span class="sxs-lookup"><span data-stu-id="8509c-118">**Probes**: contains health probes that are used to check the availability of virtual machines instances in the back-end address pool</span></span>

<span data-ttu-id="8509c-119">Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](load-balancer-arm.md).</span><span class="sxs-lookup"><span data-stu-id="8509c-119">For more information, see [Azure Resource Manager support for Load Balancer](load-balancer-arm.md).</span></span>

## <a name="set-up-cli-to-use-resource-manager"></a><span data-ttu-id="8509c-120">Configurer l’interface de ligne de commande pour utiliser le gestionnaire de ressources</span><span class="sxs-lookup"><span data-stu-id="8509c-120">Set up CLI to use Resource Manager</span></span>

1. <span data-ttu-id="8509c-121">Si vous n’avez jamais utilisé l’interface de ligne de commande Azure, consultez la section [Installer l’interface de ligne de commande Microsoft Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8509c-121">If you have never used Azure CLI, see [Install and configure the Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="8509c-122">Suivez les instructions jusqu’à l’étape de sélection du compte et de l’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8509c-122">Follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="8509c-123">Exécutez la commande **azure config mode** afin de passer au mode Resource Manager, comme suit :</span><span class="sxs-lookup"><span data-stu-id="8509c-123">Run the **azure config mode** command to switch to Resource Manager mode, as follows:</span></span>

    ```azurecli
    azure config mode arm
    ```

    <span data-ttu-id="8509c-124">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8509c-124">Expected output:</span></span>

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a><span data-ttu-id="8509c-125">Créer un équilibrage de charge interne, étape par étape</span><span class="sxs-lookup"><span data-stu-id="8509c-125">Create an internal load balancer step by step</span></span>

1. <span data-ttu-id="8509c-126">Connectez-vous à Azure.</span><span class="sxs-lookup"><span data-stu-id="8509c-126">Sign in to Azure.</span></span>

    ```azurecli
    azure login
    ```

    <span data-ttu-id="8509c-127">À l’invite, entrez vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="8509c-127">When prompted, enter your Azure credentials.</span></span>

2. <span data-ttu-id="8509c-128">Remplacez les outils de commande par le mode Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8509c-128">Change the command tools to Azure Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="8509c-129">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8509c-129">Create a resource group</span></span>

<span data-ttu-id="8509c-130">Toutes les ressources d’Azure Resource Manager sont associées à un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8509c-130">All resources in Azure Resource Manager are associated with a resource group.</span></span> <span data-ttu-id="8509c-131">Le cas échéant, créez un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="8509c-131">If you haven't done so yet, create a resource group.</span></span>

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a><span data-ttu-id="8509c-132">Créer un jeu d’équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="8509c-132">Create an internal load balancer set</span></span>

1. <span data-ttu-id="8509c-133">Créer un équilibrage de charge interne</span><span class="sxs-lookup"><span data-stu-id="8509c-133">Create an internal load balancer</span></span>

    <span data-ttu-id="8509c-134">Dans le scénario suivant, un groupe de ressources nommé nrprg est créé dans la région Est des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="8509c-134">In the following scenario, a resource group named nrprg is created in East US region.</span></span>

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > <span data-ttu-id="8509c-135">Toutes les ressources d’un équilibrage de charge interne, telles que les réseaux virtuels et les sous-réseaux du réseau virtuel doivent figurer dans le même groupe de ressources et dans la même région.</span><span class="sxs-lookup"><span data-stu-id="8509c-135">All resources for an internal load balancers, such as virtual networks and virtual network subnets, must be in the same resource group and in the same region.</span></span>

2. <span data-ttu-id="8509c-136">Créez une adresse IP frontale pour l’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="8509c-136">Create a front-end IP address for the internal load balancer.</span></span>

    <span data-ttu-id="8509c-137">L’adresse IP utilisée doit se trouver dans la plage de sous-réseau de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="8509c-137">The IP address that you use must be within the subnet range of your virtual network.</span></span>

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. <span data-ttu-id="8509c-138">Créer le pool d’adresses principal.</span><span class="sxs-lookup"><span data-stu-id="8509c-138">Create the back-end address pool.</span></span>

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    <span data-ttu-id="8509c-139">Après avoir défini une adresse IP frontale et un pool d’adresses principales, vous pouvez créer des règles d’équilibrage de charge, des règles NAT entrantes et des sondes d’intégrité personnalisées.</span><span class="sxs-lookup"><span data-stu-id="8509c-139">After you define a front-end IP address and a back-end address pool, you can create load balancer rules, inbound NAT rules, and customized health probes.</span></span>

4. <span data-ttu-id="8509c-140">Créez une règle d’équilibrage de charge pour l’équilibrage de charge interne.</span><span class="sxs-lookup"><span data-stu-id="8509c-140">Create a load balancer rule for the internal load balancer.</span></span>

    <span data-ttu-id="8509c-141">Suivant le scénario ci-dessus, la commande crée une règle d’équilibrage de charge écoutant sur le port 1433 du pool frontal et envoyant le trafic de réseau à charge équilibrée au pool d’adresses principales en utilisant également le port 1433.</span><span class="sxs-lookup"><span data-stu-id="8509c-141">When you follow the previous steps, the command creates a load-balancer rule for listening to port 1433 in the front-end pool and sending load-balanced network traffic to the back-end address pool, also using port 1433.</span></span>

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. <span data-ttu-id="8509c-142">Créez des règles NAT entrantes.</span><span class="sxs-lookup"><span data-stu-id="8509c-142">Create inbound NAT rules.</span></span>

    <span data-ttu-id="8509c-143">Les règles NAT entrantes sont utilisées pour créer des points de terminaison dans un équilibrage de charge qui pointera vers une instance d’ordinateur virtuel spécifique.</span><span class="sxs-lookup"><span data-stu-id="8509c-143">Inbound NAT rules are used to create endpoints in a load balancer that go to a specific virtual machine instance.</span></span> <span data-ttu-id="8509c-144">Les étapes précédentes ont permis de créer deux règles NAT pour le Bureau à distance.</span><span class="sxs-lookup"><span data-stu-id="8509c-144">The previous steps created two NAT rules  for remote desktop.</span></span>

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. <span data-ttu-id="8509c-145">Créez des sondes d'intégrité pour l'équilibreur de charge.</span><span class="sxs-lookup"><span data-stu-id="8509c-145">Create health probes for the load balancer.</span></span>

    <span data-ttu-id="8509c-146">Une sonde d’intégrité vérifie toutes les instances de machine virtuelle pour s’assurer qu’elles peuvent transmettre le trafic réseau.</span><span class="sxs-lookup"><span data-stu-id="8509c-146">A health probe checks all virtual machine instances to make sure they can send network traffic.</span></span> <span data-ttu-id="8509c-147">L’instance de machine virtuelle présentant des contrôles de sonde défaillants est supprimée de l’équilibrage de charge jusqu’à ce qu’elle revienne en ligne et que la sonde valide son intégrité.</span><span class="sxs-lookup"><span data-stu-id="8509c-147">The virtual machine instance with failed probe checks is removed from the load balancer until it goes back online and a probe check determines that it's healthy.</span></span>

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > <span data-ttu-id="8509c-148">La plateforme Microsoft Azure utilise une adresse IPv4 statique routable publiquement pour divers scénarios d’administration.</span><span class="sxs-lookup"><span data-stu-id="8509c-148">The Microsoft Azure platform uses a static, publicly routable IPv4 address for a variety of administrative scenarios.</span></span> <span data-ttu-id="8509c-149">L’adresse IP est 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="8509c-149">The IP address is 168.63.129.16.</span></span> <span data-ttu-id="8509c-150">Cette adresse IP ne doit pas être bloquée par les pare-feu, car cela peut entraîner un comportement inattendu.</span><span class="sxs-lookup"><span data-stu-id="8509c-150">This IP address should not be blocked by any firewalls, because this can cause unexpected behavior.</span></span>
    > <span data-ttu-id="8509c-151">En ce qui concerne l’équilibrage de charge interne Azure, cette adresse IP est utilisée par les sondes de l’équilibreur de charge, pour déterminer l’état de santé pour les machines virtuelles dans un jeu d’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8509c-151">With respect to Azure internal load balancing, this IP address is used by monitoring probes from the load balancer to determine the health state for virtual machines in a load-balanced set.</span></span> <span data-ttu-id="8509c-152">Si un groupe de sécurité réseau est utilisé pour limiter le trafic vers les machines virtuelles Azure dans un jeu d’équilibrage de charge interne, ou est appliqué à un sous-réseau de réseau virtuel, vérifiez qu’une règle de sécurité de réseau n’est ajoutée pour autoriser le trafic à partir de 168.63.129.16.</span><span class="sxs-lookup"><span data-stu-id="8509c-152">If a network security group is used to restrict traffic to Azure virtual machines in an internally load-balanced set or is applied to a virtual network subnet, ensure that a network security rule is added to allow traffic from 168.63.129.16.</span></span>

## <a name="create-nics"></a><span data-ttu-id="8509c-153">Créer des cartes réseau</span><span class="sxs-lookup"><span data-stu-id="8509c-153">Create NICs</span></span>

<span data-ttu-id="8509c-154">Vous devez créer des cartes réseau (ou modifier des cartes existantes) et les associer à des règles NAT, des règles d’équilibreur de charge et des sondes.</span><span class="sxs-lookup"><span data-stu-id="8509c-154">You need to create NICs (or modify existing ones) and associate them to NAT rules, load balancer rules, and probes.</span></span>

1. <span data-ttu-id="8509c-155">Créez une carte réseau nommée *lb-nic1-be*, puis associez-la à la règle NAT *rdp1* et au pool d’adresses principales *beilb*.</span><span class="sxs-lookup"><span data-stu-id="8509c-155">Create an NIC named *lb-nic1-be*, and then associate it with the *rdp1* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
    ```

    <span data-ttu-id="8509c-156">Sortie attendue :</span><span class="sxs-lookup"><span data-stu-id="8509c-156">Expected output:</span></span>

        info:    Executing command network nic create
        + Looking up the network interface "lb-nic1-be"
        + Looking up the subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up the network interface "lb-nic1-be"
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

2. <span data-ttu-id="8509c-157">Créez une carte réseau nommée *lb-nic2-be*, puis associez-la à la règle NAT *rdp2* et au pool d’adresses principales *beilb*.</span><span class="sxs-lookup"><span data-stu-id="8509c-157">Create an NIC named *lb-nic2-be*, and then associate it with the *rdp2* NAT rule and the *beilb* back-end address pool.</span></span>

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. <span data-ttu-id="8509c-158">Créez une machine virtuelle nommée *DB1*, puis associez-la à la carte réseau nommée *lb-nic1-be*.</span><span class="sxs-lookup"><span data-stu-id="8509c-158">Create a virtual machine named *DB1*, and then associate it with the NIC named *lb-nic1-be*.</span></span> <span data-ttu-id="8509c-159">Un compte de stockage appelé *web1nrp* est créé avant d’exécuter la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8509c-159">A storage account called *web1nrp* is created before the following command runs:</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > <span data-ttu-id="8509c-160">Les machines virtuelles d’un équilibreur de charge doivent se trouver dans le même groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8509c-160">VMs in a load balancer need to be in the same availability set.</span></span> <span data-ttu-id="8509c-161">Utilisez `azure availset create` pour créer un groupe à haute disponibilité.</span><span class="sxs-lookup"><span data-stu-id="8509c-161">Use `azure availset create` to create an availability set.</span></span>

4. <span data-ttu-id="8509c-162">Créez une machine virtuelle nommée *DB2*, puis associez-la à la carte réseau nommée *lb-nic2-be*.</span><span class="sxs-lookup"><span data-stu-id="8509c-162">Create a virtual machine (VM) named *DB2*, and then associate it with the NIC named *lb-nic2-be*.</span></span> <span data-ttu-id="8509c-163">Un compte de stockage appelé *web1nrp* a été créé avant d’exécuter la commande ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8509c-163">A storage account called *web1nrp* was created before running the following command.</span></span>

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a><span data-ttu-id="8509c-164">Suppression d’un équilibreur de charge</span><span class="sxs-lookup"><span data-stu-id="8509c-164">Delete a load balancer</span></span>

<span data-ttu-id="8509c-165">Pour supprimer un équilibrage de charge, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8509c-165">To remove a load balancer, use the following command:</span></span>

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a><span data-ttu-id="8509c-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8509c-166">Next steps</span></span>

[<span data-ttu-id="8509c-167">Configurer le mode de distribution d’équilibrage de charge à l’aide de l’affinité d’IP source</span><span class="sxs-lookup"><span data-stu-id="8509c-167">Configure a load balancer distribution mode by using source IP affinity</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="8509c-168">Configuration des paramètres du délai d’expiration TCP inactif pour votre équilibrage de charge</span><span class="sxs-lookup"><span data-stu-id="8509c-168">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)

