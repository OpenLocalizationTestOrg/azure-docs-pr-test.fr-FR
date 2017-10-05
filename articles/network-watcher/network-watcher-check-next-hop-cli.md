---
title: "Rechercher le tronçon suivant avec la fonction Tronçon suivant Azure Network Watcher - Azure CLI 2.0 | Microsoft Docs"
description: "Cet article explique comment rechercher le type de tronçon suivant et l’adresse IP avec la fonction Tronçon suivant dans l’interface de ligne de commande Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: d1ee6870ba0188ff2c473e4cca12a5bdc1f97d3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="17f6a-103">Découvrez le type de tronçon suivant grâce à la fonction Tronçon suivant Azure Network Watcher dans l’interface de ligne de commande Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="17f6a-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="17f6a-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="17f6a-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="17f6a-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="17f6a-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="17f6a-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="17f6a-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="17f6a-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="17f6a-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="17f6a-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="17f6a-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="17f6a-109">Tronçon suivant est une fonctionnalité de Network Watcher qui permet d’obtenir le type de tronçon suivant et l’adresse IP à partir d’une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="17f6a-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="17f6a-110">Cette fonctionnalité est utile pour déterminer si le trafic sortant d’une machine virtuelle passe par une passerelle, Internet ou des réseaux virtuels pour atteindre sa destination.</span><span class="sxs-lookup"><span data-stu-id="17f6a-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="17f6a-111">Dans cet article, notre CLI nouvelle génération, Azure CLI 2.0, est utilisée pour le modèle de déploiement de gestion des ressources. Celle-ci est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="17f6a-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="17f6a-112">Pour exécuter la procédure indiquée dans cet article, vous devez [installer l’interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="17f6a-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="17f6a-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="17f6a-113">Before you begin</span></span>

<span data-ttu-id="17f6a-114">Dans ce scénario, vous allez utiliser l’interface de ligne de commande Azure pour rechercher le type de tronçon suivant et l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="17f6a-114">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="17f6a-115">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="17f6a-115">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="17f6a-116">Ce scénario suppose également qu’un groupe de ressources avec une machine virtuelle valide existe et peut être utilisé.</span><span class="sxs-lookup"><span data-stu-id="17f6a-116">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="17f6a-117">Scénario</span><span class="sxs-lookup"><span data-stu-id="17f6a-117">Scenario</span></span>

<span data-ttu-id="17f6a-118">Le scénario décrit dans cet article utilise Tronçon suivant, une fonctionnalité de Network Watcher qui détecte le type de tronçon suivant et l’adresse IP d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="17f6a-118">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="17f6a-119">Pour en savoir plus sur Tronçon suivant, consultez [Next Hop Overview (Vue d’ensemble de la fonctionnalité Tronçon suivant)](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="17f6a-119">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="17f6a-120">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="17f6a-120">Get Next Hop</span></span>

<span data-ttu-id="17f6a-121">Pour obtenir le tronçon suivant, appelez l’applet de commande `az network watcher show-next-hop`.</span><span class="sxs-lookup"><span data-stu-id="17f6a-121">To get the next hop we call the `az network watcher show-next-hop` cmdlet.</span></span> <span data-ttu-id="17f6a-122">Nous transférons à l’applet de commande le groupe de ressources Network Watcher, Network Watcher, l’identifiant de la machine virtuelle, l’adresse IP source et l’adresse IP de destination.</span><span class="sxs-lookup"><span data-stu-id="17f6a-122">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="17f6a-123">Dans cet exemple, l’adresse IP de destination désigne une machine virtuelle sur un autre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="17f6a-123">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="17f6a-124">Les deux réseaux virtuels sont séparés par une passerelle réseau virtuelle.</span><span class="sxs-lookup"><span data-stu-id="17f6a-124">There is a virtual network gateway between the two virtual networks.</span></span>

<span data-ttu-id="17f6a-125">Si vous ne l’avez pas encore fait, installez et configurez la dernière version d’[Azure CLI 2.0](/cli/azure/install-az-cli2) et connectez-vous à un compte Azure par le biais de la commande [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="17f6a-125">If you haven't yet, install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="17f6a-126">Exécutez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="17f6a-126">Then run the following command:</span></span>

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
<span data-ttu-id="17f6a-127">Si la machine virtuelle possède plusieurs cartes réseau et si le transfert IP est activé sur l’une des cartes réseau, le paramètre de la carte réseau (-i nic-id) doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="17f6a-127">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="17f6a-128">Sinon, il est facultatif.</span><span class="sxs-lookup"><span data-stu-id="17f6a-128">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="17f6a-129">Passer en revue les résultats</span><span class="sxs-lookup"><span data-stu-id="17f6a-129">Review results</span></span>

<span data-ttu-id="17f6a-130">Une fois que vous avez terminé, les résultats sont présentés.</span><span class="sxs-lookup"><span data-stu-id="17f6a-130">When complete, the results are provided.</span></span> <span data-ttu-id="17f6a-131">L’adresse IP du tronçon suivant est renvoyée, ainsi que le type de ressource.</span><span class="sxs-lookup"><span data-stu-id="17f6a-131">The next hop IP address is returned as well as the type of resource it is.</span></span>

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

<span data-ttu-id="17f6a-132">La liste suivante indique les valeurs de NextHopType actuellement disponibles :</span><span class="sxs-lookup"><span data-stu-id="17f6a-132">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="17f6a-133">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="17f6a-133">**Next Hop Type**</span></span>

* <span data-ttu-id="17f6a-134">Internet</span><span class="sxs-lookup"><span data-stu-id="17f6a-134">Internet</span></span>
* <span data-ttu-id="17f6a-135">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="17f6a-135">VirtualAppliance</span></span>
* <span data-ttu-id="17f6a-136">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="17f6a-136">VirtualNetworkGateway</span></span>
* <span data-ttu-id="17f6a-137">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="17f6a-137">VnetLocal</span></span>
* <span data-ttu-id="17f6a-138">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="17f6a-138">HyperNetGateway</span></span>
* <span data-ttu-id="17f6a-139">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="17f6a-139">VnetPeering</span></span>
* <span data-ttu-id="17f6a-140">Aucun</span><span class="sxs-lookup"><span data-stu-id="17f6a-140">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="17f6a-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="17f6a-141">Next steps</span></span>

<span data-ttu-id="17f6a-142">Découvrez comment programmer la révision des paramètres de votre groupe de sécurité réseau sur la page [NSG Auditing with Network Watcher (Audit du Groupe de sécurité réseau avec Network Watcher)](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="17f6a-142">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
