---
title: "vérification du trafic aaaVerify le transfert IP de l’Observateur réseau Azure - REST | Documents Microsoft"
description: "Cet article décrit comment toocheck si tooor le trafic à partir d’un ordinateur virtuel est autorisé ou refusé"
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
ms.openlocfilehash: 956db0d326db597c6c402a9e8d4a5522c47c02d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="d9d50-103">Vérifier si le trafic est autorisé ou refusé avec le composant de vérification des flux IP d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="d9d50-103">Check if traffic is allowed or denied with IP flow verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d9d50-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="d9d50-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="d9d50-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9d50-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="d9d50-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d9d50-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="d9d50-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d9d50-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="d9d50-108">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="d9d50-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="d9d50-109">Vérifiez que les flux IP est une fonctionnalité de l’Observateur réseau qui vous permet de tooverify si le trafic est autorisé à tooor à partir d’un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="d9d50-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="d9d50-110">la validation de Hello peut être exécutée pour le trafic entrant ou sortant.</span><span class="sxs-lookup"><span data-stu-id="d9d50-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="d9d50-111">Ce scénario est utile tooget un état actuel de si un ordinateur virtuel peut communiquer avec les ressources externes tooan ou principal.</span><span class="sxs-lookup"><span data-stu-id="d9d50-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or backend.</span></span> <span data-ttu-id="d9d50-112">Les flux IP vérifier peut être utilisé tooverify si vos règles de groupe de sécurité réseau (NSG) sont correctement configurés et résoudre les problèmes de flux qui sont bloqués par les règles du groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d9d50-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="d9d50-113">Une autre raison de l’utilisation de IP flux Vérifiez à bloquer le trafic de tooensure est bloqué correctement par hello groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d9d50-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d9d50-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="d9d50-114">Before you begin</span></span>

<span data-ttu-id="d9d50-115">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d9d50-115">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="d9d50-116">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="d9d50-116">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="d9d50-117">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="d9d50-117">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

## <a name="scenario"></a><span data-ttu-id="d9d50-118">Scénario</span><span class="sxs-lookup"><span data-stu-id="d9d50-118">Scenario</span></span>

<span data-ttu-id="d9d50-119">Ce scénario utilise IP flux Vérifiez tooverify si une machine virtuelle peut communiquer avec l’ordinateur de tooanother sur le port 443.</span><span class="sxs-lookup"><span data-stu-id="d9d50-119">This scenario uses IP flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="d9d50-120">Si le trafic de hello est refusé, elle retourne la règle de sécurité hello refuse ce trafic.</span><span class="sxs-lookup"><span data-stu-id="d9d50-120">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="d9d50-121">toolearn en savoir plus sur les flux d’IP Verify, visitez [les flux IP vérifier la vue d’ensemble](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d9d50-121">toolearn more about IP flow Verify, visit [IP flow verify overview](network-watcher-ip-flow-verify-overview.md)</span></span>

<span data-ttu-id="d9d50-122">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="d9d50-122">In this scenario, you:</span></span>

* <span data-ttu-id="d9d50-123">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d9d50-123">Retrieve a virtual machine</span></span>
* <span data-ttu-id="d9d50-124">Appeler la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="d9d50-124">Call IP flow verify</span></span>
* <span data-ttu-id="d9d50-125">Vérifier les résultats</span><span class="sxs-lookup"><span data-stu-id="d9d50-125">Verify results</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="d9d50-126">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="d9d50-126">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="d9d50-127">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="d9d50-127">Retrieve a virtual machine</span></span>

<span data-ttu-id="d9d50-128">Exécutez hello suivant script tooreturn une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="d9d50-128">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="d9d50-129">Hello suivant code a besoin de valeurs pour les variables de hello :</span><span class="sxs-lookup"><span data-stu-id="d9d50-129">hello following code needs values for hello variables:</span></span>

* <span data-ttu-id="d9d50-130">**ID d’abonnement** -hello toouse de Id d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="d9d50-130">**subscriptionId** - hello subscription Id toouse.</span></span>
* <span data-ttu-id="d9d50-131">**resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="d9d50-131">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = "<subscription id>"
$resourceGroupName = "<resource group name>"

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="d9d50-132">informations nécessaires Hello sont id hello sous le type hello `Microsoft.Compute/virtualMachines`.</span><span class="sxs-lookup"><span data-stu-id="d9d50-132">hello information that is needed is hello id under hello type `Microsoft.Compute/virtualMachines`.</span></span> <span data-ttu-id="d9d50-133">les résultats de Hello doivent être similaires toohello suivant l’exemple de code :</span><span class="sxs-lookup"><span data-stu-id="d9d50-133">hello results should be similar toohello following code sample:</span></span>

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

## <a name="call-ip-flow-verify"></a><span data-ttu-id="d9d50-134">Appeler la vérification des flux IP</span><span class="sxs-lookup"><span data-stu-id="d9d50-134">Call IP flow Verify</span></span>

<span data-ttu-id="d9d50-135">Hello exemple suivant crée un demande tooverify hello du trafic d’un ordinateur virtuel spécifié.</span><span class="sxs-lookup"><span data-stu-id="d9d50-135">hello following example creates a request tooverify hello traffic for a specified virtual machine.</span></span> <span data-ttu-id="d9d50-136">réponse de Hello retourne si hello le trafic est autorisé ou si le trafic de hello est refusé.</span><span class="sxs-lookup"><span data-stu-id="d9d50-136">hello response returns if hello traffic is allowed or if hello traffic is denied.</span></span> <span data-ttu-id="d9d50-137">Si le trafic est refusé qu'il retourne également les blocs de règles hello du trafic.</span><span class="sxs-lookup"><span data-stu-id="d9d50-137">If traffic is denied it also returns what rule blocks hello traffic.</span></span>

> [!NOTE]
> <span data-ttu-id="d9d50-138">Les flux IP vérifier requiert que la ressource de machine virtuelle hello est allouée.</span><span class="sxs-lookup"><span data-stu-id="d9d50-138">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="d9d50-139">script de Hello nécessite un Id d’un ordinateur virtuel et d’une carte d’interface réseau sur l’ordinateur virtuel de hello de la ressource hello.</span><span class="sxs-lookup"><span data-stu-id="d9d50-139">hello script requires hello resource Id of a virtual machine and of a network interface card on hello virtual machine.</span></span> <span data-ttu-id="d9d50-140">Ces valeurs sont fournies par hello précédant la sortie.</span><span class="sxs-lookup"><span data-stu-id="d9d50-140">These values are provided by hello preceding output.</span></span>

> [!Important]
> <span data-ttu-id="d9d50-141">Pour le reste de l’Observateur réseau tous les appels hello nom de groupe de ressources dans l’URI est hello qui contient d’instance de l’Observateur réseau hello, pas les ressources hello vous effectuez des actions de diagnostic hello sur la demande hello.</span><span class="sxs-lookup"><span data-stu-id="d9d50-141">For all Network Watcher REST calls hello resource group name in hello request URI is hello one that contains hello Network Watcher instance, not hello resources you are performing hello diagnostic actions on.</span></span>

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

## <a name="understanding-hello-results"></a><span data-ttu-id="d9d50-142">Présentation des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="d9d50-142">Understanding hello results</span></span>

<span data-ttu-id="d9d50-143">Hello réponse renvoyée indique si le trafic de hello est autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="d9d50-143">hello response you get back tells you whether hello traffic is allowed or denied.</span></span> <span data-ttu-id="d9d50-144">réponse de Hello ressemble à un des hello exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d9d50-144">hello response looks like one of hello following examples:</span></span>

<span data-ttu-id="d9d50-145">**Autorisé**</span><span class="sxs-lookup"><span data-stu-id="d9d50-145">**Allowed**</span></span>

```json
{
  "access": "Allow",
  "ruleName": "defaultSecurityRules/AllowInternetOutBound"
}
```

<span data-ttu-id="d9d50-146">**Refusé**</span><span class="sxs-lookup"><span data-stu-id="d9d50-146">**Denied**</span></span>

```json
{
  "access": "Deny",
  "ruleName": "defaultSecurityRules/DefaultInboundDenyAll"
}
```

## <a name="next-steps"></a><span data-ttu-id="d9d50-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d9d50-147">Next steps</span></span>

<span data-ttu-id="d9d50-148">Si le trafic est bloqué et ne doit pas être, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn plus d’informations sur les groupes de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d9d50-148">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) toolearn more about Network Security Groups.</span></span>












