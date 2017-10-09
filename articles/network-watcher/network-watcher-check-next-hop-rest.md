---
title: "aaaFind tronçon suivant avec Azure réseau observateur du tronçon suivant - REST | Documents Microsoft"
description: "Cet article décrit comment vous pouvez trouver le hello de type de tronçon suivant est et l’adresse ip à l’aide de tronçon suivant hello API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2216c059-45ba-4214-8304-e56769b779a6
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: a2b61b355aae8ae513ebd44837184fbc6cfd668c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="56707-103">Savoir quel type de tronçon suivant hello est à l’aide de capacité de tronçon suivant hello dans l’Observateur réseau de Aure à l’aide des API REST Azure</span><span class="sxs-lookup"><span data-stu-id="56707-103">Find out what hello next hop type is using hello Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="56707-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="56707-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="56707-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56707-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="56707-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="56707-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="56707-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="56707-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="56707-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="56707-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="56707-109">Tronçon suivant est une fonctionnalité de l’Observateur réseau qui offre la possibilité de hello obtenir le type de tronçon suivant hello et l’adresse IP basée sur une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="56707-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="56707-110">Cette fonctionnalité est utile pour déterminer si le trafic en laissant une machine virtuelle traverse une passerelle, internet ou des réseaux virtuels tooget tooits destination.</span><span class="sxs-lookup"><span data-stu-id="56707-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56707-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="56707-111">Before you begin</span></span>

<span data-ttu-id="56707-112">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="56707-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="56707-113">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="56707-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="56707-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="56707-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="56707-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="56707-115">Scenario</span></span>

<span data-ttu-id="56707-116">scénario de Hello abordée dans cet article utilise le saut suivant, une fonctionnalité de l’Observateur réseau qui recherche le type de tronçon suivant hello et une adresse IP pour une ressource.</span><span class="sxs-lookup"><span data-stu-id="56707-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="56707-117">toolearn en savoir plus sur le tronçon suivant, visitez [vue d’ensemble du tronçon suivant](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56707-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="56707-118">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="56707-118">In this scenario, you will:</span></span>

* <span data-ttu-id="56707-119">Récupérer le saut suivant de hello pour un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="56707-119">Retrieve hello next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="56707-120">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="56707-120">Log in with ARMClient</span></span>

<span data-ttu-id="56707-121">Ouvrez une session dans tooarmclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="56707-121">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="56707-122">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="56707-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="56707-123">Exécutez hello suivant script tooreturn une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="56707-123">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="56707-124">Ces informations sont nécessaires pour l’exécution de la fonctionnalité Tronçon suivant.</span><span class="sxs-lookup"><span data-stu-id="56707-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="56707-125">Hello suivant code doit valeurs pour hello suivant variables :</span><span class="sxs-lookup"><span data-stu-id="56707-125">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="56707-126">**ID d’abonnement** -hello toouse de Id d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="56707-126">**subscriptionId** - hello subscription Id toouse.</span></span>
- <span data-ttu-id="56707-127">**resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="56707-127">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="56707-128">À partir de la sortie suivante de hello, id de hello de machine virtuelle de hello est utilisée dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="56707-128">From hello following output, hello id of hello virtual machine is used in hello following example:</span></span>

```json
...
,
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="get-next-hop"></a><span data-ttu-id="56707-129">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="56707-129">Get Next Hop</span></span>

<span data-ttu-id="56707-130">Une fois créé, l’en-tête d’autorisation hello saut suivant de hello à partir d’un ordinateur virtuel peut être récupéré.</span><span class="sxs-lookup"><span data-stu-id="56707-130">Once hello authorization header is created, hello next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="56707-131">Hello valeurs suivantes doivent être remplacées pour hello code exemple toowork.</span><span class="sxs-lookup"><span data-stu-id="56707-131">hello following values must be replaced for hello code example toowork.</span></span>

> [!Important]
> <span data-ttu-id="56707-132">Pour l’API REST de l’Observateur réseau appels hello nom de groupe de ressources dans la demande de hello QU'URI est le groupe de ressources hello contient hello Observateur réseau, pas les ressources hello vous effectuez des actions de diagnostic hello sur.</span><span class="sxs-lookup"><span data-stu-id="56707-132">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

```powershell
$sourceIP = "10.0.0.4"
$destinationIP = "8.8.8.8"
$resourceGroupName = <resource group name>
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'sourceIpAddress': '${sourceIP}',
    'destinationIpAddress': '${destinationIP}',
    'targetNicResourceId' : '${targetNic}'
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/nextHop?api-version=2016-12-01" $requestBody
```

> [!NOTE]
> <span data-ttu-id="56707-133">Tronçon suivant requiert que les ressources d’ordinateur virtuel hello est allouée toorun.</span><span class="sxs-lookup"><span data-stu-id="56707-133">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="results"></a><span data-ttu-id="56707-134">Résultats</span><span class="sxs-lookup"><span data-stu-id="56707-134">Results</span></span>

<span data-ttu-id="56707-135">Bonjour extrait de code suivant est un exemple de sortie hello reçu.</span><span class="sxs-lookup"><span data-stu-id="56707-135">hello following snippet is an example of hello output received.</span></span> <span data-ttu-id="56707-136">les résultats de Hello contiennent hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="56707-136">hello results contain hello following values:</span></span>

* <span data-ttu-id="56707-137">**type de tronçon suivant** -cette valeur est une des valeurs suivantes de hello : Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway ou None.</span><span class="sxs-lookup"><span data-stu-id="56707-137">**nextHopType** - This value is one of hello following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="56707-138">**nextHopIpAddress** -hello l’adresse IP du tronçon suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="56707-138">**nextHopIpAddress** - hello IP address of hello next hop.</span></span>
* <span data-ttu-id="56707-139">**routeTableId** - hello valeur est soit un uri pour la table d’itinéraires hello associé hello itinéraire, ou si non défini par l’utilisateur itinéraire valeur hello défini de *système itinéraire* est retourné.</span><span class="sxs-lookup"><span data-stu-id="56707-139">**routeTableId** - hello value is either a uri for hello route table associated with hello route, or if no user-defined route is defined hello value of *System Route* is returned.</span></span>

<span data-ttu-id="56707-140">Hello Voici les résultats hello au format json.</span><span class="sxs-lookup"><span data-stu-id="56707-140">hello following are hello results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="56707-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56707-141">Next steps</span></span>

<span data-ttu-id="56707-142">Une fois que vous avez été en mesure de toofind out saut suivant de hello pour un ordinateur virtuel, vous pouvez afficher la sécurité hello de ressources de votre réseau en vous rendant sur [vue d’ensemble de la vue de la sécurité](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="56707-142">Once you have been able toofind out hello next hop for a virtual machine, you can view hello security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














