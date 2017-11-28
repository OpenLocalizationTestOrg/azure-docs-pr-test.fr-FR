---
title: "à l’aide d’aaaOpen ports tooa VM hello portail Azure | Documents Microsoft"
description: "Découvrez comment tooopen un port / créer un point de terminaison de tooyour machine virtuelle Windows à l’aide du modèle de déploiement du Gestionnaire de ressources hello Bonjour portail Azure"
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
ms.openlocfilehash: aba789c65254651899aa688f256fe616c3d0126d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-ports-tooa-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="c531e-103">Comment tooopen ports virtuels tooa avec hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="c531e-103">How tooopen ports tooa virtual machine with hello Azure portal</span></span>
[!INCLUDE [virtual-machines-common-nsg-quickstart](../../../includes/virtual-machines-common-nsg-quickstart.md)]

## <a name="quick-commands"></a><span data-ttu-id="c531e-104">Commandes rapides</span><span class="sxs-lookup"><span data-stu-id="c531e-104">Quick commands</span></span>
<span data-ttu-id="c531e-105">Vous pouvez également [effectuer ces étapes à l’aide d’Azure PowerShell](nsg-quickstart-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c531e-105">You can also [perform these steps using Azure PowerShell](nsg-quickstart-powershell.md).</span></span>

<span data-ttu-id="c531e-106">Créez d’abord votre Groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c531e-106">First, create your Network Security Group.</span></span> <span data-ttu-id="c531e-107">Sélectionnez un groupe de ressources dans le portail de hello, choisissez **ajouter**, puis recherchez et sélectionnez **groupe de sécurité réseau**:</span><span class="sxs-lookup"><span data-stu-id="c531e-107">Select a resource group in hello portal, choose **Add**, then search for and select **Network security group**:</span></span>

![Ajouter un groupe de sécurité réseau](./media/nsg-quickstart-portal/add-nsg.png)

<span data-ttu-id="c531e-109">Entrez un nom pour votre groupe de sécurité réseau, sélectionnez ou créez un groupe de ressources, et sélectionnez un emplacement.</span><span class="sxs-lookup"><span data-stu-id="c531e-109">Enter a name for your Network Security Group, select or create a resource group, and select a location.</span></span> <span data-ttu-id="c531e-110">Sélectionnez **Créer** quand vous avez terminé :</span><span class="sxs-lookup"><span data-stu-id="c531e-110">Select **Create** when finished:</span></span>

![Création d'un groupe de sécurité réseau](./media/nsg-quickstart-portal/create-nsg.png)

<span data-ttu-id="c531e-112">Sélectionnez un nouveau groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="c531e-112">Select your new Network Security Group.</span></span> <span data-ttu-id="c531e-113">Sélectionnez « Entrant des règles de sécurité », puis hello **ajouter** bouton toocreate une règle :</span><span class="sxs-lookup"><span data-stu-id="c531e-113">Select 'Inbound security rules', then select hello **Add** button toocreate a rule:</span></span>

![Ajouter une règle de trafic entrant](./media/nsg-quickstart-portal/add-inbound-rule.png)

<span data-ttu-id="c531e-115">Choisissez un commun **Service** à partir du menu déroulant de hello, tel que *HTTP*.</span><span class="sxs-lookup"><span data-stu-id="c531e-115">Choose a common **Service** from hello drop-down menu, such as *HTTP*.</span></span> <span data-ttu-id="c531e-116">Vous pouvez également sélectionner *personnalisé* tooprovide un toouse de port spécifique.</span><span class="sxs-lookup"><span data-stu-id="c531e-116">You can also select *Custom* tooprovide a specific port toouse.</span></span> <span data-ttu-id="c531e-117">Si vous le souhaitez, modifier la priorité de hello ou nom.</span><span class="sxs-lookup"><span data-stu-id="c531e-117">If desired, change hello priority or name.</span></span> <span data-ttu-id="c531e-118">ordre de hello dans lequel les règles sont appliquées - une valeur numérique hello inférieure hello affecte Hello priorité, hello antérieures hello règle est appliquée.</span><span class="sxs-lookup"><span data-stu-id="c531e-118">hello priority affects hello order in which rules are applied - hello lower hello numerical value, hello earlier hello rule is applied.</span></span> <span data-ttu-id="c531e-119">Vous pouvez également sélectionner **avancé** haut hello cette tooenter écran spécifique à une source IP bloc ou plage de ports, par exemple.</span><span class="sxs-lookup"><span data-stu-id="c531e-119">You can also select **Advanced** at hello top of this screen tooenter a specific source IP block or port range, for example.</span></span> <span data-ttu-id="c531e-120">Lorsque vous êtes prêt, sélectionnez **OK** règle de hello toocreate :</span><span class="sxs-lookup"><span data-stu-id="c531e-120">When you are ready, select **OK** toocreate hello rule:</span></span>

![Créer une règle de trafic entrant](./media/nsg-quickstart-portal/create-inbound-rule.png)

<span data-ttu-id="c531e-122">L’étape finale consiste tooassociate groupe de sécurité de votre réseau avec un sous-réseau ou une interface réseau spécifique.</span><span class="sxs-lookup"><span data-stu-id="c531e-122">Your final step is tooassociate your Network Security Group with a subnet or a specific network interface.</span></span> <span data-ttu-id="c531e-123">Nous allons associer hello groupe de sécurité réseau à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c531e-123">Let's associate hello Network Security Group with a subnet.</span></span> <span data-ttu-id="c531e-124">Sélectionnez **Sous-réseaux**, puis choisissez **Associer** :</span><span class="sxs-lookup"><span data-stu-id="c531e-124">Select **Subnets**, then choose **Associate**:</span></span>

![Associer un groupe de sécurité réseau à un sous-réseau](./media/nsg-quickstart-portal/associate-subnet.png)

<span data-ttu-id="c531e-126">Sélectionnez votre réseau virtuel, puis sous-réseau approprié de hello :</span><span class="sxs-lookup"><span data-stu-id="c531e-126">Select your virtual network, and then select hello appropriate subnet:</span></span>

![Association d’un groupe de sécurité réseau à un réseau virtuel](./media/nsg-quickstart-portal/select-vnet-subnet.png)

<span data-ttu-id="c531e-128">Vous avez maintenant créé un groupe de sécurité réseau, créé une règle de trafic entrant qui autorise le trafic sur le port 80 et l’avez associé à un sous-réseau.</span><span class="sxs-lookup"><span data-stu-id="c531e-128">You have now created a Network Security Group, created an inbound rule that allows traffic on port 80, and associated it with a subnet.</span></span> <span data-ttu-id="c531e-129">Les machines virtuelles que vous vous connectez toothat sous-réseau sont accessibles sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="c531e-129">Any VMs you connect toothat subnet are reachable on port 80.</span></span>

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="c531e-130">En savoir plus sur les groupes de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="c531e-130">More information on Network Security Groups</span></span>
<span data-ttu-id="c531e-131">Hello rapide commandes vous permettent de tooget haut et en cours d’exécution avec tooyour de flux de trafic VM.</span><span class="sxs-lookup"><span data-stu-id="c531e-131">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="c531e-132">Groupes de sécurité réseau fournissent de nombreuses fonctionnalités et granularité pour contrôler les ressources tooyour accès.</span><span class="sxs-lookup"><span data-stu-id="c531e-132">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="c531e-133">Découvrez plus d’informations sur la [création d’un groupe de sécurité réseau et de règles de liste de contrôle d’accès ici](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="c531e-133">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-ps.md).</span></span>

<span data-ttu-id="c531e-134">Pour les applications Web hautement disponibles, vous devez placer vos machines virtuelles derrière un équilibreur de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="c531e-134">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="c531e-135">équilibrage de charge Hello distribue tooVMs le trafic, avec un groupe de sécurité réseau qui fournit un filtrage du trafic.</span><span class="sxs-lookup"><span data-stu-id="c531e-135">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="c531e-136">Pour plus d’informations, consultez [comment le solde tooload Linux virtual machines dans Azure toocreate une application hautement disponible](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="c531e-136">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c531e-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c531e-137">Next steps</span></span>
<span data-ttu-id="c531e-138">Dans cet exemple, vous avez créé un trafic de tooallow HTTP règle simple.</span><span class="sxs-lookup"><span data-stu-id="c531e-138">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="c531e-139">Vous trouverez des informations sur la création d’environnements plus Bonjour suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="c531e-139">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="c531e-140">Présentation d’Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="c531e-140">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="c531e-141">Présentation du groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="c531e-141">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)