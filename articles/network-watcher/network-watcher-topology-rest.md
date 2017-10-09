---
title: "topologie de l’Observateur réseau Azure aaaView - API REST | Documents Microsoft"
description: "Cet article décrit comment toouse REST API tooquery topologie de votre réseau."
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
ms.openlocfilehash: 39292025bcd561f007c9e31271b1389be48ea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-rest-api"></a><span data-ttu-id="31514-103">Afficher la topologie Azure Network Watcher par le biais de l’API REST</span><span class="sxs-lookup"><span data-stu-id="31514-103">View Network Watcher topology with REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="31514-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="31514-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="31514-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="31514-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="31514-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="31514-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="31514-107">API REST</span><span class="sxs-lookup"><span data-stu-id="31514-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="31514-108">fonctionnalité de topologie Hello de l’Observateur réseau fournit une représentation visuelle des ressources du réseau hello dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="31514-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="31514-109">Dans le portail hello, cette visualisation est présentée tooyou automatiquement.</span><span class="sxs-lookup"><span data-stu-id="31514-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="31514-110">informations Hello derrière l’affichage de la topologie hello dans le portail de hello peuvent être récupérées via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31514-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="31514-111">Cette fonctionnalité rend les informations de topologie hello plus polyvalente que les données de salutation peuvent être utilisées par les autres toobuild outils out visualisation de hello.</span><span class="sxs-lookup"><span data-stu-id="31514-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="31514-112">interconnexion de Hello est modélisée sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="31514-112">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="31514-113">**Relation d’imbrication** - exemple : le réseau virtuel contient un sous-réseau qui contient une carte réseau</span><span class="sxs-lookup"><span data-stu-id="31514-113">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="31514-114">**Associé** - exemple : une carte réseau est associée à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="31514-114">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="31514-115">Hello Voici les propriétés qui sont retournées lors de l’interrogation hello API REST de topologie.</span><span class="sxs-lookup"><span data-stu-id="31514-115">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="31514-116">**nom** hello - nom de ressource de hello</span><span class="sxs-lookup"><span data-stu-id="31514-116">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="31514-117">**ID** -hello uri de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="31514-117">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="31514-118">**emplacement** -hello emplacement où se trouve hello ressource.</span><span class="sxs-lookup"><span data-stu-id="31514-118">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="31514-119">**associations** -liste des associations toohello référencé l’objet.</span><span class="sxs-lookup"><span data-stu-id="31514-119">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="31514-120">**nom** -nom de hello de hello référencé des ressources.</span><span class="sxs-lookup"><span data-stu-id="31514-120">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="31514-121">**ID de ressource** -hello resourceId est hello les uri de ressource hello référencé dans l’association de hello.</span><span class="sxs-lookup"><span data-stu-id="31514-121">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="31514-122">**l’associationType** -relation hello entre l’objet de hello enfant et parent de hello fait référence à cette valeur.</span><span class="sxs-lookup"><span data-stu-id="31514-122">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="31514-123">Les valeurs valides sont **Contains** et **Associated**.</span><span class="sxs-lookup"><span data-stu-id="31514-123">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="31514-124">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="31514-124">Before you begin</span></span>

<span data-ttu-id="31514-125">Ce scénario, vous permet de récupérer les informations de topologie hello.</span><span class="sxs-lookup"><span data-stu-id="31514-125">In this scenario, you retrieve hello topology information.</span></span> <span data-ttu-id="31514-126">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="31514-126">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="31514-127">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="31514-127">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="31514-128">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="31514-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="31514-129">Scénario</span><span class="sxs-lookup"><span data-stu-id="31514-129">Scenario</span></span>

<span data-ttu-id="31514-130">scénario Hello abordée dans cet article récupère hello topologie de réponse pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="31514-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="31514-131">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="31514-131">Log in with ARMClient</span></span>

<span data-ttu-id="31514-132">Ouvrez une session dans tooarmclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="31514-132">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-topology"></a><span data-ttu-id="31514-133">Récupérer la topologie</span><span class="sxs-lookup"><span data-stu-id="31514-133">Retrieve topology</span></span>

<span data-ttu-id="31514-134">Hello, l’exemple suivant demande la topologie de hello hello API REST.</span><span class="sxs-lookup"><span data-stu-id="31514-134">hello following example requests hello topology from hello REST API.</span></span>  <span data-ttu-id="31514-135">exemple de Hello est paramétrable tooallow pour une grande souplesse pour la création d’un exemple.</span><span class="sxs-lookup"><span data-stu-id="31514-135">hello example is parameterized tooallow for flexibility in creating an example.</span></span>  <span data-ttu-id="31514-136">Remplacez toutes les valeurs avec \< \> qui les entoure.</span><span class="sxs-lookup"><span data-stu-id="31514-136">Replace all values with \< \> surrounding them.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>" # Resource group name toorun topology on
$NWresourceGroupName = "<resource group name>" # Network Watcher resource group name
$networkWatcherName = "<network watcher name>"
$requestBody = @"
{
    'targetResourceGroupName': '${resourceGroupName}'
}
"@

armclient POST "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/topology?api-version=2016-07-01" $requestBody
```

<span data-ttu-id="31514-137">Hello suivant la réponse est un exemple d’une réponse raccourcie qui est retourné lorsque récupérer la topologie pour un groupe de ressources :</span><span class="sxs-lookup"><span data-stu-id="31514-137">hello following response is an example of a shortened response that is returned when retrieve topology for a resourcegroup:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="31514-138">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="31514-138">Next steps</span></span>

<span data-ttu-id="31514-139">Découvrez comment toovisualize votre flux de groupe de sécurité réseau se connecte à Power BI en vous rendant sur [NSG de visualiser les flux de journaux avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="31514-139">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

