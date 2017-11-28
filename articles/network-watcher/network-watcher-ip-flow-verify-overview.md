---
title: "Présentation de la vérification des flux IP dans Azure Network Watcher | Microsoft Docs"
description: "Cette page fournit une vue d’ensemble de la fonctionnalité de vérification des flux IP de Network Watcher"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9c0dfc449b3d93d8aa4551ce16476c8313d731fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="6b872-103">Présentation de la vérification des flux IP dans Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6b872-103">Introduction to IP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="6b872-104">La vérification des flux IP contrôle si un paquet est autorisé ou refusé en direction ou en provenance d’une machine virtuelle en fonction des informations à 5 tuples.</span><span class="sxs-lookup"><span data-stu-id="6b872-104">IP flow verify checks if a packet is allowed or denied to or from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="6b872-105">Ces informations se composent de la direction, du protocole, de l’adresse IP locale, de l’adresse IP distante, du port local et du port distant.</span><span class="sxs-lookup"><span data-stu-id="6b872-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="6b872-106">Si le paquet est refusé par un groupe de sécurité, le nom de la règle qui a refusé le paquet est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="6b872-106">If the packet is denied by a security group, the name of the rule that denied the packet is returned.</span></span> <span data-ttu-id="6b872-107">Même si toutes les adresses IP source et de destination peuvent être choisies, cette fonctionnalité permet aux administrateurs de diagnostiquer rapidement les problèmes de connectivité en provenance ou à destination d’Internet et en provenance ou à destination de l’environnement local.</span><span class="sxs-lookup"><span data-stu-id="6b872-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or to the internet and from or to the on-premises environment.</span></span>

<span data-ttu-id="6b872-108">La vérification des flux IP cible une interface réseau d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6b872-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="6b872-109">Le flux de trafic est ensuite vérifié en fonction des paramètres configurés vers ou à partir de cette interface réseau.</span><span class="sxs-lookup"><span data-stu-id="6b872-109">Traffic flow is then verified based on the configured settings to or from that network interface.</span></span> <span data-ttu-id="6b872-110">Cette fonctionnalité est utile pour confirmer si une règle d’un groupe de sécurité réseau bloque le trafic entrant ou sortant d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="6b872-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic to or from a virtual machine.</span></span>

<span data-ttu-id="6b872-111">Une instance de Network Watcher doit être créée dans toutes les régions dans lesquelles vous prévoyez d’exécuter la vérification des flux IP.</span><span class="sxs-lookup"><span data-stu-id="6b872-111">An instance of Network Watcher needs to be created in all regions that you plan to run IP flow verify.</span></span> <span data-ttu-id="6b872-112">Network Watcher est un service régional et peut uniquement être exécuté sur des ressources de la même région.</span><span class="sxs-lookup"><span data-stu-id="6b872-112">Network Watcher is a regional service and can only be ran against resources in the same region.</span></span> <span data-ttu-id="6b872-113">Cela n’affecte pas les résultats de la vérification des flux IP, puisque l’itinéraire associé à la carte réseau est toujours renvoyé.</span><span class="sxs-lookup"><span data-stu-id="6b872-113">This does not affect the results of IP flow verify as the route associated with the NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="6b872-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6b872-115">Next steps</span></span>

<span data-ttu-id="6b872-116">Consultez l’article suivant pour savoir si un paquet est autorisé ou refusé pour une machine virtuelle spécifique via le portail.</span><span class="sxs-lookup"><span data-stu-id="6b872-116">Visit the following article to learn if a packet is allowed or denied for a specific virtual machine through the portal.</span></span> [<span data-ttu-id="6b872-117">Vérifier si le trafic est autorisé ou refusé en direction ou en provenance d’une machine virtuelle avec le composant de vérification des flux IP d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6b872-117">Check if traffic is allowed on a VM with IP Flow Verify using the portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












