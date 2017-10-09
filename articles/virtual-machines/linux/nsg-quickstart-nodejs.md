---
title: aaaOpen ports tooa VM Linux avec Azure CLI 1.0 | Documents Microsoft
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour Linux VM à l’aide de déploiement du Gestionnaire de ressources Azure hello modéliser et hello Azure CLI 1.0"
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
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="a9cc0-103">Ouvrir les ports et les points de terminaison tooa Linux VM dans Azure à l’aide hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a9cc0-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="a9cc0-104">Vous ouvrez un port ou créer un point de terminaison, tooa machine virtuelle (VM) dans Azure en créant un filtre de réseau sur un sous-réseau ou une interface réseau de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="a9cc0-105">Vous placez ces filtres, qui contrôlent le trafic entrant et sortant, sur une ressource de toohello de groupe de sécurité réseau associé qui reçoit le trafic de hello.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="a9cc0-106">Nous allons utiliser un exemple courant de trafic web sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="a9cc0-107">Cet article vous montre comment une machine virtuelle tooa port à l’aide de tooopen hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a9cc0-108">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="a9cc0-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a9cc0-109">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="a9cc0-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a9cc0-110">[Azure CLI 1.0](#quick-commands) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="a9cc0-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a9cc0-111">[Azure CLI 2.0](nsg-quickstart.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="a9cc0-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="a9cc0-112">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="a9cc0-112">Quick commands</span></span>
<span data-ttu-id="a9cc0-113">toocreate un groupe de sécurité réseau et des règles [hello Azure CLI 1.0](../../cli-install-nodejs.md) installé et utilise le mode Gestionnaire de ressources :</span><span class="sxs-lookup"><span data-stu-id="a9cc0-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="a9cc0-114">Bonjour les exemples suivants, remplacez les exemples de noms de paramètre par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="a9cc0-115">Les exemples de noms de paramètre comprennent *myResourceGroup*, *myNetworkSecurityGroup* et *myVMnet*.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="a9cc0-116">Créez votre groupe de sécurité réseau en entrant votre nom et votre emplacement en conséquence.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="a9cc0-117">Hello exemple suivant crée un groupe de sécurité réseau nommé *myNetworkSecurityGroup* Bonjour *eastus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="a9cc0-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="a9cc0-118">Ajouter un serveur Web de règle tooallow HTTP trafic tooyour (ou ajuster pour votre propre scénario, tel que de la connectivité de base de données ou de l’accès SSH).</span><span class="sxs-lookup"><span data-stu-id="a9cc0-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="a9cc0-119">Hello exemple suivant crée une règle nommée *myNetworkSecurityGroupRule* tooallow TCP du trafic sur le port 80 :</span><span class="sxs-lookup"><span data-stu-id="a9cc0-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

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

<span data-ttu-id="a9cc0-120">Hello groupe de sécurité réseau associé disposant d’interface réseau (NIC) de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="a9cc0-121">exemple Hello associe une carte réseau nommée *myNic* avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a9cc0-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="a9cc0-122">Vous pouvez également associer votre groupe de sécurité réseau avec un sous-réseau de réseau virtuel plutôt que simplement toohello interface de réseau sur une seule machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="a9cc0-123">exemple Hello associe un sous-réseau existant nommé *mySubnet* Bonjour *myVnet* réseau virtuel avec hello groupe de sécurité réseau nommé *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="a9cc0-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="a9cc0-124">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a9cc0-124">More information on Network Security Groups</span></span>
<span data-ttu-id="a9cc0-125">Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="a9cc0-126">Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="a9cc0-127">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a9cc0-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="a9cc0-128">Vous pouvez définir des groupes de sécurité réseau et des règles de liste de contrôle d’accès dans le cadre de modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="a9cc0-129">En savoir plus sur la [création de groupes de sécurité réseau avec des modèles](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="a9cc0-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="a9cc0-130">Si vous avez besoin de réacheminement de port de toouse toomap un unique externe tooan port interne sur votre machine virtuelle, utilisez un équilibrage de charge et les règles de traduction d’adresses réseau (NAT).</span><span class="sxs-lookup"><span data-stu-id="a9cc0-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="a9cc0-131">Par exemple, vous pouvez tooexpose le port TCP 8080 en externe et souhaitez le trafic est dirigé tooTCP port 80 sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="a9cc0-132">En savoir plus sur [la création d'un équilibreur de charge accessible sur Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="a9cc0-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9cc0-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a9cc0-133">Next steps</span></span>
<span data-ttu-id="a9cc0-134">Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple.</span><span class="sxs-lookup"><span data-stu-id="a9cc0-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="a9cc0-135">Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="a9cc0-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="a9cc0-136">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9cc0-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="a9cc0-137">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="a9cc0-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="a9cc0-138">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a9cc0-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

