---
title: "Rechercher le tronçon suivant avec la fonction Tronçon suivant Azure Network Watcher - Azure CLI 1.0 | Microsoft Docs"
description: "Cet article explique comment rechercher le type de tronçon suivant et l’adresse IP avec la fonction Tronçon suivant dans l’interface de ligne de commande Azure."
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
ms.openlocfilehash: ff88e945060ae033717ceb29db1352e112f05a3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="01aca-103">Découvrez le type de tronçon suivant grâce à la fonction Tronçon suivant Azure Network Watcher dans l’interface de ligne de commande Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="01aca-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="01aca-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="01aca-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="01aca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01aca-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="01aca-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="01aca-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="01aca-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="01aca-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="01aca-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="01aca-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="01aca-109">Tronçon suivant est une fonctionnalité de Network Watcher qui permet d’obtenir le type de tronçon suivant et l’adresse IP à partir d’une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="01aca-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="01aca-110">Cette fonctionnalité est utile pour déterminer si le trafic sortant d’une machine virtuelle passe par une passerelle, Internet ou des réseaux virtuels pour atteindre sa destination.</span><span class="sxs-lookup"><span data-stu-id="01aca-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="01aca-111">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="01aca-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="01aca-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="01aca-112">Before you begin</span></span>

<span data-ttu-id="01aca-113">Dans ce scénario, vous allez utiliser l’interface de ligne de commande Azure pour rechercher le type de tronçon suivant et l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="01aca-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="01aca-114">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="01aca-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="01aca-115">Ce scénario suppose également qu’un groupe de ressources avec une machine virtuelle valide existe et peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="01aca-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="01aca-116">Scénario</span><span class="sxs-lookup"><span data-stu-id="01aca-116">Scenario</span></span>

<span data-ttu-id="01aca-117">Le scénario décrit dans cet article utilise Tronçon suivant, une fonctionnalité de Network Watcher qui détecte le type de tronçon suivant et l’adresse IP d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="01aca-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="01aca-118">Pour en savoir plus sur Tronçon suivant, consultez [Next Hop Overview (Vue d’ensemble de la fonctionnalité Tronçon suivant)](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="01aca-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="01aca-119">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="01aca-119">Get Next Hop</span></span>

<span data-ttu-id="01aca-120">Pour obtenir le tronçon suivant, appelez l’applet de commande `azure netowrk watcher next-hop`.</span><span class="sxs-lookup"><span data-stu-id="01aca-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="01aca-121">Nous transférons à l’applet de commande le groupe de ressources Network Watcher, Network Watcher, l’identifiant de la machine virtuelle, l’adresse IP source et l’adresse IP de destination.</span><span class="sxs-lookup"><span data-stu-id="01aca-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="01aca-122">Dans cet exemple, l’adresse IP de destination désigne une machine virtuelle sur un autre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="01aca-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="01aca-123">Les deux réseaux virtuels sont séparés par une passerelle réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="01aca-123">There is a virtual network gateway between the two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="01aca-124">Si la machine virtuelle possède plusieurs cartes réseau et si le transfert IP est activé sur l’une des cartes réseau, le paramètre de la carte réseau (-i nic-id) doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="01aca-124">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="01aca-125">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="01aca-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="01aca-126">Passer en revue les résultats</span><span class="sxs-lookup"><span data-stu-id="01aca-126">Review results</span></span>

<span data-ttu-id="01aca-127">Une fois que vous avez terminé, les résultats sont présentés.</span><span class="sxs-lookup"><span data-stu-id="01aca-127">When complete, the results are provided.</span></span> <span data-ttu-id="01aca-128">L’adresse IP du tronçon suivant est renvoyée, ainsi que le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="01aca-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="01aca-129">La liste suivante indique les valeurs de NextHopType actuellement disponibles :</span><span class="sxs-lookup"><span data-stu-id="01aca-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="01aca-130">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="01aca-130">**Next Hop Type**</span></span>

* <span data-ttu-id="01aca-131">Internet</span><span class="sxs-lookup"><span data-stu-id="01aca-131">Internet</span></span>
* <span data-ttu-id="01aca-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="01aca-132">VirtualAppliance</span></span>
* <span data-ttu-id="01aca-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="01aca-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="01aca-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="01aca-134">VnetLocal</span></span>
* <span data-ttu-id="01aca-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="01aca-135">HyperNetGateway</span></span>
* <span data-ttu-id="01aca-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="01aca-136">VnetPeering</span></span>
* <span data-ttu-id="01aca-137">Aucun</span><span class="sxs-lookup"><span data-stu-id="01aca-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="01aca-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="01aca-138">Next steps</span></span>

<span data-ttu-id="01aca-139">Découvrez comment programmer la révision des paramètres de votre groupe de sécurité réseau sur la page [NSG Auditing with Network Watcher (Audit du Groupe de sécurité réseau avec Network Watcher)](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="01aca-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
