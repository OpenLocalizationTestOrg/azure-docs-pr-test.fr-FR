---
title: "tootopology aaaIntroduction dans l’Observateur réseau de Azure | Documents Microsoft"
description: "Cette page fournit une vue d’ensemble des fonctionnalités de topologie hello Observateur réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e753a435-38e0-482b-846b-121cb547555c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 7fa1c5518e4a25a5db999d898a9ee19fd0121db7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tootopology-in-azure-network-watcher"></a><span data-ttu-id="fcc7d-103">Tootopology de présentation dans l’Observateur réseau de Azure</span><span class="sxs-lookup"><span data-stu-id="fcc7d-103">Introduction tootopology in Azure Network Watcher</span></span>

<span data-ttu-id="fcc7d-104">La topologie renvoie un graphique des ressources réseau figurant dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="fcc7d-105">graphique de Hello représente l’interconnexion hello entre la connectivité réseau de hello ressources toorepresent hello fin tooend.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-105">hello graph depicts hello interconnection between hello resources toorepresent hello end tooend network connectivity.</span></span>

![Vue d’ensemble de la topologie][1]

<span data-ttu-id="fcc7d-107">Dans le portail hello, topologie retourne des objets de ressource hello sur une base de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-107">In hello portal, Topology returns hello resource objects on a per virtual network basis.</span></span> <span data-ttu-id="fcc7d-108">relations de Hello sont représentées par des lignes entre les ressources de hello ressources en dehors de la région de hello Observateur réseau, même si dans la ressource de hello groupe s’afficheront pas.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-108">hello relationships are depicted by lines between hello resources Resources outside of hello Network Watcher region, even if in hello resource group will not be displayed.</span></span> <span data-ttu-id="fcc7d-109">ressources Hello retournées dans la vue du portail hello sont un sous-ensemble de composants réseau hello qui sont représentés graphiquement.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-109">hello resources returned in hello portal view are a subset of hello networking components that are graphed.</span></span> <span data-ttu-id="fcc7d-110">toosee hello la liste complète des ressources réseau, vous pouvez utiliser [PowerShell](network-watcher-topology-powershell.md) ou [REST](network-watcher-topology-rest.md)</span><span class="sxs-lookup"><span data-stu-id="fcc7d-110">toosee hello full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="fcc7d-111">Une instance de l’Observateur réseau est requis dans chaque région que vous voulez toorun topologie sur.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-111">An instance of Network Watcher is required in each region that you want toorun Topology on.</span></span>

<span data-ttu-id="fcc7d-112">Comme les ressources sont retournées les connexion hello entre eux sont modélisés sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-112">As resources are returned hello connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="fcc7d-113">**Imbrication** - Exemple : un réseau virtuel contient un sous-ensemble contenant une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="fcc7d-114">**Associé** - Exemple : une carte réseau est associée à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="fcc7d-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="fcc7d-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fcc7d-115">Next steps</span></span>

<span data-ttu-id="fcc7d-116">Découvrez comment afficher les toouse PowerShell tooretrieve hello topologie en vous rendant sur [topologie de l’Observateur réseau avec PowerShell](network-watcher-topology-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="fcc7d-116">Learn how toouse PowerShell tooretrieve hello Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
