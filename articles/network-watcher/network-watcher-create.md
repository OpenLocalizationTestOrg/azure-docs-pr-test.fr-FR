---
title: "aaaCreate une instance de l’Observateur réseau Azure | Documents Microsoft"
description: "Cette page fournit hello étapes toocreate une instance de l’Observateur réseau à l’aide du portail de hello et l’API REST Azure"
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
ms.openlocfilehash: 90d4f90c9709a80e4b27863e79e5b6e16de145c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-network-watcher-instance"></a><span data-ttu-id="7892f-103">Créer une instance d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="7892f-103">Create an Azure Network Watcher instance</span></span>

<span data-ttu-id="7892f-104">Observateur réseau est un service régional qui permet de vous toomonitor et diagnostiquer des conditions à un niveau de scénario réseau, vers et depuis Azure.</span><span class="sxs-lookup"><span data-stu-id="7892f-104">Network Watcher is a regional service that enables you toomonitor and diagnose conditions at a network scenario level in, to, and from Azure.</span></span> <span data-ttu-id="7892f-105">Surveillance au niveau du scénario vous permet de problèmes toodiagnose à une vue au niveau du réseau tooend fin.</span><span class="sxs-lookup"><span data-stu-id="7892f-105">Scenario level monitoring enables you toodiagnose problems at an end tooend network level view.</span></span> <span data-ttu-id="7892f-106">Diagnostic de réseau et les outils de visualisation disponibles avec l’Observateur réseau vous aider à comprendre, de diagnostiquer et de mieux réseau de tooyour insights dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7892f-106">Network diagnostic and visualization tools available with Network Watcher help you understand, diagnose, and gain insights tooyour network in Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="7892f-107">Comme l’Observateur réseau prend actuellement en charge uniquement les CLI 1.0, hello instructions toocreate une nouvelle instance de l’Observateur réseau est fournie pour CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="7892f-107">As Network Watcher currently only supports CLI 1.0, hello instructions toocreate a new Network Watcher instance is provided for CLI 1.0.</span></span>

## <a name="create-a-network-watcher-in-hello-portal"></a><span data-ttu-id="7892f-108">Créer un observateur réseau dans le portail de hello</span><span class="sxs-lookup"><span data-stu-id="7892f-108">Create a Network Watcher in hello portal</span></span>

<span data-ttu-id="7892f-109">Accédez trop**plus Services** > **réseau** > **Observateur réseau**.</span><span class="sxs-lookup"><span data-stu-id="7892f-109">Navigate too**More Services** > **Networking** > **Network Watcher**.</span></span> <span data-ttu-id="7892f-110">Vous pouvez sélectionner tous les abonnements hello souhaité tooenable Observateur réseau pour.</span><span class="sxs-lookup"><span data-stu-id="7892f-110">You can select all hello subscriptions you want tooenable Network Watcher for.</span></span> <span data-ttu-id="7892f-111">Cette action crée un Network Watcher dans chaque région disponible.</span><span class="sxs-lookup"><span data-stu-id="7892f-111">This action creates a Network Watcher in every region that is available.</span></span>

![créer un Network Watcher][1]

<span data-ttu-id="7892f-113">Lorsque vous activez Observateur réseau à l’aide de hello Portal, nom hello d’instance de l’Observateur réseau hello aura automatiquement la valeur tooNetworkWatcher_region_name où le nom de région correspond toohello région Azure où l’instance de hello a été activé.</span><span class="sxs-lookup"><span data-stu-id="7892f-113">When you enable Network Watcher using hello Portal, hello name of hello Network Watcher instance will automatically be set tooNetworkWatcher_region_name where region_name corresponds toohello Azure Region where hello instance was enabled.</span></span>  <span data-ttu-id="7892f-114">Par exemple, une instance de Network Watcher activée dans la région États-Unis Centre-Ouest sera nommée NetworkWatcher_westcentralus.</span><span class="sxs-lookup"><span data-stu-id="7892f-114">For example, a Network Watcher enabled in West Central US region will be named NetworkWatcher_westcentralus</span></span>

<span data-ttu-id="7892f-115">En outre, instance de l’Observateur réseau hello est automatiquement ajoutée à un groupe de ressources appelé NetworkWatcherRG.</span><span class="sxs-lookup"><span data-stu-id="7892f-115">Additionally, hello Network Watcher instance will automatically be added into a Resource Group called NetworkWatcherRG.</span></span>  <span data-ttu-id="7892f-116">Il sera créé s’il n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="7892f-116">This Resource Group will be created if it does not already exist.</span></span>

<span data-ttu-id="7892f-117">Si vous voulez que le nom de hello toocustomize d’une instance de l’Observateur réseau et d’hello groupe de ressources, il est placé dans, vous pouvez utiliser les méthodes ARMClient, hello API REST ou Powershell décrites ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7892f-117">If you wish toocustomize hello name of a Network Watcher instance and hello Resource Group it's placed into, you can use Powershell, hello REST API, or ARMClient methods described below.</span></span>  <span data-ttu-id="7892f-118">Dans chaque option, hello groupe de ressources doit exister pour que vous placez hello Observateur réseau dans celui-ci.</span><span class="sxs-lookup"><span data-stu-id="7892f-118">In each option, hello Resource Group must exist before you place hello Network Watcher into it.</span></span>  

## <a name="create-a-network-watcher-with-powershell"></a><span data-ttu-id="7892f-119">Créer un Network Watcher avec PowerShell</span><span class="sxs-lookup"><span data-stu-id="7892f-119">Create a Network Watcher with PowerShell</span></span>

<span data-ttu-id="7892f-120">toocreate une instance de l’Observateur réseau, exécutez hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7892f-120">toocreate an instance of Network Watcher, run hello following example:</span></span>

```powershell
New-AzureRmNetworkWatcher -Name "NetworkWatcher_westcentralus" -ResourceGroupName "NetworkWatcherRG" -Location "West Central US"
```

## <a name="create-a-network-watcher-with-hello-rest-api"></a><span data-ttu-id="7892f-121">Créer un observateur réseau avec l’API REST de hello</span><span class="sxs-lookup"><span data-stu-id="7892f-121">Create a Network Watcher with hello REST API</span></span>

<span data-ttu-id="7892f-122">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7892f-122">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="7892f-123">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="7892f-123">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

### <a name="log-in-with-armclient"></a><span data-ttu-id="7892f-124">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="7892f-124">Log in with ARMClient</span></span>

```powerShell
armclient login
```

### <a name="create-hello-network-watcher"></a><span data-ttu-id="7892f-125">Créer l’Observateur réseau de hello</span><span class="sxs-lookup"><span data-stu-id="7892f-125">Create hello network watcher</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7892f-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7892f-126">Next steps</span></span>

<span data-ttu-id="7892f-127">Maintenant que vous avez une instance de l’Observateur réseau, en savoir plus sur les fonctions hello disponibles :</span><span class="sxs-lookup"><span data-stu-id="7892f-127">Now that you have an instance of Network Watcher, learn about hello features available:</span></span>

* [<span data-ttu-id="7892f-128">Topologie</span><span class="sxs-lookup"><span data-stu-id="7892f-128">Topology</span></span>](network-watcher-topology-overview.md)
* [<span data-ttu-id="7892f-129">Capture de paquets</span><span class="sxs-lookup"><span data-stu-id="7892f-129">Packet capture</span></span>](network-watcher-packet-capture-overview.md)
* [<span data-ttu-id="7892f-130">Vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="7892f-130">IP flow verify</span></span>](network-watcher-ip-flow-verify-overview.md)
* [<span data-ttu-id="7892f-131">Tronçon suivant</span><span class="sxs-lookup"><span data-stu-id="7892f-131">Next hop</span></span>](network-watcher-next-hop-overview.md)
* [<span data-ttu-id="7892f-132">Affichage des groupes de sécurité</span><span class="sxs-lookup"><span data-stu-id="7892f-132">Security group view</span></span>](network-watcher-security-group-view-overview.md)
* [<span data-ttu-id="7892f-133">Journalisation des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="7892f-133">NSG flow logging</span></span>](network-watcher-nsg-flow-logging-overview.md)
* [<span data-ttu-id="7892f-134">Résolution des problèmes de passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="7892f-134">Virtual Network Gateway troubleshooting</span></span>](network-watcher-troubleshoot-overview.md)

<span data-ttu-id="7892f-135">Une fois qu’une instance de l’Observateur réseau a été créée, la capture de package peut être configurée par article hello suivant : [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="7892f-135">Once a Network Watcher instance has been created, package capture can be configured by following hello article: [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

[1]: ./media/network-watcher-create/figure1.png











