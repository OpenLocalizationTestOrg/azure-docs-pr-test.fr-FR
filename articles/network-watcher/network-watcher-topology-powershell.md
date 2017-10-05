---
title: Afficher la topologie Azure Network Watcher - PowerShell | Microsoft Docs
description: "Cet article explique comment utiliser PowerShell pour interroger la topologie de votre réseau."
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
ms.openlocfilehash: 40e01a7a6a2ea6127ab725f04649cec47b9d9422
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-powershell"></a><span data-ttu-id="21435-103">Afficher la topologie Network Watcher par le biais de PowerShell</span><span class="sxs-lookup"><span data-stu-id="21435-103">View Network Watcher topology with PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="21435-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="21435-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="21435-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="21435-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="21435-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="21435-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="21435-107">API REST</span><span class="sxs-lookup"><span data-stu-id="21435-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="21435-108">La fonctionnalité Topologie de Network Watcher fournit une représentation visuelle des ressources réseau dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="21435-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="21435-109">Dans le portail, cette visualisation vous est présentée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="21435-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="21435-110">Les informations relatives à la vue Topologie du portail peuvent être récupérées par le biais de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="21435-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="21435-111">Cette fonctionnalité rend les informations de topologie plus polyvalentes, car les données peuvent être utilisées par d’autres outils pour générer la visualisation.</span><span class="sxs-lookup"><span data-stu-id="21435-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="21435-112">L’interconnexion est modélisée sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="21435-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="21435-113">**Relation d’imbrication** - exemple : le réseau virtuel contient un sous-réseau qui contient une carte réseau</span><span class="sxs-lookup"><span data-stu-id="21435-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="21435-114">**Associé** - exemple : une carte réseau est associée à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="21435-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="21435-115">La liste suivante répertorie les propriétés renvoyées lors de l’interrogation de l’API REST Topologie.</span><span class="sxs-lookup"><span data-stu-id="21435-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="21435-116">**name** : nom du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="21435-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="21435-117">**id** : URI de la ressource.</span><span class="sxs-lookup"><span data-stu-id="21435-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="21435-118">**location** : emplacement de la ressource.</span><span class="sxs-lookup"><span data-stu-id="21435-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="21435-119">**associations** : liste des associations réalisées vis-à-vis de l’objet référencé.</span><span class="sxs-lookup"><span data-stu-id="21435-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="21435-120">**name** : nom de la ressource référencée.</span><span class="sxs-lookup"><span data-stu-id="21435-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="21435-121">**resourceId** : URI de la ressource référencée dans l’association.</span><span class="sxs-lookup"><span data-stu-id="21435-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="21435-122">**associationType** : cette valeur fait référence à la relation entre l’objet enfant et le parent.</span><span class="sxs-lookup"><span data-stu-id="21435-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="21435-123">Les valeurs valides sont **Contains** et **Associated**.</span><span class="sxs-lookup"><span data-stu-id="21435-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="21435-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="21435-124">Before you begin</span></span>

<span data-ttu-id="21435-125">Dans ce scénario, vous utilisez l’applet de commande `Get-AzureRmNetworkWatcherTopology` pour récupérer les informations de topologie.</span><span class="sxs-lookup"><span data-stu-id="21435-125">In this scenario, you use the `Get-AzureRmNetworkWatcherTopology` cmdlet to retrieve the topology information.</span></span> <span data-ttu-id="21435-126">Un article explique aussi comment [récupérer la topologie du réseau avec l’API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="21435-126">There is also an article on how to [retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="21435-127">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="21435-127">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="21435-128">Scénario</span><span class="sxs-lookup"><span data-stu-id="21435-128">Scenario</span></span>

<span data-ttu-id="21435-129">Le scénario décrit dans cet article récupère la réponse de la topologie pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="21435-129">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="21435-130">Récupérer Network Watcher</span><span class="sxs-lookup"><span data-stu-id="21435-130">Retrieve Network Watcher</span></span>

<span data-ttu-id="21435-131">La première étape consiste à récupérer l’instance de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="21435-131">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="21435-132">La variable `$networkWatcher` est transmise à l’applet de commande `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="21435-132">The `$networkWatcher` variable is passed to the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" }
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName
```

## <a name="retrieve-topology"></a><span data-ttu-id="21435-133">Récupérer la topologie</span><span class="sxs-lookup"><span data-stu-id="21435-133">Retrieve topology</span></span>

<span data-ttu-id="21435-134">L’applet de commande `Get-AzureRmNetworkWatcherTopology` récupère la topologie pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="21435-134">The `Get-AzureRmNetworkWatcherTopology` cmdlet retrieves the topology for a given resource group.</span></span>

```powershell
Get-AzureRmNetworkWatcherTopology -NetworkWatcher $networkWatcher -TargetResourceGroupName testrg
```

## <a name="results"></a><span data-ttu-id="21435-135">Résultats</span><span class="sxs-lookup"><span data-stu-id="21435-135">Results</span></span>

<span data-ttu-id="21435-136">Les résultats renvoyés affichent une propriété nommée « Resources », qui contient le corps de réponse json pour l’applet de commande `Get-AzureRmNetworkWatcherTopology`.</span><span class="sxs-lookup"><span data-stu-id="21435-136">The results returned have a property name "Resources", which contains the json response body for the `Get-AzureRmNetworkWatcherTopology` cmdlet.</span></span>  <span data-ttu-id="21435-137">La réponse contient les ressources du groupe de sécurité réseau et leurs associations (autrement dit, Contains et Associated).</span><span class="sxs-lookup"><span data-stu-id="21435-137">The response contains the resources in the Network Security Group and their associations (that is, Contains, Associated).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="21435-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="21435-138">Next steps</span></span>

<span data-ttu-id="21435-139">Découvrez comment visualiser vos journaux de flux NSG avec Power BI en consultant la page [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualiser les journaux de flux NSG avec Power BI)</span><span class="sxs-lookup"><span data-stu-id="21435-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>


