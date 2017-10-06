---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - Azure CLI 1.0 | Documents Microsoft"
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
ms.openlocfilehash: 54124c051021413695d70ba93c370605abc6ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="e0c13-103">Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide d’Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e0c13-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="e0c13-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="e0c13-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="e0c13-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0c13-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="e0c13-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="e0c13-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="e0c13-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="e0c13-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="e0c13-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="e0c13-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="e0c13-109">Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="e0c13-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="e0c13-110">Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.</span><span class="sxs-lookup"><span data-stu-id="e0c13-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

<span data-ttu-id="e0c13-111">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="e0c13-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e0c13-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e0c13-112">Before you begin</span></span>

<span data-ttu-id="e0c13-113">Dans ce scénario, vous allez utiliser hello le type de tronçon suivant CLI d’Azure toofind hello et l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="e0c13-113">In this scenario, you will use hello Azure CLI toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="e0c13-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="e0c13-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="e0c13-115">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="e0c13-115">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="e0c13-116">Scénario</span><span class="sxs-lookup"><span data-stu-id="e0c13-116">Scenario</span></span>

<span data-ttu-id="e0c13-117">scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="e0c13-117">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="e0c13-118">toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0c13-118">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="e0c13-119">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="e0c13-119">Get Next Hop</span></span>

<span data-ttu-id="e0c13-120">Nous appelons hello du tronçon suivant hello tooget `azure netowrk watcher next-hop` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="e0c13-120">tooget hello next hop we call hello `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="e0c13-121">Nous transmettons le groupe de ressources de l’Observateur réseau hello applet de commande hello hello NetworkWatcher, l’ordinateur virtuel Id, adresse IP source et adresse IP de destination.</span><span class="sxs-lookup"><span data-stu-id="e0c13-121">We pass hello cmdlet hello Network Watcher resource group, hello NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="e0c13-122">Dans cet exemple, adresse IP de destination hello est tooa machine virtuelle dans un autre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="e0c13-122">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="e0c13-123">Il existe une passerelle de réseau virtuel entre des réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="e0c13-123">There is a virtual network gateway between hello two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="e0c13-124">Si hello machine virtuelle possède plusieurs cartes réseau et le transfert IP est activé sur aucun des hello cartes réseau, puis hello paramètre de carte réseau (-i-l’id de la carte réseau) doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="e0c13-124">If hello VM has multiple NICs and IP forwarding is enabled on any of hello NICs, then hello NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="e0c13-125">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="e0c13-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="e0c13-126">Passer en revue les résultats</span><span class="sxs-lookup"><span data-stu-id="e0c13-126">Review results</span></span>

<span data-ttu-id="e0c13-127">Lorsque vous avez terminé, les résultats de hello sont fournies.</span><span class="sxs-lookup"><span data-stu-id="e0c13-127">When complete, hello results are provided.</span></span> <span data-ttu-id="e0c13-128">adresse IP du tronçon suivant Hello est retournée, ainsi que de type hello de ressource, qu'il s’agit.</span><span class="sxs-lookup"><span data-stu-id="e0c13-128">hello next hop IP address is returned as well as hello type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="e0c13-129">Hello liste suivante présente les valeurs de tronçon suivant actuellement disponibles hello :</span><span class="sxs-lookup"><span data-stu-id="e0c13-129">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="e0c13-130">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="e0c13-130">**Next Hop Type**</span></span>

* <span data-ttu-id="e0c13-131">Internet</span><span class="sxs-lookup"><span data-stu-id="e0c13-131">Internet</span></span>
* <span data-ttu-id="e0c13-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="e0c13-132">VirtualAppliance</span></span>
* <span data-ttu-id="e0c13-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="e0c13-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="e0c13-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="e0c13-134">VnetLocal</span></span>
* <span data-ttu-id="e0c13-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="e0c13-135">HyperNetGateway</span></span>
* <span data-ttu-id="e0c13-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="e0c13-136">VnetPeering</span></span>
* <span data-ttu-id="e0c13-137">Aucun</span><span class="sxs-lookup"><span data-stu-id="e0c13-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0c13-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0c13-138">Next steps</span></span>

<span data-ttu-id="e0c13-139">Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e0c13-139">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
