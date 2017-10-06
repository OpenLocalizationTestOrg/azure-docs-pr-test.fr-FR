---
title: "saut de toonext aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello Observateur réseau capacité de tronçon suivante"
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
ms.openlocfilehash: 916af736d0d52abadeafed746f0f8a0173b11033
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonext-hop-in-azure-network-watcher"></a><span data-ttu-id="26d17-103">Saut de toonext de présentation dans l’Observateur réseau de Azure</span><span class="sxs-lookup"><span data-stu-id="26d17-103">Introduction toonext hop in Azure Network Watcher</span></span>

<span data-ttu-id="26d17-104">Le trafic à partir d’une machine virtuelle est envoyé à destination tooa selon les itinéraires effectifs hello associés à une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="26d17-104">Traffic from a VM is sent tooa destination based on hello effective routes associated with a NIC.</span></span> <span data-ttu-id="26d17-105">Tronçon suivant obtient les type de tronçon suivant hello et l’adresse IP d’un paquet à partir d’un ordinateur virtuel spécifique et la carte réseau.</span><span class="sxs-lookup"><span data-stu-id="26d17-105">Next hop gets hello next hop type and IP address of a packet from a specific virtual machine and NIC.</span></span> <span data-ttu-id="26d17-106">Cela permet de toodetermine si hello paquet est dirigée toohello destination ou est dipositif de trafic hello est noir.</span><span class="sxs-lookup"><span data-stu-id="26d17-106">This helps toodetermine if hello packet is being directed toohello destination or is hello traffic being black holed.</span></span> <span data-ttu-id="26d17-107">Une mauvaise configuration des itinéraires par utilisateur hello, où un trafic est dirigé tooan local emplacement ou un équipement virtuel, peut entraîner des problèmes de tooconnectivity.</span><span class="sxs-lookup"><span data-stu-id="26d17-107">An improper configuration of routes by hello user, where a traffic is directed tooan on-premises location or a virtual appliance, can lead tooconnectivity issues.</span></span> <span data-ttu-id="26d17-108">Tronçon suivant retourne également la table d’itinéraires hello associée saut suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="26d17-108">Next hop also returns hello route table associated with hello next hop.</span></span> <span data-ttu-id="26d17-109">Lorsque vous interrogez un tronçon suivant si l’itinéraire de hello est défini comme un itinéraire défini par l’utilisateur, cet itinéraire est retourné.</span><span class="sxs-lookup"><span data-stu-id="26d17-109">When querying a next hop if hello route is defined as a user-defined route, that route will be returned.</span></span> <span data-ttu-id="26d17-110">Sinon, le tronçon suivant renvoie « Itinéraire du système ».</span><span class="sxs-lookup"><span data-stu-id="26d17-110">Otherwise Next hop returns "System Route".</span></span>

![vue d’ensemble du tronçon suivant][1]

<span data-ttu-id="26d17-112">Hello Voici une liste de hello types de tronçon suivant qui peuvent être retournées lors de l’interrogation de tronçon suivant.</span><span class="sxs-lookup"><span data-stu-id="26d17-112">hello following is a list of hello next hop types that can be returned when querying Next hop.</span></span>

* <span data-ttu-id="26d17-113">Internet</span><span class="sxs-lookup"><span data-stu-id="26d17-113">Internet</span></span>
* <span data-ttu-id="26d17-114">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="26d17-114">VirtualAppliance</span></span>
* <span data-ttu-id="26d17-115">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="26d17-115">VirtualNetworkGateway</span></span>
* <span data-ttu-id="26d17-116">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="26d17-116">VnetLocal</span></span>
* <span data-ttu-id="26d17-117">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="26d17-117">HyperNetGateway</span></span>
* <span data-ttu-id="26d17-118">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="26d17-118">VnetPeering</span></span>
* <span data-ttu-id="26d17-119">Aucun</span><span class="sxs-lookup"><span data-stu-id="26d17-119">None</span></span>

### <a name="next-steps"></a><span data-ttu-id="26d17-120">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="26d17-120">Next steps</span></span>

<span data-ttu-id="26d17-121">Découvrez comment toofind de tronçon suivant toouse problèmes de connectivité de réseau en vous rendant sur [saut suivant de vérification hello sur une machine virtuelle](network-watcher-check-next-hop-portal.md)</span><span class="sxs-lookup"><span data-stu-id="26d17-121">Learn how toouse next hop toofind issues with network connectivity by visiting [Check hello next hop on a VM](network-watcher-check-next-hop-portal.md)</span></span>

<!--Image references-->
[1]: ./media/network-watcher-next-hop-overview/figure1.png













