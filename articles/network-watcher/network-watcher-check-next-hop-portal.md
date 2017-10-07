---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - portail Azure | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver le hello de type de tronçon suivant est et l’adresse ip à l’aide de tronçon suivant hello portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 7b459dcf-4077-424e-a774-f7bfa34c5975
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b64a2a5275c15aa8bdb10601de4ae1504a9ab551
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-hello-portal"></a><span data-ttu-id="a833a-103">Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="a833a-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using hello portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a833a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="a833a-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="a833a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a833a-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="a833a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a833a-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="a833a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a833a-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="a833a-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="a833a-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="a833a-109">Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="a833a-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="a833a-110">Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.</span><span class="sxs-lookup"><span data-stu-id="a833a-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a833a-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a833a-111">Before you begin</span></span>

<span data-ttu-id="a833a-112">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="a833a-112">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="a833a-113">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="a833a-113">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a833a-114">Scénario</span><span class="sxs-lookup"><span data-stu-id="a833a-114">Scenario</span></span>

<span data-ttu-id="a833a-115">scénario de Hello abordée dans cet article utilise toofind de tronçon suivant out de type hello du saut suivant et l’adresse IP pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="a833a-115">hello scenario covered in this article uses Next hop toofind out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="a833a-116">toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a833a-116">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="a833a-117">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="a833a-117">In this scenario, you will:</span></span>

* <span data-ttu-id="a833a-118">Récupérer le saut suivant de hello à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="a833a-118">Retrieve hello next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="a833a-119">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="a833a-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="a833a-120">Étape 1</span><span class="sxs-lookup"><span data-stu-id="a833a-120">Step 1</span></span>

<span data-ttu-id="a833a-121">Accédez tooyour des ressources de l’Observateur réseau Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a833a-121">Navigate tooyour Network Watcher resource in hello Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="a833a-122">Étape 2</span><span class="sxs-lookup"><span data-stu-id="a833a-122">Step 2</span></span>

<span data-ttu-id="a833a-123">Cliquez sur **de tronçon suivant** hello volet de navigation, sélectionnez hello virtual machine et interface réseau, remplir hello les IP source et de destination, puis cliquez sur hello **de tronçon suivant** bouton.</span><span class="sxs-lookup"><span data-stu-id="a833a-123">Click **Next hop** in hello navigation pane, select hello virtual machine and network interface, fill out hello source and destination IP, and click hello **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="a833a-124">Tronçon suivant requiert que les ressources d’ordinateur virtuel hello est allouée toorun.</span><span class="sxs-lookup"><span data-stu-id="a833a-124">Next hop requires that hello VM resource is allocated toorun.</span></span>

![Vue d’ensemble de l’écran d’obtention du tronçon suivant][1]

### <a name="step-3"></a><span data-ttu-id="a833a-126">Étape 3 :</span><span class="sxs-lookup"><span data-stu-id="a833a-126">Step 3</span></span>

<span data-ttu-id="a833a-127">Une fois la tâche hello est terminée, les résultats de hello sont fournies.</span><span class="sxs-lookup"><span data-stu-id="a833a-127">Once hello task is complete, hello results are provided.</span></span> <span data-ttu-id="a833a-128">Hello d’adresse IP et le type du saut suivant de périphérique hello est, s’affiche.</span><span class="sxs-lookup"><span data-stu-id="a833a-128">hello IP address and type of device hello next hop is, is displayed.</span></span> <span data-ttu-id="a833a-129">Hello tableau suivant montre les valeurs retournées disponible hello dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="a833a-129">hello following table shows hello available returned values in hello portal.</span></span>

<span data-ttu-id="a833a-130">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="a833a-130">**Next Hop Type**</span></span>

* <span data-ttu-id="a833a-131">Internet</span><span class="sxs-lookup"><span data-stu-id="a833a-131">Internet</span></span>
* <span data-ttu-id="a833a-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="a833a-132">VirtualAppliance</span></span>
* <span data-ttu-id="a833a-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="a833a-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="a833a-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="a833a-134">VnetLocal</span></span>
* <span data-ttu-id="a833a-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="a833a-135">HyperNetGateway</span></span>
* <span data-ttu-id="a833a-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="a833a-136">VnetPeering</span></span>
* <span data-ttu-id="a833a-137">Aucun</span><span class="sxs-lookup"><span data-stu-id="a833a-137">None</span></span>

<span data-ttu-id="a833a-138">Si un itinéraire personnalisé a été utilisé tooroute ce trafic, itinéraire défini par l’utilisateur de hello (UDR) est également affiché avec les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="a833a-138">If a custom route was used tooroute this traffic, hello User-defined route (UDR) is shown as well with hello results.</span></span>

![Résultats d’obtention du tronçon suivant][2]

## <a name="next-steps"></a><span data-ttu-id="a833a-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a833a-140">Next steps</span></span>

<span data-ttu-id="a833a-141">Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a833a-141">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














