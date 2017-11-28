---
title: Afficher la topologie Azure Network Watcher - API REST | Microsoft Docs
description: "Cet article explique comment utiliser l’API REST pour interroger la topologie de votre réseau."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: de9af643-aea1-4c4c-89c5-21f1bf334c06
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 568f3060da372f4a08cec342e04359172522cb69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="4ebe2-103">Afficher la topologie Azure Network Watcher par le biais de l’API REST</span><span class="sxs-lookup"><span data-stu-id="4ebe2-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="4ebe2-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ebe2-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="4ebe2-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="4ebe2-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="4ebe2-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4ebe2-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="4ebe2-107">API REST</span><span class="sxs-lookup"><span data-stu-id="4ebe2-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="4ebe2-108">La fonctionnalité Topologie de Network Watcher fournit une représentation visuelle des ressources réseau dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-108">The Topology feature of Network Watcher provides a visual representation of the network resources in a subscription.</span></span> <span data-ttu-id="4ebe2-109">Dans le portail, cette visualisation vous est présentée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-109">In the portal, this visualization is presented to you automatically.</span></span> <span data-ttu-id="4ebe2-110">Les informations relatives à la vue Topologie du portail peuvent être récupérées par le biais de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-110">The information behind the topology view in the portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="4ebe2-111">Cette fonctionnalité rend les informations de topologie plus polyvalentes, car les données peuvent être utilisées par d’autres outils pour générer la visualisation.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-111">This capability makes the topology information more versatile as the data can be consumed by other tools to build out the visualization.</span></span>

<span data-ttu-id="4ebe2-112">L’interconnexion est modélisée sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-112">The interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="4ebe2-113">**Relation d’imbrication** - exemple : le réseau virtuel contient un sous-réseau qui contient une carte réseau</span><span class="sxs-lookup"><span data-stu-id="4ebe2-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="4ebe2-114">**Associé** - exemple : une carte réseau est associée à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="4ebe2-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="4ebe2-115">La liste suivante répertorie les propriétés renvoyées lors de l’interrogation de l’API REST Topologie.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-115">The following list is properties that are returned when querying the Topology REST API.</span></span>

* <span data-ttu-id="4ebe2-116">**name** : nom du groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="4ebe2-116">**name** - The name of the resource</span></span>
* <span data-ttu-id="4ebe2-117">**id** : URI de la ressource.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-117">**id** - The uri of the resource.</span></span>
* <span data-ttu-id="4ebe2-118">**location** : emplacement de la ressource.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-118">**location** - The location where the resource exists.</span></span>
* <span data-ttu-id="4ebe2-119">**associations** : liste des associations réalisées vis-à-vis de l’objet référencé.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-119">**associations** - A list of associations to the referenced object.</span></span>
    * <span data-ttu-id="4ebe2-120">**name** : nom de la ressource référencée.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-120">**name** - The name of the referenced resource.</span></span>
    * <span data-ttu-id="4ebe2-121">**resourceId** : URI de la ressource référencée dans l’association.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-121">**resourceId** - The resourceId is the uri of the resource referenced in the association.</span></span>
    * <span data-ttu-id="4ebe2-122">**associationType** : cette valeur fait référence à la relation entre l’objet enfant et le parent.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-122">**associationType** - This value references the relationship between the child object and the parent.</span></span> <span data-ttu-id="4ebe2-123">Les valeurs valides sont **Contains** et **Associated**.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4ebe2-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4ebe2-124">Before you begin</span></span>

<span data-ttu-id="4ebe2-125">Dans ce scénario, vous récupérez les informations de topologie.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-125">In this scenario, you retrieve the topology information.</span></span> <span data-ttu-id="4ebe2-126">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-126">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="4ebe2-127">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="4ebe2-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="4ebe2-128">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-128">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="4ebe2-129">Scénario</span><span class="sxs-lookup"><span data-stu-id="4ebe2-129">Scenario</span></span>

<span data-ttu-id="4ebe2-130">Le scénario décrit dans cet article récupère la réponse de la topologie pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-130">The scenario covered in this article retrieves the topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="4ebe2-131">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="4ebe2-131">Log in with ARMClient</span></span>

<span data-ttu-id="4ebe2-132">Connectez-vous à armclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-132">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="4ebe2-133">Récupérer la topologie</span><span class="sxs-lookup"><span data-stu-id="4ebe2-133">Retrieve topology</span></span>

<span data-ttu-id="4ebe2-134">L’exemple suivant demande la topologie à partir de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-134">The following example requests the topology from the REST API.</span></span>  <span data-ttu-id="4ebe2-135">L’exemple est paramétré pour permettre une certaine flexibilité dans la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-135">The example is parameterized to allow for flexibility in creating an example.</span></span>  <span data-ttu-id="4ebe2-136">Remplacez toutes les valeurs avec \< \> qui les entoure.</span><span class="sxs-lookup"><span data-stu-id="4ebe2-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name to run topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="4ebe2-137">La réponse suivante est un exemple de réponse abrégée qui est renvoyée lors de la récupération de la topologie pour un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="4ebe2-137">The following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

```json
{
  "id": "ecd6c860-9cf5-411a-bdba-512f8df7799f",
  "createdDateTime": "2017-01-18T04:13:07.1974591Z",
  "lastModified": "2017-01-17T22:11:52.3527348Z",
  "resources": [
    {
      "name": "virtualNetwork1",
      "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/{virtualNetworkName}",
      "location": "westcentralus",
      "associations": [
        {
          "name": "{subnetName}",
          "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/virtualNetworks/(virtualNetworkName)/subnets
/{subnetName}",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "webtestnsg-wjplxls65qcto",
      "resourceId": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}
s65qcto",
      "associationType": "Associated"
    },
    ...
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="4ebe2-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ebe2-138">Next steps</span></span>

<span data-ttu-id="4ebe2-139">Découvrez comment visualiser vos journaux de flux NSG avec Power BI en consultant la page [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md) (Visualiser les journaux de flux NSG avec Power BI)</span><span class="sxs-lookup"><span data-stu-id="4ebe2-139">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

