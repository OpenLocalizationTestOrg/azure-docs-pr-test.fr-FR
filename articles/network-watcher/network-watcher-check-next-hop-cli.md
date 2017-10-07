---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - Azure CLI 2.0 | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver quel hello de type de tronçon suivant est et à l’aide des adresses ip de tronçon suivant à l’aide de CLI d’Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="4e667-103">Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e667-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4e667-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="4e667-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="4e667-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e667-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="4e667-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4e667-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="4e667-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e667-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="4e667-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="4e667-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="4e667-109">Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="4e667-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="4e667-110">Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.</span><span class="sxs-lookup"><span data-stu-id="4e667-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="4e667-111">Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="4e667-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="4e667-112">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4e667-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4e667-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4e667-113">Before you begin</span></span>

<span data-ttu-id="4e667-114">Dans ce scénario, vous allez utiliser hello le type de tronçon suivant CLI d’Azure toofind hello et l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="4e667-114">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="4e667-115">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="4e667-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="4e667-116">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="4e667-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="4e667-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="4e667-117">Scenario</span></span>

<span data-ttu-id="4e667-118">scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="4e667-118">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="4e667-119">toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e667-119">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="4e667-120">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="4e667-120">Get Next Hop</span></span>

<span data-ttu-id="4e667-121">Nous appelons hello du tronçon suivant hello tooget `az network watcher show-next-hop` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="4e667-121">tooget hello next hop we call hello `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="4e667-122">Nous transmettons le groupe de ressources de l’Observateur réseau hello applet de commande hello hello NetworkWatcher, l’ordinateur virtuel Id, adresse IP source et adresse IP de destination.</span><span class="sxs-lookup"><span data-stu-id="4e667-122">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="4e667-123">Dans cet exemple, adresse IP de destination hello est tooa machine virtuelle dans un autre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="4e667-123">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="4e667-124">Il existe une passerelle de réseau virtuel entre des réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="4e667-124">There is a virtual network gateway between hello two virtual networks.</span></span>

<span data-ttu-id="4e667-125">Si vous n’avez pas encore, installer et configurer hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4e667-125">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="4e667-126">Ensuite, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="4e667-126">Then run hello following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="4e667-127">Si hello machine virtuelle possède plusieurs cartes réseau et le transfert IP est activé sur aucun des hello cartes réseau, puis hello paramètre de carte réseau (-i-l’id de la carte réseau) doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="4e667-127">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="4e667-128">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="4e667-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="4e667-129">Passer en revue les résultats</span><span class="sxs-lookup"><span data-stu-id="4e667-129">Review results</span></span>

<span data-ttu-id="4e667-130">Lorsque vous avez terminé, les résultats de hello sont fournies.</span><span class="sxs-lookup"><span data-stu-id="4e667-130">When complete, hello results are provided.</span></span> <span data-ttu-id="4e667-131">adresse IP du tronçon suivant Hello est retournée, ainsi que de type hello de ressource, qu'il s’agit.</span><span class="sxs-lookup"><span data-stu-id="4e667-131">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="4e667-132">Hello liste suivante présente les valeurs de tronçon suivant actuellement disponibles hello :</span><span class="sxs-lookup"><span data-stu-id="4e667-132">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="4e667-133">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="4e667-133">**Next Hop Type**</span></span>

* <span data-ttu-id="4e667-134">Internet</span><span class="sxs-lookup"><span data-stu-id="4e667-134">Internet</span></span>
* <span data-ttu-id="4e667-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="4e667-135">VirtualAppliance</span></span>
* <span data-ttu-id="4e667-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="4e667-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="4e667-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="4e667-137">VnetLocal</span></span>
* <span data-ttu-id="4e667-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="4e667-138">HyperNetGateway</span></span>
* <span data-ttu-id="4e667-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="4e667-139">VnetPeering</span></span>
* <span data-ttu-id="4e667-140">Aucun</span><span class="sxs-lookup"><span data-stu-id="4e667-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e667-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4e667-141">Next steps</span></span>

<span data-ttu-id="4e667-142">Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="4e667-142">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
