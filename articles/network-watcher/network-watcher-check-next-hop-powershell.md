---
title: "aaaFind de tronçon suivant avec Azure réseau observateur du prochain saut - PowerShell | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver le hello de type de tronçon suivant est et à l’aide des adresses ip de tronçon suivant à l’aide de PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="513e2-103">Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Azure à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="513e2-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="513e2-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="513e2-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="513e2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="513e2-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="513e2-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="513e2-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="513e2-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="513e2-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="513e2-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="513e2-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="513e2-109">Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="513e2-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="513e2-110">Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.</span><span class="sxs-lookup"><span data-stu-id="513e2-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="513e2-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="513e2-111">Before you begin</span></span>

<span data-ttu-id="513e2-112">Dans ce scénario, vous allez utiliser hello type de tronçon suivant toofind portail Azure hello et l’adresse IP.</span><span class="sxs-lookup"><span data-stu-id="513e2-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="513e2-113">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="513e2-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="513e2-114">scénario de Hello suppose également qu’un groupe de ressources avec un ordinateur virtuel valide existe toobe utilisé.</span><span class="sxs-lookup"><span data-stu-id="513e2-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="513e2-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="513e2-115">Scenario</span></span>

<span data-ttu-id="513e2-116">scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="513e2-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="513e2-117">toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="513e2-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="513e2-118">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="513e2-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="513e2-119">première étape de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="513e2-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="513e2-120">Hello `$networkWatcher` variable est passée de tronçon suivant de toohello vérifier l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="513e2-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="513e2-121">Obtenir une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="513e2-121">Get a virtual machine</span></span>

<span data-ttu-id="513e2-122">Tronçon suivant retourne le saut suivant de hello et l’adresse IP hello saut suivant de hello à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="513e2-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="513e2-123">Un Id d’un ordinateur virtuel est requis pour l’applet de commande hello.</span><span class="sxs-lookup"><span data-stu-id="513e2-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="513e2-124">Si vous connaissez déjà les ID hello de hello machine virtuelle toouse, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="513e2-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="513e2-125">Tronçon suivant requiert que les ressources d’ordinateur virtuel hello est allouée toorun.</span><span class="sxs-lookup"><span data-stu-id="513e2-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="513e2-126">Obtenir les interfaces réseau de hello</span><span class="sxs-lookup"><span data-stu-id="513e2-126">Get hello network interfaces</span></span>

<span data-ttu-id="513e2-127">adresse IP de Hello d’une carte réseau sur l’ordinateur virtuel de hello est nécessaire, dans cet exemple, nous récupérons hello cartes d’interface réseau sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="513e2-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="513e2-128">Si vous connaissez déjà hello IP d’adresses que vous souhaitez tootest sur l’ordinateur virtuel de hello, vous pouvez ignorer cette étape.</span><span class="sxs-lookup"><span data-stu-id="513e2-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="513e2-129">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="513e2-129">Get Next Hop</span></span>

<span data-ttu-id="513e2-130">Maintenant que nous appelons hello `Get-AzureRmNetworkWatcherNextHop` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="513e2-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="513e2-131">Nous allons passer hello d’applet de commande hello Observateur réseau, l’ordinateur virtuel Id, adresse IP source et adresse IP de destination.</span><span class="sxs-lookup"><span data-stu-id="513e2-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="513e2-132">Dans cet exemple, adresse IP de destination hello est tooa machine virtuelle dans un autre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="513e2-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="513e2-133">Il existe une passerelle de réseau virtuel entre des réseaux virtuels deux hello.</span><span class="sxs-lookup"><span data-stu-id="513e2-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="513e2-134">Passer en revue les résultats</span><span class="sxs-lookup"><span data-stu-id="513e2-134">Review results</span></span>

<span data-ttu-id="513e2-135">Lorsque vous avez terminé, les résultats de hello sont fournies.</span><span class="sxs-lookup"><span data-stu-id="513e2-135">When complete, hello results are provided.</span></span> <span data-ttu-id="513e2-136">adresse IP du tronçon suivant Hello est retournée, ainsi que de type hello de ressource, qu'il s’agit.</span><span class="sxs-lookup"><span data-stu-id="513e2-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="513e2-137">Dans ce scénario, il est hello adresse IP publique de passerelle de réseau virtuel hello.</span><span class="sxs-lookup"><span data-stu-id="513e2-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="513e2-138">Hello liste suivante présente les valeurs de tronçon suivant actuellement disponibles hello :</span><span class="sxs-lookup"><span data-stu-id="513e2-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="513e2-139">**Type de tronçon suivant**</span><span class="sxs-lookup"><span data-stu-id="513e2-139">**Next Hop Type**</span></span>

* <span data-ttu-id="513e2-140">Internet</span><span class="sxs-lookup"><span data-stu-id="513e2-140">Internet</span></span>
* <span data-ttu-id="513e2-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="513e2-141">VirtualAppliance</span></span>
* <span data-ttu-id="513e2-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="513e2-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="513e2-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="513e2-143">VnetLocal</span></span>
* <span data-ttu-id="513e2-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="513e2-144">HyperNetGateway</span></span>
* <span data-ttu-id="513e2-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="513e2-145">VnetPeering</span></span>
* <span data-ttu-id="513e2-146">Aucun</span><span class="sxs-lookup"><span data-stu-id="513e2-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="513e2-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="513e2-147">Next steps</span></span>

<span data-ttu-id="513e2-148">Découvrez comment tooreview vos paramètres de groupe de sécurité réseau par programme en vous rendant sur [NSG audit avec l’Observateur réseau](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="513e2-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















