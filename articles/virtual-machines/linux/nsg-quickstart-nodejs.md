---
title: "Ouvrir des ports sur une machine virtuelle Linux avec Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment ouvrir un port / créer un point de terminaison sur votre machine virtuelle Linux à l’aide du modèle de déploiement Azure Resource Manager et de l’interface de ligne de commande Azure 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 847bc76c37ed929851712ba1c12463a01032e267
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="1d6ef-103">Ouverture de ports et de points de terminaison sur une machine virtuelle Linux dans Azure à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1d6ef-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="1d6ef-104">Pour ouvrir un port ou créer un point de terminaison sur une machine virtuelle dans Azure, créez un filtre réseau sur un sous-réseau ou une interface réseau de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="1d6ef-105">Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, dans un groupe de sécurité réseau associé à la ressource qui reçoit le trafic.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="1d6ef-106">Nous allons utiliser un exemple courant de trafic web sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="1d6ef-107">Cet article vous montre comment ouvrir un port sur une machine virtuelle à l’aide de l’interface de ligne de commande Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="1d6ef-108">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="1d6ef-108">CLI versions to complete the task</span></span>
<span data-ttu-id="1d6ef-109">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="1d6ef-110">[Azure CLI 1.0](#quick-commands) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="1d6ef-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1d6ef-111">[Azure CLI 2.0](nsg-quickstart.md) : notre interface Azure CLI nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d6ef-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="1d6ef-112">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="1d6ef-112">Quick commands</span></span>
<span data-ttu-id="1d6ef-113">Pour créer un groupe de sécurité réseau et des règles, vous devez installer[l’interface de ligne de commande Azure 1.0](../../cli-install-nodejs.md) et utiliser le mode Resource Manager :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="1d6ef-114">Dans les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="1d6ef-115">Les exemples de noms de paramètre comprennent *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="1d6ef-116">Créez votre groupe de sécurité réseau en entrant votre nom et votre emplacement en conséquence.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="1d6ef-117">L’exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* à l’emplacement *eastus* :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-117">The following example creates a Network Security Group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="1d6ef-118">Ajoutez une règle pour autoriser le trafic HTTP sur votre serveur Web (ou ajustez une règle en fonction de votre propre scénario, notamment l’accès SSH ou la connectivité de base de données).</span><span class="sxs-lookup"><span data-stu-id="1d6ef-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="1d6ef-119">L’exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* pour autoriser le trafic TCP sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-119">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="1d6ef-120">Associez un groupe de sécurité réseau associé à l’interface réseau (NIC) de vos machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="1d6ef-121">L’exemple suivant associe une carte réseau existante nommée *myNic* au groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-121">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="1d6ef-122">Vous pouvez également associer votre groupe de sécurité réseau à un sous-réseau de réseau virtuel et non uniquement à l’interface réseau d’une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="1d6ef-123">L’exemple suivant associe un sous-réseau existant nommé *mySubnet* dans le réseau virtuel *myVnet* au groupe de sécurité réseau nommé *myNetworkSecurityGroup* :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-123">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="1d6ef-124">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="1d6ef-124">More information on Network Security Groups</span></span>
<span data-ttu-id="1d6ef-125">Les commandes rapides vous permettent d’être opérationnel avec le trafic entrant vers votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="1d6ef-126">Les groupes de sécurité réseau fournissent un grand nombre de fonctionnalités intéressantes et une granularité pour contrôler l’accès à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="1d6ef-127">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="1d6ef-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="1d6ef-128">Vous pouvez définir des groupes de sécurité réseau et des règles de liste de contrôle d’accès dans le cadre de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="1d6ef-129">En savoir plus sur la [création de groupes de sécurité réseau avec des modèles](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="1d6ef-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="1d6ef-130">Si vous devez utiliser le réacheminement de port pour mapper un seul port externe sur un port interne de votre machine virtuelle, utilisez un équilibreur de charge et des règles de traduction d’adresses réseau (NAT).</span><span class="sxs-lookup"><span data-stu-id="1d6ef-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="1d6ef-131">Par exemple, vous souhaitez peut-être exposer le port TCP 8080 en externe et diriger le trafic vers le port TCP 80 sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="1d6ef-132">En savoir plus sur [la création d'un équilibreur de charge accessible sur Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="1d6ef-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d6ef-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1d6ef-133">Next steps</span></span>
<span data-ttu-id="1d6ef-134">Dans cet exemple, vous avez créé une règle simple pour autoriser le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="1d6ef-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="1d6ef-135">Vous trouverez plus d’informations sur la création d’environnements plus détaillés dans les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="1d6ef-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="1d6ef-136">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d6ef-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="1d6ef-137">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="1d6ef-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="1d6ef-138">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1d6ef-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

