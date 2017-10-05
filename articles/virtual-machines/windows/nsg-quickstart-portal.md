---
title: "Ouvrir des ports sur une machine virtuelle à l’aide du portail Azure | Microsoft Docs"
description: "Découvrez comment ouvrir un port / créer un point de terminaison sur votre machine virtuelle Windows à l’aide du modèle de déploiement Resource Manager dans le Portail Azure"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: f7cf0319-5ee7-435e-8f94-c484bf5ee6f1
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 33bc0be0aeae6d0276fd8999b9ac0a010e3067ba
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-open-ports-to-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="f71e9-103">Guide d’ouverture de ports vers une machine virtuelle avec le portail Azure</span><span class="sxs-lookup"><span data-stu-id="f71e9-103">How to open ports to a virtual machine with the Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="f71e9-104">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="f71e9-104">Quick commands</span></span>
<span data-ttu-id="f71e9-105">Vous pouvez également [effectuer ces étapes à l’aide d’Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f71e9-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="f71e9-106">Créez d’abord votre Groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f71e9-106">First, create your Network Security Group.</span></span> <span data-ttu-id="f71e9-107">Sélectionnez un groupe de ressources dans le portail, choisissez **Ajouter**, puis recherchez et sélectionnez **Groupe de sécurité de réseau** :</span><span class="sxs-lookup"><span data-stu-id="f71e9-107">Select a resource group in the portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Ajouter un groupe de sécurité réseau](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="f71e9-109">Entrez un nom pour votre groupe de sécurité réseau, sélectionnez ou créez un groupe de ressources, et sélectionnez un emplacement.</span><span class="sxs-lookup"><span data-stu-id="f71e9-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="f71e9-110">Sélectionnez **Créer** quand vous avez terminé :</span><span class="sxs-lookup"><span data-stu-id="f71e9-110">Select **Create** when finished:</span></span>

![Création d'un groupe de sécurité réseau](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="f71e9-112">Sélectionnez un nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f71e9-112">Select your new Network Security Group.</span></span> <span data-ttu-id="f71e9-113">Sélectionnez « Règles de sécurité entrantes », puis cliquez sur le bouton **Ajouter** pour créer une règle :</span><span class="sxs-lookup"><span data-stu-id="f71e9-113">Select 'Inbound security rules', then select the **Add** button to create a rule:</span></span>

![Ajouter une règle de trafic entrant](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="f71e9-115">Choisissez un **Service** courant dans le menu déroulant, tel que *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="f71e9-115">Choose a common **Service** from the drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="f71e9-116">Vous pouvez aussi sélectionner *Personnalisé* pour indiquer un port spécifique à utiliser.</span><span class="sxs-lookup"><span data-stu-id="f71e9-116">You can also select *Custom* to provide a specific port to use.</span></span> <span data-ttu-id="f71e9-117">Si vous le souhaitez, modifiez la priorité ou le nom.</span><span class="sxs-lookup"><span data-stu-id="f71e9-117">If desired, change the priority or name.</span></span> <span data-ttu-id="f71e9-118">La priorité affecte l’ordre dans lequel les règles sont appliquées (plus la valeur numérique est faible, plus la règle est appliquée précocement).</span><span class="sxs-lookup"><span data-stu-id="f71e9-118">The priority affects the order in which rules are applied - the lower the numerical value, the earlier the rule is applied.</span></span> <span data-ttu-id="f71e9-119">Vous pouvez aussi sélectionner **Avancé** en haut de cet écran pour entrer un bloc d’adresses IP sources ou une plage de ports spécifique, par exemple.</span><span class="sxs-lookup"><span data-stu-id="f71e9-119">You can also select **Advanced** at the top of this screen to enter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="f71e9-120">Quand vous êtes prêt, sélectionnez **OK** pour créer la règle :</span><span class="sxs-lookup"><span data-stu-id="f71e9-120">When you are ready, select **OK** to create the rule:</span></span>

![Créer une règle de trafic entrant](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="f71e9-122">L’étape finale consiste à associer un sous-réseau ou une interface réseau spécifique à votre groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="f71e9-122">Your final step is to associate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="f71e9-123">Associons le groupe de sécurité réseau à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f71e9-123">Let's associate the Network Security Group with a subnet.</span></span> <span data-ttu-id="f71e9-124">Sélectionnez **Sous-réseaux**, puis choisissez **Associer** :</span><span class="sxs-lookup"><span data-stu-id="f71e9-124">Select **Subnets**, then choose **Associate**:</span></span>

![Associer un groupe de sécurité réseau à un sous-réseau](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="f71e9-126">Sélectionnez votre réseau virtuel, puis sélectionnez le sous-réseau approprié :</span><span class="sxs-lookup"><span data-stu-id="f71e9-126">Select your virtual network, and then select the appropriate subnet:</span></span>

![Association d’un groupe de sécurité réseau à un réseau virtuel](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="f71e9-128">Vous avez maintenant créé un groupe de sécurité réseau, créé une règle de trafic entrant qui autorise le trafic sur le port 80 et l’avez associé à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="f71e9-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="f71e9-129">Toute machine virtuelle que vous connectez à ce sous-réseau est accessible sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="f71e9-129">Any VMs you connect to that subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="f71e9-130">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="f71e9-130">More information on Network Security Groups</span></span>
<span data-ttu-id="f71e9-131">Les commandes rapides vous permettent d’être opérationnel avec le trafic entrant vers votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="f71e9-131">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="f71e9-132">Les groupes de sécurité réseau fournissent un grand nombre de fonctionnalités intéressantes et une granularité pour contrôler l’accès à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="f71e9-132">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="f71e9-133">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f71e9-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="f71e9-134">Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="f71e9-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="f71e9-135">L’équilibreur de charge répartit le trafic entre les machines virtuelles, avec un groupe de sécurité réseau qui assure le filtrage du trafic.</span><span class="sxs-lookup"><span data-stu-id="f71e9-135">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="f71e9-136">Pour plus d’informations, consultez [Guide pratique pour équilibrer la charge des machines virtuelles Linux dans Azure pour créer une application hautement disponible](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="f71e9-136">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f71e9-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f71e9-137">Next steps</span></span>
<span data-ttu-id="f71e9-138">Dans cet exemple, vous avez créé une règle simple pour autoriser le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="f71e9-138">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="f71e9-139">Vous trouverez plus d’informations sur la création d’environnements plus détaillés dans les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f71e9-139">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="f71e9-140">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f71e9-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="f71e9-141">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="f71e9-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)