---
title: "Exemples d’interface de ligne de commande Azure | Microsoft Docs"
description: "Exemples d’interface de ligne de commande Azure"
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: kumud
ms.openlocfilehash: 7977460f61bfdabd399e45e86d9bbf2e5083992b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cli-samples-for-networking"></a><span data-ttu-id="14cf4-103">Exemples d’interface de ligne de commande Azure pour la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="14cf4-103">Azure CLI Samples for networking</span></span>

<span data-ttu-id="14cf4-104">Le tableau suivant contient des liens vers des scripts Bash créés à l’aide de l’interface de ligne de commande Azure.</span><span class="sxs-lookup"><span data-stu-id="14cf4-104">The following table includes links to bash scripts built using the Azure CLI.</span></span>

| | |
|-|-|
|<span data-ttu-id="14cf4-105">**Connectivité entre les ressources Azure**</span><span class="sxs-lookup"><span data-stu-id="14cf4-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="14cf4-106">Créer un réseau virtuel pour les applications multiniveau</span><span class="sxs-lookup"><span data-stu-id="14cf4-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-cli-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14cf4-107">Crée un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="14cf4-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="14cf4-108">Le trafic vers le sous-réseau frontal est limité à HTTP et SSH, tandis que le trafic vers le sous-réseau principal est limité à MySQL, port 3306.</span><span class="sxs-lookup"><span data-stu-id="14cf4-108">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> |
| [<span data-ttu-id="14cf4-109">Homologuer deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="14cf4-109">Peer two virtual networks</span></span>](./scripts/virtual-network-cli-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14cf4-110">Crée et connecte deux réseaux virtuels dans la même région.</span><span class="sxs-lookup"><span data-stu-id="14cf4-110">Creates and connects two virtual networks in the same region.</span></span> |
| [<span data-ttu-id="14cf4-111">Acheminer le trafic via une appliance virtuelle réseau</span><span class="sxs-lookup"><span data-stu-id="14cf4-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-cli-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14cf4-112">Crée un réseau virtuel avec des sous-réseaux frontal et principal et une machine virtuelle en mesure d’acheminer le trafic entre les deux sous-réseaux.</span><span class="sxs-lookup"><span data-stu-id="14cf4-112">Creates a virtual network with front-end and back-end subnets and a VM that is able to route traffic between the two subnets.</span></span> |
| [<span data-ttu-id="14cf4-113">Filtrer le trafic réseau de machine virtuelle entrant et sortant</span><span class="sxs-lookup"><span data-stu-id="14cf4-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14cf4-114">Crée un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="14cf4-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="14cf4-115">Le trafic réseau entrant vers le sous-réseau frontal est limité à HTTP, HTTPS et SSH.</span><span class="sxs-lookup"><span data-stu-id="14cf4-115">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH.</span></span> <span data-ttu-id="14cf4-116">Le trafic sortant vers Internet à partir du sous-réseau principal n’est pas autorisé.</span><span class="sxs-lookup"><span data-stu-id="14cf4-116">Outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="14cf4-117">**Équilibrage de charge et direction de trafic**</span><span class="sxs-lookup"><span data-stu-id="14cf4-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="14cf4-118">Équilibrer le trafic sur les machines virtuelles pour la haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="14cf4-118">Load balance traffic to VMs for high availability</span></span>](./scripts/load-balancer-linux-cli-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14cf4-119">Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="14cf4-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="14cf4-120">Équilibrer la charge de plusieurs sites web sur des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="14cf4-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-linux-cli-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="14cf4-121">Crée deux machines virtuelles avec plusieurs configurations IP, jointes à un groupe à haute disponibilité Azure, accessible via Azure Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="14cf4-121">Creates two VMs with multiple IP configurations, joined to an Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="14cf4-122">Diriger le trafic dans plusieurs régions pour une haute disponibilité des applications</span><span class="sxs-lookup"><span data-stu-id="14cf4-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-cli-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="14cf4-123">Crée deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="14cf4-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
