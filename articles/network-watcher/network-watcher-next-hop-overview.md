---
title: "Présentation du tronçon suivant dans Azure Network Watcher | Microsoft Docs"
description: "Cette page fournit une vue d’ensemble de la fonctionnalité de tronçon suivant de Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: febf7bca-e0b7-41d5-838f-a5a40ebc5aac
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 5dd65d2418cae206965a13013dd990b916ad0733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-next-hop-in-azure-network-watcher"></a><span data-ttu-id="12cb4-103">Présentation du tronçon suivant dans Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="12cb4-103">Introduction to next hop in Azure Network Watcher</span></span>

<span data-ttu-id="12cb4-104">Le trafic d’une machine virtuelle est envoyé vers une destination en fonction des itinéraires effectifs associés à une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="12cb4-104">Traffic from a VM is sent to a destination based on the effective routes associated with a NIC.</span></span> <span data-ttu-id="12cb4-105">Le tronçon suivant obtient le type de tronçon suivant et l’adresse IP d’un paquet à partir d’une machine virtuelle et d’une carte réseau spécifiques.</span><span class="sxs-lookup"><span data-stu-id="12cb4-105">Next hop gets the next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="12cb4-106">Cela permet de déterminer si le paquet est dirigé vers la destination ou si le trafic est dirigé vers un trou noir.</span><span class="sxs-lookup"><span data-stu-id="12cb4-106">This helps to determine if the packet is being directed to the destination or is the traffic being black holed.</span></span> <span data-ttu-id="12cb4-107">Une mauvaise configuration des itinéraires par l’utilisateur, où le trafic est dirigé vers un emplacement local ou une appliance virtuelle, peut provoquer des problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="12cb4-107">An improper configuration of routes by the user, where a traffic is directed to an on-premises location or a virtual appliance, can lead to connectivity issues.</span></span> <span data-ttu-id="12cb4-108">Le tronçon suivant renvoie également la table d’itinéraires associée au tronçon suivant.</span><span class="sxs-lookup"><span data-stu-id="12cb4-108">Next hop also returns the route table associated with the next hop.</span></span> <span data-ttu-id="12cb4-109">Lorsque vous interrogez un tronçon suivant pour savoir si l’itinéraire est défini comme un itinéraire défini par l’utilisateur, celui-ci est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="12cb4-109">When querying a next hop if the route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="12cb4-110">Sinon, le tronçon suivant renvoie « Itinéraire du système ».</span><span class="sxs-lookup"><span data-stu-id="12cb4-110">Otherwise Next hop returns "System Route".</span></span>

![vue d’ensemble du tronçon suivant][1]

<span data-ttu-id="12cb4-112">Voici une liste des types de tronçons suivants qui peuvent être renvoyés lors de l’interrogation du tronçon suivant.</span><span class="sxs-lookup"><span data-stu-id="12cb4-112">The following is a list of the next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="12cb4-113">Internet</span><span class="sxs-lookup"><span data-stu-id="12cb4-113">Internet</span></span>
* <span data-ttu-id="12cb4-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="12cb4-114">VirtualAppliance</span></span>
* <span data-ttu-id="12cb4-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="12cb4-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="12cb4-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="12cb4-116">VnetLocal</span></span>
* <span data-ttu-id="12cb4-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="12cb4-117">HyperNetGateway</span></span>
* <span data-ttu-id="12cb4-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="12cb4-118">VnetPeering</span></span>
* <span data-ttu-id="12cb4-119">Aucun</span><span class="sxs-lookup"><span data-stu-id="12cb4-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="12cb4-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12cb4-120">Next steps</span></span>

<span data-ttu-id="12cb4-121">Découvrez comment utiliser le tronçon suivant pour repérer les problèmes de connectivité réseau en consultant [Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal](network-watcher-check-next-hop-portal.md) (Déterminer quel est le type de tronçon suivant utilisé par la fonctionnalité de tronçon suivant dans Azure Network Watcher à l’aide du portail).</span><span class="sxs-lookup"><span data-stu-id="12cb4-121">Learn how to use next hop to find issues with network connectivity by visiting [Check the next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













