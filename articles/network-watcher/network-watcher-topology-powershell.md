---
title: "topologie de l’Observateur réseau Azure aaaView - PowerShell | Documents Microsoft"
description: "Cet article décrit comment toouse PowerShell tooquery topologie de votre réseau."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: bd0e882d-8011-45e8-a7ce-de231a69fb85
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2bc0ecf5baa81a68be53f55c74f362a7bc97116f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="b6783-103">Afficher la topologie Network Watcher par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6783-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b6783-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6783-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="b6783-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b6783-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="b6783-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b6783-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="b6783-107">API REST</span><span class="sxs-lookup"><span data-stu-id="b6783-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="b6783-108">fonctionnalité de topologie Hello de l’Observateur réseau fournit une représentation visuelle des ressources du réseau hello dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="b6783-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="b6783-109">Dans le portail hello, cette visualisation est présentée tooyou automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b6783-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="b6783-110">informations Hello derrière l’affichage de la topologie hello dans le portail de hello peuvent être récupérées via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b6783-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="b6783-111">Cette fonctionnalité rend les informations de topologie hello plus polyvalente que les données de salutation peuvent être utilisées par les autres toobuild outils out visualisation de hello.</span><span class="sxs-lookup"><span data-stu-id="b6783-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="b6783-112">interconnexion de Hello est modélisée sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="b6783-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="b6783-113">**Relation d’imbrication** - exemple : le réseau virtuel contient un sous-réseau qui contient une carte réseau</span><span class="sxs-lookup"><span data-stu-id="b6783-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="b6783-114">**Associé** - exemple : une carte réseau est associée à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="b6783-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="b6783-115">Hello Voici les propriétés qui sont retournées lors de l’interrogation hello API REST de topologie.</span><span class="sxs-lookup"><span data-stu-id="b6783-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="b6783-116">**nom** hello - nom de ressource de hello</span><span class="sxs-lookup"><span data-stu-id="b6783-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="b6783-117">**ID** -hello uri de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="b6783-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="b6783-118">**emplacement** -hello emplacement où se trouve hello ressource.</span><span class="sxs-lookup"><span data-stu-id="b6783-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="b6783-119">**associations** -liste des associations toohello référencé l’objet.</span><span class="sxs-lookup"><span data-stu-id="b6783-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="b6783-120">**nom** -nom de hello de hello référencé des ressources.</span><span class="sxs-lookup"><span data-stu-id="b6783-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="b6783-121">**ID de ressource** -hello resourceId est hello les uri de ressource hello référencé dans l’association de hello.</span><span class="sxs-lookup"><span data-stu-id="b6783-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="b6783-122">**l’associationType** -relation hello entre l’objet de hello enfant et parent de hello fait référence à cette valeur.</span><span class="sxs-lookup"><span data-stu-id="b6783-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="b6783-123">Les valeurs valides sont **Contains** et **Associated**.</span><span class="sxs-lookup"><span data-stu-id="b6783-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6783-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b6783-124">Before you begin</span></span>

<span data-ttu-id="b6783-125">Dans ce scénario, vous utilisez hello `Get-AzureRmNetworkWatcherTopology` informations de topologie d’applet de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="b6783-125">In this scenario, you use hello `Get-AzureRmNetworkWatcherTopology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="b6783-126">Il existe également un article sur la façon de trop[récupérer la topologie du réseau avec l’API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="b6783-126">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="b6783-127">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="b6783-127">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="b6783-128">Scénario</span><span class="sxs-lookup"><span data-stu-id="b6783-128">Scenario</span></span>

<span data-ttu-id="b6783-129">scénario Hello abordée dans cet article récupère hello topologie de réponse pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="b6783-129">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="b6783-130">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="b6783-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="b6783-131">première étape de Hello est instance de l’Observateur réseau tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="b6783-131">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="b6783-132">Hello `$networkWatcher` variable est passée toohello `Get-AzureRmNetworkWatcherTopology` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b6783-132">hello `$networkWatcher` variable is passed toohello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="b6783-133">Récupérer la topologie</span><span class="sxs-lookup"><span data-stu-id="b6783-133">Retrieve topology</span></span>

<span data-ttu-id="b6783-134">Hello `Get-AzureRmNetworkWatcherTopology` applet de commande extrait la topologie hello pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="b6783-134">hello `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves hello topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="b6783-135">Résultats</span><span class="sxs-lookup"><span data-stu-id="b6783-135">Results</span></span>

<span data-ttu-id="b6783-136">Hello résultats retournés ont une propriété de nom « ressources », qui contient le corps de réponse json hello pour hello `Get-AzureRmNetworkWatcherTopology` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="b6783-136">hello results returned have a property name "Resources", which contains hello json response body for hello `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="b6783-137">réponse de Hello contient des ressources de hello dans hello groupe de sécurité réseau et leurs associations (autrement dit, Contains, associée).</span><span class="sxs-lookup"><span data-stu-id="b6783-137">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
Id              : 00000000-0000-0000-0000-000000000000
CreatedDateTime : 2/1/2017 7:52:21 PM
LastModified    : 2/1/2017 7:46:18 PM
Resources       : [
                    {
                      "Name": "testrg-vnet",
                      "Id":
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet/subnets/default"
                        }
                      ]
                    },
                    {
                      "Name": "default",
                      "Id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testr
                  g-vnet/subnets/default",
                      "Location": "westcentralus",
                      "Associations": []
                    },
                    {
                      "Name": "testrg-vnet2",
                      "Id": 
                  "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet2",
                      "Location": "westcentralus",
                      "Associations": [
                        {
                          "AssociationType": "Contains",
                          "Name": "default",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/default"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "GatewaySubnet",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworks/testrg-vnet2/subnets/GatewaySubnet"
                        },
                        {
                          "AssociationType": "Contains",
                          "Name": "gateway2",
                          "ResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNe
                  tworkGateways/gateway2"
                        }
                      ]
                    },
                    ...
                  ]
```

## <a name="next-steps"></a><span data-ttu-id="b6783-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6783-138">Next steps</span></span>

<span data-ttu-id="b6783-139">Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="b6783-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


