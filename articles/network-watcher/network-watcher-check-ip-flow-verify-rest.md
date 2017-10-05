---
title: "Vérifier le trafic avec la vérification des flux IP d’Azure Network Watcher - REST | Microsoft Docs"
description: "Cet article explique comment savoir si le trafic en direction ou en provenance d’une machine virtuelle est autorisé ou refusé"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 3307a79f-03be-46a0-aaaf-b2079cb5f3b2
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 6d3ce00a7d4f9c0cd57fa8815625a1065b03b5b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="8ce97-103">Vérifier si le trafic est autorisé ou refusé avec le composant de vérification des flux IP d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="8ce97-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="8ce97-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="8ce97-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="8ce97-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8ce97-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="8ce97-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="8ce97-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="8ce97-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="8ce97-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="8ce97-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="8ce97-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="8ce97-109">La vérification des flux IP est une fonctionnalité de Network Watcher qui vous permet de vérifier si le trafic en direction ou en provenance d’une machine virtuelle est autorisé.</span><span class="sxs-lookup"><span data-stu-id="8ce97-109">IP flow verify is a feature of Network Watcher that allows you to verify if traffic is allowed to or from a virtual machine.</span></span> <span data-ttu-id="8ce97-110">La validation peut être exécutée pour le trafic entrant ou sortant.</span><span class="sxs-lookup"><span data-stu-id="8ce97-110">The validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="8ce97-111">Cette fonctionnalité est très utile pour définir si une machine virtuelle peut actuellement communiquer avec une ressource externe ou un serveur back-end.</span><span class="sxs-lookup"><span data-stu-id="8ce97-111">This scenario is useful to get a current state of whether a virtual machine can talk to an external resource or backend.</span></span> <span data-ttu-id="8ce97-112">La vérification des flux IP peut être utilisée pour vérifier si les règles de votre groupe de sécurité réseau sont correctement configurées et pour résoudre les problèmes de flux bloqués par les règles de groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8ce97-112">IP flow verify can be used to verify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="8ce97-113">La vérification des flux IP permet aussi de s’assurer que le trafic que vous souhaitez bloquer est correctement bloqué par le groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8ce97-113">Another reason for using IP flow verify is to ensure traffic that you want blocked is being blocked properly by the NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="8ce97-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8ce97-114">Before you begin</span></span>

<span data-ttu-id="8ce97-115">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8ce97-115">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="8ce97-116">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="8ce97-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="8ce97-117">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="8ce97-117">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="8ce97-118">Scénario</span><span class="sxs-lookup"><span data-stu-id="8ce97-118">Scenario</span></span>

<span data-ttu-id="8ce97-119">Ce scénario utilise la vérification des flux IP pour vérifier si une machine virtuelle peut communiquer avec une autre machine par le biais du port 443.</span><span class="sxs-lookup"><span data-stu-id="8ce97-119">This scenario uses IP flow Verify to verify if a virtual machine can talk to another machine over port 443.</span></span> <span data-ttu-id="8ce97-120">Si le trafic est refusé, la règle de sécurité refusant ce trafic est renvoyée.</span><span class="sxs-lookup"><span data-stu-id="8ce97-120">If the traffic is denied, it returns the security rule that is denying that traffic.</span></span> <span data-ttu-id="8ce97-121">Pour en savoir plus sur la vérification des flux IP, consultez [Vue d’ensemble de la vérification des flux IP](network-watcher-ip-flow-verify-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8ce97-121">To learn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="8ce97-122">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="8ce97-122">In this scenario, you:</span></span>

* <span data-ttu-id="8ce97-123">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8ce97-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="8ce97-124">Appeler la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="8ce97-124">Call IP flow verify</span></span>
* <span data-ttu-id="8ce97-125">Vérifier les résultats</span><span class="sxs-lookup"><span data-stu-id="8ce97-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="8ce97-126">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="8ce97-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="8ce97-127">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="8ce97-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="8ce97-128">Exécutez le script suivant pour renvoyer une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ce97-128">Run the following script to return a virtual machine.</span></span> <span data-ttu-id="8ce97-129">Le code suivant a besoin de valeurs pour les variables :</span><span class="sxs-lookup"><span data-stu-id="8ce97-129">The following code needs values for the variables:</span></span>

* <span data-ttu-id="8ce97-130">**subscriptionId** - L’ID d’abonnement à utiliser.</span><span class="sxs-lookup"><span data-stu-id="8ce97-130">**subscriptionId** - The subscription Id to use.</span></span>
* <span data-ttu-id="8ce97-131">**resourceGroupName** - Le nom d’un groupe de ressources qui contient les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="8ce97-131">**resourceGroupName** - The name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="8ce97-132">Les informations nécessaires sont l’ID sous le type de `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="8ce97-132">The information that is needed is the id under the type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="8ce97-133">Les résultats doivent ressembler à l’exemple de code suivant :</span><span class="sxs-lookup"><span data-stu-id="8ce97-133">The results should be similar to the following code sample:</span></span>

```json
...,
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft
.Network/networkInterfaces/contosovm842"
            }
          ]
        },
        "provisioningState": "Succeeded"
      },
      "resources": [
        {
          "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Com
pute/virtualMachines/ContosoVM/extensions/CustomScriptExtension"
        }
      ],
      "type": "Microsoft.Compute/virtualMachines",
      "location": "westcentralus",
      "id": "/subscriptions/{00000000-0000-0000-0000-000000000000}/resourceGroups/ContosoExampleRG/providers/Microsoft.Compute
/virtualMachines/ContosoVM",
      "name": "ContosoVM"
    }
  ]
}
```

## <a name="call-ip-flow-verify"></a><span data-ttu-id="8ce97-134">Appeler la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="8ce97-134">Call IP flow Verify</span></span>

<span data-ttu-id="8ce97-135">L’exemple suivant crée une demande pour vérifier le trafic d’une machine virtuelle spécifiée.</span><span class="sxs-lookup"><span data-stu-id="8ce97-135">The following example creates a request to verify the traffic for a specified virtual machine.</span></span> <span data-ttu-id="8ce97-136">La réponse renvoyée indique si le trafic est autorisé ou si le trafic est refusé.</span><span class="sxs-lookup"><span data-stu-id="8ce97-136">The response returns if the traffic is allowed or if the traffic is denied.</span></span> <span data-ttu-id="8ce97-137">Si le trafic est refusé, elle indique également quelle règle bloque le trafic.</span><span class="sxs-lookup"><span data-stu-id="8ce97-137">If traffic is denied it also returns what rule blocks the traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="8ce97-138">La vérification des flux IP nécessite l’attribution de la ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ce97-138">IP flow verify requires that the VM resource is allocated.</span></span>

<span data-ttu-id="8ce97-139">Le script requiert l’ID de la ressource d’une machine virtuelle et d’une carte d’interface réseau sur la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="8ce97-139">The script requires the resource Id of a virtual machine and of a network interface card on the virtual machine.</span></span> <span data-ttu-id="8ce97-140">Ces valeurs sont fournies par le résultat précédent.</span><span class="sxs-lookup"><span data-stu-id="8ce97-140">These values are provided by the preceding output.</span></span>

> [!Important]
> <span data-ttu-id="8ce97-141">Pour tous les appels REST de Network Watcher, le nom du groupe de ressources dans l’URI de requête correspond à celui qui contient l’instance de Network Watcher, et non les ressources sur lesquelles vous exécutez les actions de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="8ce97-141">For all Network Watcher REST calls the resource group name in the request URI is the one that contains the Network Watcher instance, not the resources you are performing the diagnostic actions on.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"
$networkWatcherName = "<network watcher name>"
$vmName = "<vm name>"
$vmNICName = "<vm NIC name>"
$direction = "<direction of traffic>" # Examples are: Inbound or Outbound
$localIP = "<source IP>"
$localPort = "<source Port>"
$remoteIP = "<destination IP>"
$remotePort = "<destination Port>" # Examples are: 80, or 80-120
$protocol = "<UDP, TCP or *>"
$targetUri = "<uri of target resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.compute/virtualMachine/${vmName}
$targetNic = "<uri of target nic resource>" # Example: /subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkInterfaces/${vmNICName}

$requestBody = @"
{
    'targetResourceId':  '$targetUri',
    'direction':  '$direction',
    'protocol':  '$protocol',
    'localPort':  '$localPort',
    'remotePort':  '$remotePort',
    'localIPAddress':  '$localIP',
    'remoteIPAddress':  '$remoteIP',
    'targetNICResourceId':  '$targetNic'
}
"@
        
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/ipFlowVerify?api-version=2016-12-01" $requestBody -verbose
```

## <a name="understanding-the-results"></a><span data-ttu-id="8ce97-142">Compréhension des résultats</span><span class="sxs-lookup"><span data-stu-id="8ce97-142">Understanding the results</span></span>

<span data-ttu-id="8ce97-143">La réponse que vous obtenez en retour vous indique si le trafic est autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="8ce97-143">The response you get back tells you whether the traffic is allowed or denied.</span></span> <span data-ttu-id="8ce97-144">La réponse ressemble à l’un des exemples suivants :</span><span class="sxs-lookup"><span data-stu-id="8ce97-144">The response looks like one of the following examples:</span></span>

<span data-ttu-id="8ce97-145">**Autorisé**</span><span class="sxs-lookup"><span data-stu-id="8ce97-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="8ce97-146">**Refusé**</span><span class="sxs-lookup"><span data-stu-id="8ce97-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="8ce97-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8ce97-147">Next steps</span></span>

<span data-ttu-id="8ce97-148">Si le trafic est bloqué alors qu’il ne devrait pas l’être, consultez [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) pour en savoir plus sur les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="8ce97-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to learn more about Network Security Groups.</span></span>












