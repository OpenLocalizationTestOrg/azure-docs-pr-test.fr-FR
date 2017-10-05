---
title: "Rechercher le tronçon suivant avec la fonction Tronçon suivant d’Azure Network Watcher - Portail Azure | Microsoft Docs"
description: "Cet article explique comment rechercher le type de tronçon suivant et l’adresse IP à l’aide de la fonction Tronçon suivant par le biais du Portail Azure."
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
ms.openlocfilehash: 5434b7972346821985c459fc4620805adb88676b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-the-portal"></a><span data-ttu-id="16d5a-103">Découvrez le type de tronçon suivant grâce à la fonction Tronçon suivant d’Azure Network Watcher dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16d5a-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using the portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="16d5a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="16d5a-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="16d5a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="16d5a-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="16d5a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="16d5a-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="16d5a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="16d5a-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="16d5a-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="16d5a-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="16d5a-109">Tronçon suivant est une fonctionnalité de Network Watcher qui permet d’obtenir le type de tronçon suivant et l’adresse IP à partir d’une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="16d5a-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="16d5a-110">Cette fonctionnalité est utile pour déterminer si le trafic sortant d’une machine virtuelle passe par une passerelle, Internet ou des réseaux virtuels pour atteindre sa destination.</span><span class="sxs-lookup"><span data-stu-id="16d5a-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="16d5a-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="16d5a-111">Before you begin</span></span>

<span data-ttu-id="16d5a-112">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="16d5a-112">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="16d5a-113">Ce scénario suppose également qu’un groupe de ressources avec une machine virtuelle valide existe et peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="16d5a-113">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="16d5a-114">Scénario</span><span class="sxs-lookup"><span data-stu-id="16d5a-114">Scenario</span></span>

<span data-ttu-id="16d5a-115">Le scénario décrit dans cet article utilise la fonctionnalité Tronçon suivant pour rechercher le type de tronçon suivant et l’adresse IP d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="16d5a-115">The scenario covered in this article uses Next hop to find out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="16d5a-116">Pour en savoir plus sur Tronçon suivant, consultez [Next Hop Overview (Vue d’ensemble de la fonctionnalité Tronçon suivant)](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="16d5a-116">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="16d5a-117">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="16d5a-117">In this scenario, you will:</span></span>

* <span data-ttu-id="16d5a-118">Récupérer le tronçon suivant à partir d’une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="16d5a-118">Retrieve the next hop from a virtual machine.</span></span>

## <a name="get-next-hop"></a><span data-ttu-id="16d5a-119">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="16d5a-119">Get Next Hop</span></span>

### <a name="step-1"></a><span data-ttu-id="16d5a-120">Étape 1 :</span><span class="sxs-lookup"><span data-stu-id="16d5a-120">Step 1</span></span>

<span data-ttu-id="16d5a-121">Accédez à votre ressource Network Watcher dans le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="16d5a-121">Navigate to your Network Watcher resource in the Azure portal.</span></span>

### <a name="step-2"></a><span data-ttu-id="16d5a-122">Étape 2</span><span class="sxs-lookup"><span data-stu-id="16d5a-122">Step 2</span></span>

<span data-ttu-id="16d5a-123">Dans le volet de navigation, cliquez sur **Tronçon suivant**, sélectionnez la machine virtuelle et l’interface réseau, renseignez les adresses IP source et de destination, puis cliquez sur le bouton **Tronçon suivant**.</span><span class="sxs-lookup"><span data-stu-id="16d5a-123">Click **Next hop** in the navigation pane, select the virtual machine and network interface, fill out the source and destination IP, and click the **Next hop** button.</span></span>

> [!NOTE]
> <span data-ttu-id="16d5a-124">L’exécution de la fonctionnalité Tronçon suivant nécessite l’allocation de la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="16d5a-124">Next hop requires that the VM resource is allocated to run.</span></span>

![Vue d’ensemble de l’écran d’obtention du tronçon suivant][1]

### <a name="step-3"></a><span data-ttu-id="16d5a-126">Étape 3</span><span class="sxs-lookup"><span data-stu-id="16d5a-126">Step 3</span></span>

<span data-ttu-id="16d5a-127">Une fois la tâche exécutée, les résultats sont présentés.</span><span class="sxs-lookup"><span data-stu-id="16d5a-127">Once the task is complete, the results are provided.</span></span> <span data-ttu-id="16d5a-128">L’adresse IP et le type d’appareil sur lequel figure le saut suivant s’affichent.</span><span class="sxs-lookup"><span data-stu-id="16d5a-128">The IP address and type of device the next hop is, is displayed.</span></span> <span data-ttu-id="16d5a-129">La section ci-après présente les valeurs pouvant être renvoyées dans le portail.</span><span class="sxs-lookup"><span data-stu-id="16d5a-129">The following table shows the available returned values in the portal.</span></span>

<span data-ttu-id="16d5a-130">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="16d5a-130">**Next Hop Type**</span></span>

* <span data-ttu-id="16d5a-131">Internet</span><span class="sxs-lookup"><span data-stu-id="16d5a-131">Internet</span></span>
* <span data-ttu-id="16d5a-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="16d5a-132">VirtualAppliance</span></span>
* <span data-ttu-id="16d5a-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="16d5a-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="16d5a-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="16d5a-134">VnetLocal</span></span>
* <span data-ttu-id="16d5a-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="16d5a-135">HyperNetGateway</span></span>
* <span data-ttu-id="16d5a-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="16d5a-136">VnetPeering</span></span>
* <span data-ttu-id="16d5a-137">Aucun</span><span class="sxs-lookup"><span data-stu-id="16d5a-137">None</span></span>

<span data-ttu-id="16d5a-138">Si un routage personnalisé a été utilisé pour acheminer ce trafic, le routage défini par l’utilisateur (UDR) apparaît avec les résultats.</span><span class="sxs-lookup"><span data-stu-id="16d5a-138">If a custom route was used to route this traffic, the User-defined route (UDR) is shown as well with the results.</span></span>

![Résultats d’obtention du tronçon suivant][2]

## <a name="next-steps"></a><span data-ttu-id="16d5a-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="16d5a-140">Next steps</span></span>

<span data-ttu-id="16d5a-141">Découvrez comment programmer la révision des paramètres de votre groupe de sécurité réseau sur la page [NSG Auditing with Network Watcher (Audit du Groupe de sécurité réseau avec Network Watcher)](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="16d5a-141">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-check-next-hop-portal/figure1.png
[2]: ./media/network-watcher-check-next-hop-portal/figure2.png














