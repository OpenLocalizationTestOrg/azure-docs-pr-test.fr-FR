---
title: aaaOpen ports tooa VM Linux avec Azure CLI 2.0 | Documents Microsoft
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour Linux VM à l’aide de déploiement du Gestionnaire de ressources Azure hello modéliser et hello Azure CLI 2.0"
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
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="9d47a-103">Ouvrir les ports et les points de terminaison tooa Linux VM avec hello CLI d’Azure</span><span class="sxs-lookup"><span data-stu-id="9d47a-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="9d47a-104">Vous ouvrez un port ou créer un point de terminaison, tooa machine virtuelle (VM) dans Azure en créant un filtre de réseau sur un sous-réseau ou une interface réseau de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9d47a-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="9d47a-105">Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, sur une ressource de toohello de groupe de sécurité réseau associé qui reçoit le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="9d47a-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="9d47a-106">Nous allons utiliser un exemple courant de trafic web sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="9d47a-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="9d47a-107">Cet article vous explique comment tooopen un tooa port VM par hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="9d47a-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="9d47a-108">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9d47a-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="9d47a-109">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="9d47a-109">Quick commands</span></span>
<span data-ttu-id="9d47a-110">Groupe de sécurité réseau toocreate et règles, vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="9d47a-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="9d47a-111">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="9d47a-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="9d47a-112">Les noms de paramètre sont par exemple *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.</span><span class="sxs-lookup"><span data-stu-id="9d47a-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="9d47a-113">Créer le groupe de sécurité réseau hello avec [az réseau nsg créer](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="9d47a-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="9d47a-114">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="9d47a-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="9d47a-115">Ajouter une règle avec [créer de règle de groupe de sécurité réseau du réseau az](/cli/azure/network/nsg/rule#create) tooallow HTTP tooyour webserver du trafic (ou l’ajuster pour votre propre scénario, tel que de la connectivité de base de données ou de l’accès SSH).</span><span class="sxs-lookup"><span data-stu-id="9d47a-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="9d47a-116">Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* tooallow TCP du trafic sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="9d47a-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="9d47a-117">Associer hello groupe de sécurité réseau avec l’interface de réseau de votre machine virtuelle (NIC) [mise à jour de la carte réseau az réseau](/cli/azure/network/nic#update).</span><span class="sxs-lookup"><span data-stu-id="9d47a-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="9d47a-118">exemple Hello associe une carte réseau nommée *myNic* avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="9d47a-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="9d47a-119">Ou bien, vous pouvez associer votre groupe de sécurité réseau avec un sous-réseau de réseau virtuel avec [mise à jour de sous-réseau de réseau virtuel az réseau](/cli/azure/network/vnet/subnet#update) plutôt que de simplement toohello interface de réseau sur une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9d47a-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="9d47a-120">exemple Hello associe un sous-réseau existant nommé *mySubnet* Bonjour *myVnet* réseau virtuel avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="9d47a-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="9d47a-121">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="9d47a-121">More information on Network Security Groups</span></span>
<span data-ttu-id="9d47a-122">Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM.</span><span class="sxs-lookup"><span data-stu-id="9d47a-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="9d47a-123">Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès.</span><span class="sxs-lookup"><span data-stu-id="9d47a-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="9d47a-124">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](tutorial-virtual-network.md#secure-network-traffic).</span><span class="sxs-lookup"><span data-stu-id="9d47a-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="9d47a-125">Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="9d47a-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="9d47a-126">équilibrage de charge Hello distribue tooVMs le trafic, avec un groupe de sécurité réseau qui fournit un filtrage du trafic.</span><span class="sxs-lookup"><span data-stu-id="9d47a-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="9d47a-127">Pour plus d’informations, consultez [comment le solde tooload Linux virtual machines dans Azure toocreate une application hautement disponible](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="9d47a-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d47a-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9d47a-128">Next steps</span></span>
<span data-ttu-id="9d47a-129">Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple.</span><span class="sxs-lookup"><span data-stu-id="9d47a-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="9d47a-130">Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="9d47a-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="9d47a-131">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9d47a-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="9d47a-132">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="9d47a-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
