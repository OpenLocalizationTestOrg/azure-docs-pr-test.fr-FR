---
title: "Ouvrir des ports sur une machine virtuelle Linux avec Azure CLI 2.0 | Microsoft Docs"
description: "Découvrez comment ouvrir un port / créer un point de terminaison sur votre machine virtuelle Linux à l’aide du modèle de déploiement Azure Resource Manager et d’Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: d176187fe465264b5f433260de5178b48ca9dd4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-and-endpoints-to-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="ab49b-103">Ouvrir des ports et des points de terminaison sur une machine virtuelle Linux dans Azure avec Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ab49b-103">Open ports and endpoints to a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="ab49b-104">Pour ouvrir un port ou créer un point de terminaison sur une machine virtuelle dans Azure, créez un filtre réseau sur un sous-réseau ou une interface réseau de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ab49b-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="ab49b-105">Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, dans un groupe de sécurité réseau associé à la ressource qui reçoit le trafic.</span><span class="sxs-lookup"><span data-stu-id="ab49b-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="ab49b-106">Nous allons utiliser un exemple courant de trafic web sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="ab49b-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="ab49b-107">Cet article vous montre comment ouvrir un port sur une machine virtuelle avec Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ab49b-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="ab49b-108">Vous pouvez également suivre ces étapes avec [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ab49b-108">You can also perform these steps with the [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ab49b-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="ab49b-109">Quick commands</span></span>
<span data-ttu-id="ab49b-110">Pour créer un groupe de sécurité réseau et des règles, la dernière version [d’Azure CLI 2.0](/cli/azure/install-az-cli2) doit être installée et connectée à un compte Azure à l’aide de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="ab49b-110">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ab49b-111">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="ab49b-111">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ab49b-112">Les noms de paramètre sont par exemple *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.</span><span class="sxs-lookup"><span data-stu-id="ab49b-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="ab49b-113">Créez le groupe de sécurité réseau avec la commande [az network nsg create](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="ab49b-113">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="ab49b-114">L’exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="ab49b-114">The following example creates a network security group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="ab49b-115">Ajoutez une règle avec la commande [az network nsg rule create](/cli/azure/network/nsg/rule#create) pour autoriser le trafic HTTP sur votre serveur Web (ou adaptez en fonction de votre propre scénario, notamment l’accès SSH ou la connectivité de base de données).</span><span class="sxs-lookup"><span data-stu-id="ab49b-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="ab49b-116">L’exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* pour autoriser le trafic TCP sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="ab49b-116">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="ab49b-117">Associez le groupe de sécurité réseau à l’interface réseau (NIC) de votre machine virtuelle avec la commande [az network nic update](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="ab49b-117">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="ab49b-118">L’exemple suivant associe une carte réseau existante nommée *myNic* au groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="ab49b-118">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="ab49b-119">Vous pouvez également associer votre groupe de sécurité réseau à un sous-réseau de réseau virtuel avec la commande [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) et non uniquement à l’interface réseau d’une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ab49b-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="ab49b-120">L’exemple suivant associe un sous-réseau existant nommé *mySubnet* dans le réseau virtuel *myVnet* au groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="ab49b-120">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="ab49b-121">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ab49b-121">More information on Network Security Groups</span></span>
<span data-ttu-id="ab49b-122">Les commandes rapides vous permettent d’être opérationnel avec le trafic entrant vers votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="ab49b-122">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="ab49b-123">Les groupes de sécurité réseau fournissent un grand nombre de fonctionnalités intéressantes et une granularité pour contrôler l’accès à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="ab49b-123">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="ab49b-124">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="ab49b-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="ab49b-125">Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="ab49b-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="ab49b-126">L’équilibreur de charge répartit le trafic entre les machines virtuelles, avec un groupe de sécurité réseau qui assure le filtrage du trafic.</span><span class="sxs-lookup"><span data-stu-id="ab49b-126">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="ab49b-127">Pour plus d’informations, consultez [Guide pratique pour équilibrer la charge des machines virtuelles Linux dans Azure pour créer une application hautement disponible](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="ab49b-127">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab49b-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ab49b-128">Next steps</span></span>
<span data-ttu-id="ab49b-129">Dans cet exemple, vous avez créé une règle simple pour autoriser le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="ab49b-129">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="ab49b-130">Vous trouverez plus d’informations sur la création d’environnements plus détaillés dans les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="ab49b-130">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="ab49b-131">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ab49b-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="ab49b-132">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ab49b-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
