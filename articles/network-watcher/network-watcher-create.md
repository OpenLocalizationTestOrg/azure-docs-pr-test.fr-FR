---
title: "Créer une instance d’Azure Network Watcher | Microsoft Docs"
description: "Cette page fournit la procédure nécessaire pour créer une instance de Network Watcher à l’aide du portail et de l’API REST Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: b1314119-0b87-4f4d-b44c-2c4d0547fb76
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2aeaffdd5ab552e18677cbd1a24a748dd14bf172
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="cfffd-103">Créer une instance d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="cfffd-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="cfffd-104">Network Watcher est un service régional qui vous permet de surveiller et de diagnostiquer l’état au niveau d’un scénario réseau dans, vers et depuis Azure.</span><span class="sxs-lookup"><span data-stu-id="cfffd-104">Network Watcher is a regional service that enables you to monitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="cfffd-105">La surveillance au niveau des scénarios vous permet de diagnostiquer les problèmes avec une vue de bout en bout du réseau.</span><span class="sxs-lookup"><span data-stu-id="cfffd-105">Scenario level monitoring enables you to diagnose problems at an end to end network level view.</span></span> <span data-ttu-id="cfffd-106">Les outils de visualisation et de diagnostic réseau disponibles avec Network Watcher vous aident à comprendre, diagnostiquer et obtenir des informations sur votre réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cfffd-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights to your network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="cfffd-107">Comme Network Watcher ne prend actuellement en charge que l’interface CLI 1.0, les instructions fournies pour créer une nouvelle instance de Network Watcher s’appliquent à cette version.</span><span class="sxs-lookup"><span data-stu-id="cfffd-107">As Network Watcher currently only supports CLI 1.0, the instructions to create a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-the-portal"></a><span data-ttu-id="cfffd-108">Créer un Network Watcher dans le portail</span><span class="sxs-lookup"><span data-stu-id="cfffd-108">Create a Network Watcher in the portal</span></span>

<span data-ttu-id="cfffd-109">Accédez à **Plus de services** > **Mise en réseau** > **Network Watcher**.</span><span class="sxs-lookup"><span data-stu-id="cfffd-109">Navigate to **More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="cfffd-110">Vous pouvez sélectionner tous les abonnements pour lesquels vous souhaitez activer Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="cfffd-110">You can select all the subscriptions you want to enable Network Watcher for.</span></span> <span data-ttu-id="cfffd-111">Cette action crée un Network Watcher dans chaque région disponible.</span><span class="sxs-lookup"><span data-stu-id="cfffd-111">This action creates a Network Watcher in every region that is available.</span></span>

![créer un Network Watcher][1]

<span data-ttu-id="cfffd-113">Lorsque Network Watcher est activé à l’aide du portail, le nom de l’instance de Network Watcher est automatiquement défini comme NetworkWatcher_nom_région, où nom_région correspond à la région Azure dans laquelle l’instance a été activée.</span><span class="sxs-lookup"><span data-stu-id="cfffd-113">When you enable Network Watcher using the Portal, the name of the Network Watcher instance will automatically be set to NetworkWatcher_region_name where region_name corresponds to the Azure Region where the instance was enabled.</span></span>  <span data-ttu-id="cfffd-114">Par exemple, une instance de Network Watcher activée dans la région États-Unis Centre-Ouest sera nommée NetworkWatcher_westcentralus.</span><span class="sxs-lookup"><span data-stu-id="cfffd-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="cfffd-115">En outre, l’instance de Network Watcher sera automatiquement ajoutée à un groupe de ressources nommé NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="cfffd-115">Additionally, the Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="cfffd-116">Il sera créé s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="cfffd-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="cfffd-117">Si vous souhaitez personnaliser le nom d’une instance de Network Watcher et le groupe de ressources dans lequel elle est placée, vous pouvez utiliser les méthodes PowerShell, API REST et ARMClient décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cfffd-117">If you wish to customize the name of a Network Watcher instance and the Resource Group it's placed into, you can use Powershell, the REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="cfffd-118">Dans chacune des options, le groupe de ressources doit déjà exister pour que vous puissiez y placer l’instance de Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="cfffd-118">In each option, the Resource Group must exist before you place the Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="cfffd-119">Créer un Network Watcher avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="cfffd-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="cfffd-120">Pour créer une instance de Network Watcher, exécutez l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="cfffd-120">To create an instance of Network Watcher, run the following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-the-rest-api"></a><span data-ttu-id="cfffd-121">Créer un Network Watcher avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="cfffd-121">Create a Network Watcher with the REST API</span></span>

<span data-ttu-id="cfffd-122">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cfffd-122">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="cfffd-123">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="cfffd-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="cfffd-124">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="cfffd-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-the-network-watcher"></a><span data-ttu-id="cfffd-125">Créer le Network Watcher</span><span class="sxs-lookup"><span data-stu-id="cfffd-125">Create the network watcher</span></span>

```powershell
$subscriptionId = '<subscription id>'
$networkWatcherName = '<name of network watcher>'
$resourceGroupName = '<resource group name>'
$apiversion = "2016-09-01"
$requestBody = @"
{
'location': 'West Central US'
}
"@

armclient put "https://management.azure.com/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}?api-version=${api-version}" $requestBody
```

## <a name="next-steps"></a><span data-ttu-id="cfffd-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cfffd-126">Next steps</span></span>

<span data-ttu-id="cfffd-127">Maintenant que vous avez une instance de Network Watcher, découvrez les fonctionnalités disponibles :</span><span class="sxs-lookup"><span data-stu-id="cfffd-127">Now that you have an instance of Network Watcher, learn about the features available:</span></span>

* [<span data-ttu-id="cfffd-128">Topologie</span><span class="sxs-lookup"><span data-stu-id="cfffd-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="cfffd-129">Capture de paquets</span><span class="sxs-lookup"><span data-stu-id="cfffd-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="cfffd-130">Vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="cfffd-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="cfffd-131">Tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="cfffd-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="cfffd-132">Affichage des groupes de sécurité</span><span class="sxs-lookup"><span data-stu-id="cfffd-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="cfffd-133">Journalisation des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="cfffd-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="cfffd-134">Résolution des problèmes de passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="cfffd-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="cfffd-135">Après la création d’une instance Network Watcher, lisez l’article [Créer une capture de paquets déclenchée par une alerte](network-watcher-alert-triggered-packet-capture.md) pour configurer la capture de paquets.</span><span class="sxs-lookup"><span data-stu-id="cfffd-135">Once a Network Watcher instance has been created, package capture can be configured by following the article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











