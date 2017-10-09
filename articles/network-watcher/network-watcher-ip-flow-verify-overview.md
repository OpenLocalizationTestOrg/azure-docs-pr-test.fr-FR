---
title: "flux de tooIP aaaIntroduction Vérifiez dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble de hello IP de l’Observateur réseau flux vérifier la capacité"
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
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="12cef-103">Flux de tooIP introduction Vérifiez dans l’Observateur réseau de Azure</span><span class="sxs-lookup"><span data-stu-id="12cef-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="12cef-104">Les flux IP vérifier si un paquet est autorisé ou refusé tooor à partir d’un ordinateur virtuel en fonction des informations de 5-tuple.</span><span class="sxs-lookup"><span data-stu-id="12cef-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="12cef-105">Ces informations se composent de la direction, du protocole, de l’adresse IP locale, de l’adresse IP distante, du port local et du port distant.</span><span class="sxs-lookup"><span data-stu-id="12cef-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="12cef-106">Si les paquets hello sont refusée par un groupe de sécurité, nom hello de règle hello refusé les paquets hello est retournée.</span><span class="sxs-lookup"><span data-stu-id="12cef-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="12cef-107">Alors que toutes les adresses IP source ou de destination peut être choisie, cette fonctionnalité permet aux administrateurs de diagnostiquer rapidement les problèmes de connectivité à partir d’ou toohello internet et à partir d’ou l’environnement local de toohello.</span><span class="sxs-lookup"><span data-stu-id="12cef-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="12cef-108">La vérification des flux IP cible une interface réseau d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="12cef-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="12cef-109">Flux de trafic est ensuite vérifié selon tooor de paramètres hello configuré à partir de cette interface réseau.</span><span class="sxs-lookup"><span data-stu-id="12cef-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="12cef-110">Cette fonctionnalité est utile pour confirmer si une règle dans un groupe de sécurité réseau bloque entrée ou sortie tooor le trafic à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="12cef-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="12cef-111">Une instance de l’Observateur réseau besoins toobe est créé dans toutes les régions que vous envisagez de flux d’IP toorun vérifier.</span><span class="sxs-lookup"><span data-stu-id="12cef-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="12cef-112">L’Observateur réseau est un service régional et peut uniquement être exécuté sur les ressources Bonjour même région.</span><span class="sxs-lookup"><span data-stu-id="12cef-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="12cef-113">Cela n’affecte pas hello résultats de flux de l’IP vérifier comme itinéraire hello associé hello que s’affichera toujours de carte réseau.</span><span class="sxs-lookup"><span data-stu-id="12cef-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="12cef-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="12cef-115">Next steps</span></span>

<span data-ttu-id="12cef-116">Visitez hello suivant article toolearn si un paquet est autorisé ou refusé pour un ordinateur virtuel spécifique via le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="12cef-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="12cef-117">Vérifiez si le trafic est autorisé sur une machine virtuelle avec IP flux vérifier à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="12cef-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












