---
title: "Rechercher le tronçon suivant avec la fonction Tronçon suivant Azure Network Watcher - REST | Microsoft Docs"
description: "Cet article explique comment rechercher le type de tronçon suivant et l’adresse IP à l’aide de la fonction Tronçon suivant par le biais de l’API REST"
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
ms.openlocfilehash: 644713d365191bf5e51517d0cc565efbc2abc144
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-aure-network-watcher-using-azure-rest-api"></a><span data-ttu-id="df357-103">Découvrez le type de tronçon suivant grâce à la fonction Tronçon suivant Azure Network Watcher à l’aide de l’API REST</span><span class="sxs-lookup"><span data-stu-id="df357-103">Find out what the next hop type is using the Next Hop capability in Aure Network Watcher using Azure REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="df357-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="df357-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="df357-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="df357-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="df357-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="df357-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="df357-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="df357-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="df357-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="df357-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="df357-109">Tronçon suivant est une fonctionnalité de Network Watcher qui permet d’obtenir le type de tronçon suivant et l’adresse IP à partir d’une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="df357-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="df357-110">Cette fonctionnalité est utile pour déterminer si le trafic sortant d’une machine virtuelle passe par une passerelle, Internet ou des réseaux virtuels pour atteindre sa destination.</span><span class="sxs-lookup"><span data-stu-id="df357-110">This capability is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="df357-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="df357-111">Before you begin</span></span>

<span data-ttu-id="df357-112">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="df357-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="df357-113">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="df357-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="df357-114">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="df357-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="df357-115">Scénario</span><span class="sxs-lookup"><span data-stu-id="df357-115">Scenario</span></span>

<span data-ttu-id="df357-116">Le scénario décrit dans cet article utilise Tronçon suivant, une fonctionnalité de Network Watcher qui détecte le type de tronçon suivant et l’adresse IP d’une ressource.</span><span class="sxs-lookup"><span data-stu-id="df357-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="df357-117">Pour en savoir plus sur Tronçon suivant, consultez [Next Hop Overview (Vue d’ensemble de la fonctionnalité Tronçon suivant)](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="df357-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

<span data-ttu-id="df357-118">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="df357-118">In this scenario, you will:</span></span>

* <span data-ttu-id="df357-119">Récupérer le tronçon suivant pour une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="df357-119">Retrieve the next hop for a virtual machine.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="df357-120">Vous connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="df357-120">Log in with ARMClient</span></span>

<span data-ttu-id="df357-121">Vous connecter à armclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="df357-121">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="df357-122">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="df357-122">Retrieve a virtual machine</span></span>

<span data-ttu-id="df357-123">Exécutez le script suivant pour renvoyer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="df357-123">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="df357-124">Ces informations sont nécessaires pour l’exécution de la fonctionnalité Tronçon suivant.</span><span class="sxs-lookup"><span data-stu-id="df357-124">This information is needed for running next hop.</span></span>

<span data-ttu-id="df357-125">Les codes suivants ont besoin de valeurs pour les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="df357-125">The following code needs values for the following variables:</span></span>

- <span data-ttu-id="df357-126">**subscriptionId** : l’ID d’abonnement à utiliser.</span><span class="sxs-lookup"><span data-stu-id="df357-126">**subscriptionId** - The subscription Id to use.</span></span>
- <span data-ttu-id="df357-127">**resourceGroupName** : le nom d’un groupe de ressources qui contient les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="df357-127">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="df357-128">À partir de la sortie suivante, l’ID de la machine virtuelle est utilisé dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="df357-128">From the following output, the id of the virtual machine is used in the following example:</span></span>

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

## <a name="get-next-hop"></a><span data-ttu-id="df357-129">Obtenir le tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="df357-129">Get Next Hop</span></span>

<span data-ttu-id="df357-130">Une fois que l’en-tête d’autorisation est créé, le tronçon suivant d’une machine virtuelle peut être récupéré.</span><span class="sxs-lookup"><span data-stu-id="df357-130">Once the authorization header is created, the next hop from a virtual machine can be retrieved.</span></span> <span data-ttu-id="df357-131">Les valeurs suivantes doivent être remplacées pour que l’exemple de code fonctionne.</span><span class="sxs-lookup"><span data-stu-id="df357-131">The following values must be replaced for the code example to work.</span></span>

> [!Important]
> <span data-ttu-id="df357-132">Pour les appels de l’API REST de Network Watcher, le nom du groupe de ressources dans l’URI de requête correspond au groupe de ressources qui contient Network Watcher, mais pas les ressources sur lesquelles vous exécutez les actions de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="df357-132">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

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
> <span data-ttu-id="df357-133">L’exécution de la fonctionnalité Tronçon suivant nécessite l’allocation de la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="df357-133">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="results"></a><span data-ttu-id="df357-134">Résultats</span><span class="sxs-lookup"><span data-stu-id="df357-134">Results</span></span>

<span data-ttu-id="df357-135">L’extrait de code suivant est un exemple de sortie reçue.</span><span class="sxs-lookup"><span data-stu-id="df357-135">The following snippet is an example of the output received.</span></span> <span data-ttu-id="df357-136">Les résultats contiennent les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="df357-136">The results contain the following values:</span></span>

* <span data-ttu-id="df357-137">**nextHopType** : cette valeur est l’une des valeurs suivantes : Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway ou None.</span><span class="sxs-lookup"><span data-stu-id="df357-137">**nextHopType** - This value is one of the following values: Internet, VirtualAppliance, VirtualNetworkGateway, VnetLocal, HyperNetGateway, or None.</span></span>
* <span data-ttu-id="df357-138">**nextHopIpAddress** : l’adresse IP du tronçon suivant.</span><span class="sxs-lookup"><span data-stu-id="df357-138">**nextHopIpAddress** - The IP address of the next hop.</span></span>
* <span data-ttu-id="df357-139">**routeTableId** : la valeur est un URI pour la table de routage associée à l’itinéraire ou, aucun itinéraire défini par l’utilisateur n’est défini, la valeur d’*itinéraire système* est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="df357-139">**routeTableId** - The value is either a uri for the route table associated with the route, or if no user-defined route is defined the value of *System Route* is returned.</span></span>

<span data-ttu-id="df357-140">Voici les résultats au format json.</span><span class="sxs-lookup"><span data-stu-id="df357-140">The following are the results in json format.</span></span>

```json
{
  "nextHopType": "Internet",
  "routeTableId": "System Route"
}
```

## <a name="next-steps"></a><span data-ttu-id="df357-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="df357-141">Next steps</span></span>

<span data-ttu-id="df357-142">Lorsque vous avez trouvé le tronçon suivant pour une machine virtuelle, vous pouvez afficher la sécurité de vos ressources réseau en vous rendant dans la [vue d’ensemble de la vue de sécurité](network-watcher-security-group-view-overview.md)</span><span class="sxs-lookup"><span data-stu-id="df357-142">Once you have been able to find out the next hop for a virtual machine, you can view the security of your network resources by visiting [Security View overview](network-watcher-security-group-view-overview.md)</span></span>














