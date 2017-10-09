---
title: aaaAzure exemples PowerShell | Documents Microsoft
description: Exemples Azure PowerShell
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/24/2017
ms.author: georgewallace
ms.openlocfilehash: 130a6e755691b46a9549cad5acaa5bde4fe38e95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-powershell-samples-for-networking"></a><span data-ttu-id="8ab02-103">Exemples Azure PowerShell pour la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="8ab02-103">Azure PowerShell Samples for networking</span></span>

<span data-ttu-id="8ab02-104">Hello tableau suivant inclut tooscripts de liens créés à l’aide d’Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ab02-104">hello following table includes links tooscripts built using Azure PowerShell.</span></span>

| | |
|-|-|
|<span data-ttu-id="8ab02-105">**Connectivité entre les ressources Azure**</span><span class="sxs-lookup"><span data-stu-id="8ab02-105">**Connectivity between Azure resources**</span></span>||
| [<span data-ttu-id="8ab02-106">Créer un réseau virtuel pour les applications multiniveau</span><span class="sxs-lookup"><span data-stu-id="8ab02-106">Create a virtual network for multi-tier applications</span></span>](./scripts/virtual-network-powershell-sample-multi-tier-application.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="8ab02-107">Crée un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="8ab02-107">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="8ab02-108">Sous-réseau de trafic toohello frontal est tooHTTP limitée, lorsque le trafic toohello sous-réseau principal est tooSQL limitée, le port 1433.</span><span class="sxs-lookup"><span data-stu-id="8ab02-108">Traffic toohello front-end subnet is limited tooHTTP, while traffic toohello back-end subnet is limited tooSQL, port 1433.</span></span> |
| [<span data-ttu-id="8ab02-109">Homologuer deux réseaux virtuels</span><span class="sxs-lookup"><span data-stu-id="8ab02-109">Peer two virtual networks</span></span>](./scripts/virtual-network-powershell-sample-peer-two-virtual-networks.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="8ab02-110">Crée et connecte deux réseaux virtuels Bonjour même région.</span><span class="sxs-lookup"><span data-stu-id="8ab02-110">Creates and connects two virtual networks in hello same region.</span></span> |
| [<span data-ttu-id="8ab02-111">Acheminer le trafic via une appliance virtuelle réseau</span><span class="sxs-lookup"><span data-stu-id="8ab02-111">Route traffic through a network virtual appliance</span></span>](./scripts/virtual-network-powershell-sample-route-traffic-through-nva.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="8ab02-112">Crée un réseau virtuel avec les sous-réseaux des serveurs frontaux et principaux et un ordinateur virtuel qui tooroute en mesure de trafic entre les sous-réseaux de hello deux.</span><span class="sxs-lookup"><span data-stu-id="8ab02-112">Creates a virtual network with front-end and back-end subnets and a VM that is able tooroute traffic between hello two subnets.</span></span> |
| [<span data-ttu-id="8ab02-113">Filtrer le trafic réseau de machine virtuelle entrant et sortant</span><span class="sxs-lookup"><span data-stu-id="8ab02-113">Filter inbound and outbound VM network traffic</span></span>](./scripts/virtual-network-powershell-filter-network-traffic.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="8ab02-114">Crée un réseau virtuel avec des sous-réseaux frontaux et principaux.</span><span class="sxs-lookup"><span data-stu-id="8ab02-114">Creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="8ab02-115">Le trafic du réseau entrant toohello le sous-réseau frontal est limitée tooHTTP et HTTPS...</span><span class="sxs-lookup"><span data-stu-id="8ab02-115">Inbound network traffic toohello front-end subnet is limited tooHTTP and HTTPS..</span></span> <span data-ttu-id="8ab02-116">Le trafic sortant toohello Internet à partir du sous-réseau principal de hello n’est pas autorisée.</span><span class="sxs-lookup"><span data-stu-id="8ab02-116">Outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> |
|<span data-ttu-id="8ab02-117">**Équilibrage de charge et direction de trafic**</span><span class="sxs-lookup"><span data-stu-id="8ab02-117">**Load balancing and traffic direction**</span></span>||
| [<span data-ttu-id="8ab02-118">Charger tooVMs le trafic de solde pour la haute disponibilité</span><span class="sxs-lookup"><span data-stu-id="8ab02-118">Load balance traffic tooVMs for high availability</span></span>](./scripts/load-balancer-windows-powershell-sample-nlb.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="8ab02-119">Crée plusieurs machines virtuelles dans une configuration haute disponibilité avec équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="8ab02-119">Creates several virtual machines in a highly available and load balanced configuration.</span></span> |
| [<span data-ttu-id="8ab02-120">Équilibrer la charge de plusieurs sites web sur des machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="8ab02-120">Load balance multiple websites on VMs</span></span>](./scripts/load-balancer-windows-powershell-load-balance-multiple-websites-vm.md?toc=%2fazure%2fnetworking%2ftoc.json) | <span data-ttu-id="8ab02-121">Crée deux machines virtuelles avec plusieurs configurations IP, tooan jointe à haute disponibilité Azure, accessible via un équilibrage de charge Azure.</span><span class="sxs-lookup"><span data-stu-id="8ab02-121">Creates two VMs with multiple IP configurations, joined tooan Azure Availability Set, accessible through an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="8ab02-122">Diriger le trafic dans plusieurs régions pour une haute disponibilité des applications</span><span class="sxs-lookup"><span data-stu-id="8ab02-122">Direct traffic across multiple regions for high application availability</span></span>](./scripts/traffic-manager-powershell-websites-high-availability.md?toc=%2fazure%2fnetworking%2ftoc.json) |  <span data-ttu-id="8ab02-123">Crée deux plans App Service, deux applications web, un profil Traffic Manager et deux points de terminaison Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="8ab02-123">Creates two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> |
| | |
