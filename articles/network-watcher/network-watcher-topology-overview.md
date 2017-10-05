---
title: "Présentation de la topologie dans Azure Network Watcher | Microsoft Docs"
description: "Cette page fournit une vue d’ensemble des fonctionnalités de topologie de Network Watcher"
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
ms.openlocfilehash: 42443f614b76b8180ac163b9889163021adbf048
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-topology-in-azure-network-watcher"></a><span data-ttu-id="0657f-103">Présentation de la topologie dans Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="0657f-103">Introduction to topology in Azure Network Watcher</span></span>

<span data-ttu-id="0657f-104">La topologie renvoie un graphique des ressources réseau figurant dans un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0657f-104">Topology returns a graph of network resources in a virtual network.</span></span> <span data-ttu-id="0657f-105">Ce graphique illustre l’interconnexion entre les ressources afin de représenter la connectivité réseau de bout en bout.</span><span class="sxs-lookup"><span data-stu-id="0657f-105">The graph depicts the interconnection between the resources to represent the end to end network connectivity.</span></span>

![Vue d’ensemble de la topologie][1]

<span data-ttu-id="0657f-107">Dans le portail, la fonction Topologie renvoie les objets de ressource par réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="0657f-107">In the portal, Topology returns the resource objects on a per virtual network basis.</span></span> <span data-ttu-id="0657f-108">Les relations sont représentées par des lignes entre les ressources. Les ressources situées à l’extérieur de la région Network Watcher, même si elles figurent dans le groupe de ressources, ne sont pas affichées.</span><span class="sxs-lookup"><span data-stu-id="0657f-108">The relationships are depicted by lines between the resources Resources outside of the Network Watcher region, even if in the resource group will not be displayed.</span></span> <span data-ttu-id="0657f-109">Les ressources renvoyées dans la vue du portail sont un sous-ensemble des composants réseau qui sont représentés graphiquement.</span><span class="sxs-lookup"><span data-stu-id="0657f-109">The resources returned in the portal view are a subset of the networking components that are graphed.</span></span> <span data-ttu-id="0657f-110">Pour visualiser la liste complète des ressources réseau, vous pouvez utiliser [PowerShell](network-watcher-topology-powershell.md) ou [REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="0657f-110">To see the full list of networking resources you can use [PowerShell](network-watcher-topology-powershell.md) or [REST](network-watcher-topology-rest.md)</span></span>

> [!NOTE]
> <span data-ttu-id="0657f-111">Une instance de Network Watcher est requise dans chaque région sur laquelle vous souhaitez exécuter la fonction Topologie.</span><span class="sxs-lookup"><span data-stu-id="0657f-111">An instance of Network Watcher is required in each region that you want to run Topology on.</span></span>

<span data-ttu-id="0657f-112">Lorsque les ressources sont renvoyées, la connexion entre ces dernières est modélisée sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="0657f-112">As resources are returned the connection between them are modeled under two relationships.</span></span>

- <span data-ttu-id="0657f-113">**Imbrication** - Exemple : un réseau virtuel contient un sous-ensemble contenant une carte réseau.</span><span class="sxs-lookup"><span data-stu-id="0657f-113">**Containment** - Example: Virtual Network contains a Subnet which contains a NIC</span></span>
- <span data-ttu-id="0657f-114">**Associé** - Exemple : une carte réseau est associée à une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="0657f-114">**Associated** - Example: A NIC is associated with a VM</span></span>

### <a name="next-steps"></a><span data-ttu-id="0657f-115">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0657f-115">Next steps</span></span>

<span data-ttu-id="0657f-116">Découvrez comment utiliser PowerShell pour récupérer la vue Topologie en consultant l’article [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md) (Visualiser la topologie Network Watcher avec PowerShell).</span><span class="sxs-lookup"><span data-stu-id="0657f-116">Learn how to use PowerShell to retrieve the Topology view by visiting [Network Watcher topology with PowerShell](network-watcher-topology-powershell.md)</span></span>

<!--Image references-->

[1]: ./media/network-watcher-topology-overview/topology.png
