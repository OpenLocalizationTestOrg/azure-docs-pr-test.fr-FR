---
title: "topologie de l’Observateur réseau Azure aaaView - Azure CLI 1.0 | Documents Microsoft"
description: "Cet article décrit comment toouse Azure CLI 1.0 tooquery topologie de votre réseau."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 5cd279d7-3ab0-4813-aaa4-6a648bf74e7b
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 30679d6dc74e85bacfc86c63bd1afa873893c772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="view-network-watcher-topology-with-azure-cli-10"></a><span data-ttu-id="2bf14-103">Afficher la topologie Azure Network Watcher avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2bf14-103">View Network Watcher topology with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2bf14-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2bf14-104">PowerShell</span></span>](network-watcher-topology-powershell.md)
> - [<span data-ttu-id="2bf14-105">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2bf14-105">CLI 1.0</span></span>](network-watcher-topology-cli-nodejs.md)
> - [<span data-ttu-id="2bf14-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2bf14-106">CLI 2.0</span></span>](network-watcher-topology-cli.md)
> - [<span data-ttu-id="2bf14-107">API REST</span><span class="sxs-lookup"><span data-stu-id="2bf14-107">REST API</span></span>](network-watcher-topology-rest.md)

<span data-ttu-id="2bf14-108">fonctionnalité de topologie Hello de l’Observateur réseau fournit une représentation visuelle des ressources du réseau hello dans un abonnement.</span><span class="sxs-lookup"><span data-stu-id="2bf14-108">hello Topology feature of Network Watcher provides a visual representation of hello network resources in a subscription.</span></span> <span data-ttu-id="2bf14-109">Dans le portail hello, cette visualisation est présentée tooyou automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2bf14-109">In hello portal, this visualization is presented tooyou automatically.</span></span> <span data-ttu-id="2bf14-110">informations Hello derrière l’affichage de la topologie hello dans le portail de hello peuvent être récupérées via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2bf14-110">hello information behind hello topology view in hello portal can be retrieved through PowerShell.</span></span>
<span data-ttu-id="2bf14-111">Cette fonctionnalité rend les informations de topologie hello plus polyvalente que les données de salutation peuvent être utilisées par les autres toobuild outils out visualisation de hello.</span><span class="sxs-lookup"><span data-stu-id="2bf14-111">This capability makes hello topology information more versatile as hello data can be consumed by other tools toobuild out hello visualization.</span></span>

<span data-ttu-id="2bf14-112">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="2bf14-112">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> 

<span data-ttu-id="2bf14-113">interconnexion de Hello est modélisée sous deux relations.</span><span class="sxs-lookup"><span data-stu-id="2bf14-113">hello interconnection is modeled under two relationships.</span></span>

- <span data-ttu-id="2bf14-114">**Relation d’imbrication** - exemple : le réseau virtuel contient un sous-réseau qui contient une carte réseau</span><span class="sxs-lookup"><span data-stu-id="2bf14-114">**Containment** - Example: VNet contains a Subnet contains a NIC</span></span>
- <span data-ttu-id="2bf14-115">**Associé** - exemple : une carte réseau est associée à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="2bf14-115">**Associated** - Example: NIC is associated with a VM</span></span>

<span data-ttu-id="2bf14-116">Hello Voici les propriétés qui sont retournées lors de l’interrogation hello API REST de topologie.</span><span class="sxs-lookup"><span data-stu-id="2bf14-116">hello following list is properties that are returned when querying hello Topology REST API.</span></span>

* <span data-ttu-id="2bf14-117">**nom** hello - nom de ressource de hello</span><span class="sxs-lookup"><span data-stu-id="2bf14-117">**name** - hello name of hello resource</span></span>
* <span data-ttu-id="2bf14-118">**ID** -hello uri de ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="2bf14-118">**id** - hello uri of hello resource.</span></span>
* <span data-ttu-id="2bf14-119">**emplacement** -hello emplacement où se trouve hello ressource.</span><span class="sxs-lookup"><span data-stu-id="2bf14-119">**location** - hello location where hello resource exists.</span></span>
* <span data-ttu-id="2bf14-120">**associations** -liste des associations toohello référencé l’objet.</span><span class="sxs-lookup"><span data-stu-id="2bf14-120">**associations** - A list of associations toohello referenced object.</span></span>
    * <span data-ttu-id="2bf14-121">**nom** -nom de hello de hello référencé des ressources.</span><span class="sxs-lookup"><span data-stu-id="2bf14-121">**name** - hello name of hello referenced resource.</span></span>
    * <span data-ttu-id="2bf14-122">**ID de ressource** -hello resourceId est hello les uri de ressource hello référencé dans l’association de hello.</span><span class="sxs-lookup"><span data-stu-id="2bf14-122">**resourceId** - hello resourceId is hello uri of hello resource referenced in hello association.</span></span>
    * <span data-ttu-id="2bf14-123">**l’associationType** -relation hello entre l’objet de hello enfant et parent de hello fait référence à cette valeur.</span><span class="sxs-lookup"><span data-stu-id="2bf14-123">**associationType** - This value references hello relationship between hello child object and hello parent.</span></span> <span data-ttu-id="2bf14-124">Les valeurs valides sont **Contains** et **Associated**.</span><span class="sxs-lookup"><span data-stu-id="2bf14-124">Valid values are **Contains** or **Associated**.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2bf14-125">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2bf14-125">Before you begin</span></span>

<span data-ttu-id="2bf14-126">Dans ce scénario, vous utilisez hello `network watcher topology` informations de topologie d’applet de commande tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="2bf14-126">In this scenario, you use hello `network watcher topology` cmdlet tooretrieve hello topology information.</span></span> <span data-ttu-id="2bf14-127">Il existe également un article sur la façon de trop[récupérer la topologie du réseau avec l’API REST](network-watcher-topology-rest.md).</span><span class="sxs-lookup"><span data-stu-id="2bf14-127">There is also an article on how too[retrieve network topology with REST API](network-watcher-topology-rest.md).</span></span>

<span data-ttu-id="2bf14-128">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="2bf14-128">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="2bf14-129">Scénario</span><span class="sxs-lookup"><span data-stu-id="2bf14-129">Scenario</span></span>

<span data-ttu-id="2bf14-130">scénario Hello abordée dans cet article récupère hello topologie de réponse pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="2bf14-130">hello scenario covered in this article retrieves hello topology response for a given resource group.</span></span>

## <a name="retrieve-topology"></a><span data-ttu-id="2bf14-131">Récupérer la topologie</span><span class="sxs-lookup"><span data-stu-id="2bf14-131">Retrieve topology</span></span>

<span data-ttu-id="2bf14-132">Hello `network watcher topology` applet de commande extrait la topologie hello pour un groupe de ressources donné.</span><span class="sxs-lookup"><span data-stu-id="2bf14-132">hello `network watcher topology` cmdlet retrieves hello topology for a given resource group.</span></span> <span data-ttu-id="2bf14-133">Ajouter un argument de hello »--json « oput de hello tooview au format json</span><span class="sxs-lookup"><span data-stu-id="2bf14-133">Add hello argument "--json" tooview hello oput in json format</span></span>

```azurecli
azure network watcher topology -g resourceGroupName -n networkWatcherName -r topologyResourceGroupName --json
```

## <a name="results"></a><span data-ttu-id="2bf14-134">Résultats</span><span class="sxs-lookup"><span data-stu-id="2bf14-134">Results</span></span>

<span data-ttu-id="2bf14-135">Hello résultats retournés ont une propriété de nom « ressources », qui contient le corps de réponse json hello pour hello `network watcher topology` applet de commande.</span><span class="sxs-lookup"><span data-stu-id="2bf14-135">hello results returned have a property name "Resources", which contains hello json response body for hello `network watcher topology` cmdlet.</span></span>  <span data-ttu-id="2bf14-136">réponse de Hello contient des ressources de hello dans hello groupe de sécurité réseau et leurs associations (autrement dit, Contains, associée).</span><span class="sxs-lookup"><span data-stu-id="2bf14-136">hello response contains hello resources in hello Network Security Group and their associations (that is, Contains, Associated).</span></span>

```json
{
  "id": "00000000-0000-0000-0000-000000000000",
  "createdDateTime": "2017-02-17T22:20:59.461Z",
  "lastModified": "2016-12-19T22:23:02.546Z",
  "resources": [
    {
      "name": "testrg-vnet",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet",
      "location": "westcentralus",
      "associations": [
        {
          "name": "default",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
          "associationType": "Contains"
        }
      ]
    },
    {
      "name": "default",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testrg-vnet/subnets/default",
      "location": "westcentralus",
      "associations": []
    },
    {
      "name": "testclient",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Compute/virtualMachines/testclient",
      "location": "westcentralus",
      "associations": [
        {
          "name": "testNic",
          "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/testrg/providers/Microsoft.Network/networkInterfaces/testNic",
          "associationType": "Contains"
        }
      ]
    },
    ...    
  ]
}
```

## <a name="next-steps"></a><span data-ttu-id="2bf14-137">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2bf14-137">Next steps</span></span>

<span data-ttu-id="2bf14-138">En savoir plus sur les règles de sécurité hello qui sont des ressources du réseau tooyour appliqué en vous rendant sur [présentation du mode de groupe de sécurité](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2bf14-138">Learn more about hello security rules that are applied tooyour network resources by visiting [Security group view overview](network-watcher-security-group-view-overview.md)</span></span>
