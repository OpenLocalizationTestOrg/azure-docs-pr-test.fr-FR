---
title: "connectivité aaaCheck avec l’Observateur réseau de Azure - portail Azure | Documents Microsoft"
description: "Cette page explique comment toocheck une connectivité avec l’Observateur réseau dans hello portail Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: gwallace
ms.openlocfilehash: 8560011906fcce46d31556fc52cbfa671e8e653a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="a2264-103">Vérifiez la connectivité avec l’Observateur réseau de Azure à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a2264-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a2264-104">Portail</span><span class="sxs-lookup"><span data-stu-id="a2264-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="a2264-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a2264-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="a2264-106">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a2264-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="a2264-107">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="a2264-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="a2264-108">Découvrez comment toouse connectivité tooverify si une connexion TCP directe à partir d’un tooa de machine virtuelle donné du point de terminaison peut être établie.</span><span class="sxs-lookup"><span data-stu-id="a2264-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a2264-109">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a2264-109">Before you begin</span></span>

<span data-ttu-id="a2264-110">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="a2264-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="a2264-111">Une instance de l’Observateur réseau dans la région de hello souhaité toocheck connectivité.</span><span class="sxs-lookup"><span data-stu-id="a2264-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="a2264-112">Machines virtuelles toocheck la connectivité avec.</span><span class="sxs-lookup"><span data-stu-id="a2264-112">Virtual machines toocheck connectivity with.</span></span>

<span data-ttu-id="a2264-113">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a2264-113">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="a2264-114">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="a2264-114">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient).</span></span>

<span data-ttu-id="a2264-115">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="a2264-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="a2264-116">La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="a2264-116">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="a2264-117">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="a2264-117">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="a2264-118">Inscrire la fonction d’aperçu hello</span><span class="sxs-lookup"><span data-stu-id="a2264-118">Register hello preview capability</span></span>

<span data-ttu-id="a2264-119">Vérification de la connectivité est actuellement en version préliminaire publique, toouse cette fonctionnalité, qu'il doit toobe inscrit.</span><span class="sxs-lookup"><span data-stu-id="a2264-119">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="a2264-120">toodo, exécution hello suivant l’exemple PowerShell :</span><span class="sxs-lookup"><span data-stu-id="a2264-120">toodo this, run hello following PowerShell sample:</span></span>

```powershell
Register-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace Microsoft.Network
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="a2264-121">l’inscription de hello tooverify a réussi, exécutez hello suivant l’exemple Powershell :</span><span class="sxs-lookup"><span data-stu-id="a2264-121">tooverify hello registration was successful, run hello following Powershell sample:</span></span>

```powershell
Get-AzureRmProviderFeature -FeatureName AllowNetworkWatcherConnectivityCheck  -ProviderNamespace  Microsoft.Network
```

<span data-ttu-id="a2264-122">Si la fonctionnalité de hello a été inscrit correctement, sortie de hello doit correspondre au suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="a2264-122">If hello feature was properly registered, hello output should match hello following:</span></span>

```
FeatureName                             ProviderName      RegistrationState
-----------                             ------------      -----------------
AllowNetworkWatcherConnectivityCheck    Microsoft.Network Registered
```

## <a name="log-in-with-armclient"></a><span data-ttu-id="a2264-123">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="a2264-123">Log in with ARMClient</span></span>

<span data-ttu-id="a2264-124">Ouvrez une session dans tooarmclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="a2264-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="retrieve-a-virtual-machine"></a><span data-ttu-id="a2264-125">Récupérer une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="a2264-125">Retrieve a virtual machine</span></span>

<span data-ttu-id="a2264-126">Exécutez hello suivant script tooreturn une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a2264-126">Run hello following script tooreturn a virtual machine.</span></span> <span data-ttu-id="a2264-127">Ces informations sont nécessaires pour l’exécution de la connectivité.</span><span class="sxs-lookup"><span data-stu-id="a2264-127">This information is needed for running connectivity.</span></span> 

<span data-ttu-id="a2264-128">Hello suivant code doit valeurs pour hello suivant variables :</span><span class="sxs-lookup"><span data-stu-id="a2264-128">hello following code needs values for hello following variables:</span></span>

- <span data-ttu-id="a2264-129">**ID d’abonnement** -hello toouse de ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="a2264-129">**subscriptionId** - hello subscription ID toouse.</span></span>
- <span data-ttu-id="a2264-130">**resourceGroupName** hello - nom du groupe de ressources qui contient des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="a2264-130">**resourceGroupName** - hello name of a resource group that contains virtual machines.</span></span>

```powershell
$subscriptionId = '<subscription id>'
$resourceGroupName = '<resource group name>'

armclient get https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Compute/virtualMachines?api-version=2015-05-01-preview
```

<span data-ttu-id="a2264-131">À partir de la sortie suivante de hello, hello des ID de machine virtuelle de hello est utilisée dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a2264-131">From hello following output, hello ID of hello virtual machine is used in hello following example:</span></span>

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="a2264-132">Vérifiez la connectivité tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="a2264-132">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="a2264-133">Cet exemple vérifie l’ordinateur virtuel de destination de tooa connectivité via le port 80.</span><span class="sxs-lookup"><span data-stu-id="a2264-133">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="a2264-134">Exemple</span><span class="sxs-lookup"><span data-stu-id="a2264-134">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/Database0"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'resourceId': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="a2264-135">Étant donné que cette opération est longue en cours d’exécution, hello URI pour le résultat de hello est retourné dans l’en-tête de réponse hello comme indiqué dans hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="a2264-135">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="a2264-136">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="a2264-136">**Important Values**</span></span>

* <span data-ttu-id="a2264-137">**Emplacement** -cette propriété contient hello URI où hello résultats sont lorsque hello l’opération est terminée</span><span class="sxs-lookup"><span data-stu-id="a2264-137">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: f09b55fe-1d3a-4df7-817f-bceb8d2a94c8
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/f09b55fe-1d3a-4df7-817f-bceb8d2a94c8?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 367a91aa-7142-436a-867d-d3a36f80bc54
x-ms-routing-request-id: WESTUS2:20170602T202117Z:367a91aa-7142-436a-867d-d3a36f80bc54
Date: Fri, 02 Jun 2017 20:21:16 GMT

null
```

### <a name="response"></a><span data-ttu-id="a2264-138">Réponse</span><span class="sxs-lookup"><span data-stu-id="a2264-138">Response</span></span>

<span data-ttu-id="a2264-139">Hello suivant la réponse est à partir de l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="a2264-139">hello following response is from hello previous example.</span></span>  <span data-ttu-id="a2264-140">Dans cette réponse, hello `ConnectionStatus` est **inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="a2264-140">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="a2264-141">Vous pouvez voir que tous les hello sondes envoyées ayant échouées.</span><span class="sxs-lookup"><span data-stu-id="a2264-141">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="a2264-142">Échec de la connectivité de Hello au niveau de l’appliance virtuelle hello tooa échéance configurée par l’utilisateur `NetworkSecurityRule` nommé **UserRule_Port80**, configuré tooblock du trafic entrant sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="a2264-142">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="a2264-143">Ces informations peuvent être utilisées tooresearch les problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="a2264-143">This information can be used tooresearch connection issues.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "0cb75c91-7ebf-4df8-8424-15594d6fb51c",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "06dee00a-9c4a-4fb1-b2ea-fa0a539ca684",
      "address": "10.1.2.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fwNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "75e0cfa5-f9d2-48d8-b705-2c7016f81570"
      ],
      "issues": []
    },
    {
      "type": "VirtualAppliance",
      "id": "75e0cfa5-f9d2-48d8-b705-2c7016f81570",
      "address": "10.1.3.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/auNic/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "86caf6aa-33b0-48a1-b4da-f3c9ce785072"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule",
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ]
        }
      ]
    },
    {
      "type": "VnetLocal",
      "id": "86caf6aa-33b0-48a1-b4da-f3c9ce785072",
      "address": "10.1.4.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/dbNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="a2264-144">Valider les problèmes de routage</span><span class="sxs-lookup"><span data-stu-id="a2264-144">Validate routing issues</span></span>

<span data-ttu-id="a2264-145">exemple de Hello vérifie la connectivité entre un ordinateur virtuel et un point de terminaison distant.</span><span class="sxs-lookup"><span data-stu-id="a2264-145">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="a2264-146">Exemple</span><span class="sxs-lookup"><span data-stu-id="a2264-146">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "13.107.21.200"
$destinationPort = "80"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="a2264-147">Étant donné que cette opération est longue en cours d’exécution, hello URI pour le résultat de hello est retourné dans l’en-tête de réponse hello comme indiqué dans hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="a2264-147">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="a2264-148">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="a2264-148">**Important Values**</span></span>

* <span data-ttu-id="a2264-149">**Emplacement** -cette propriété contient hello URI où hello résultats sont lorsque hello l’opération est terminée</span><span class="sxs-lookup"><span data-stu-id="a2264-149">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 15eeeb69-fcef-41db-bc4a-e2adcf2658e0
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/15eeeb69-fcef-41db-bc4a-e2adcf2658e0?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4370b798-cd8b-4d3e-ba28-22232bc81dc5
x-ms-routing-request-id: WESTUS:20170602T202606Z:4370b798-cd8b-4d3e-ba28-22232bc81dc5
Date: Fri, 02 Jun 2017 20:26:05 GMT

null
```

### <a name="response"></a><span data-ttu-id="a2264-150">Réponse</span><span class="sxs-lookup"><span data-stu-id="a2264-150">Response</span></span>

<span data-ttu-id="a2264-151">Dans l’exemple suivant de hello, hello `connectionStatus` est affiché comme **inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="a2264-151">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="a2264-152">Bonjour `hops` plus d’informations, vous pouvez voir sous `issues` que le trafic de hello a été bloqué échéance tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="a2264-152">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "5528055a-b393-4751-97bc-353d8c0aaeff",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "66eefa79-5bfe-48b2-b6ca-eec8247457a3"
      ],
      "issues": [
        {
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute",
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ]
        }
      ]
    },
    {
      "type": "Destination",
      "id": "66eefa79-5bfe-48b2-b6ca-eec8247457a3",
      "address": "13.107.21.200",
      "resourceId": "Unknown",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Unreachable",
  "probesSent": 100,
  "probesFailed": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="a2264-153">Vérifier la latence du site Web</span><span class="sxs-lookup"><span data-stu-id="a2264-153">Check website latency</span></span>

<span data-ttu-id="a2264-154">Hello exemple suivant vérifie le site Web du tooa hello connectivité.</span><span class="sxs-lookup"><span data-stu-id="a2264-154">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="a2264-155">Exemple</span><span class="sxs-lookup"><span data-stu-id="a2264-155">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "http://bing.com"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="a2264-156">Étant donné que cette opération est longue en cours d’exécution, hello URI pour le résultat de hello est retourné dans l’en-tête de réponse hello comme indiqué dans hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="a2264-156">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="a2264-157">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="a2264-157">**Important Values**</span></span>

* <span data-ttu-id="a2264-158">**Emplacement** -cette propriété contient hello URI où hello résultats sont lorsque hello l’opération est terminée</span><span class="sxs-lookup"><span data-stu-id="a2264-158">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: e49b12c7-c232-472c-b6d2-6c257ce80fa5
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/e49b12c7-c232-472c-b6d2-6c257ce80fa5?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: c3d9744f-5683-427d-bdd1-636b68ab01b6
x-ms-routing-request-id: WESTUS:20170602T203101Z:c3d9744f-5683-427d-bdd1-636b68ab01b6
Date: Fri, 02 Jun 2017 20:31:00 GMT

null
```

### <a name="response"></a><span data-ttu-id="a2264-159">Réponse</span><span class="sxs-lookup"><span data-stu-id="a2264-159">Response</span></span>

<span data-ttu-id="a2264-160">Bonjour suivant la réponse, vous pouvez voir hello `connectionStatus` affiche sous la forme **joignable**.</span><span class="sxs-lookup"><span data-stu-id="a2264-160">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="a2264-161">Lorsqu’une connexion est établie, les valeurs de latence sont fournies.</span><span class="sxs-lookup"><span data-stu-id="a2264-161">When a connection is successful, latency values are provided.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "204.79.197.200",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="a2264-162">Vérifiez le point de terminaison de stockage de connectivité tooa</span><span class="sxs-lookup"><span data-stu-id="a2264-162">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="a2264-163">Hello exemple suivant vérifie la hello connectivité à partir d’un compte de stockage de blog de l’ordinateur virtuel tooa.</span><span class="sxs-lookup"><span data-stu-id="a2264-163">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="a2264-164">Exemple</span><span class="sxs-lookup"><span data-stu-id="a2264-164">Example</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$sourceResourceId = "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Compute/virtualMachines/MultiTierApp0"
$destinationAddress = "https://build2017nwdiag360.blob.core.windows.net/"
$destinationPort = "0"
$requestBody = @"
{
  'source': {
    'resourceId': '${sourceResourceId}',
    'port': 0
  },
  'destination': {
    'address': '${destinationAddress}',
    'port': ${destinationPort}
  }
}
"@

$response = armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/connectivityCheck?api-version=2017-03-01" $requestBody
```

<span data-ttu-id="a2264-165">Étant donné que cette opération est longue en cours d’exécution, hello URI pour le résultat de hello est retourné dans l’en-tête de réponse hello comme indiqué dans hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="a2264-165">Since this operation is long running, hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="a2264-166">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="a2264-166">**Important Values**</span></span>

* <span data-ttu-id="a2264-167">**Emplacement** -cette propriété contient hello URI où hello résultats sont lorsque hello l’opération est terminée</span><span class="sxs-lookup"><span data-stu-id="a2264-167">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/c4ed3806-61ea-4a6b-abc1-9d6f2afc79c2?api-version=2017-03-01
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
x-ms-routing-request-id: WESTUS2:20170602T200504Z:93bf5af0-fef5-4b7a-bb9e-9976ba5cdb95
Date: Fri, 02 Jun 2017 20:05:03 GMT

null
```

### <a name="response"></a><span data-ttu-id="a2264-168">Réponse</span><span class="sxs-lookup"><span data-stu-id="a2264-168">Response</span></span>

<span data-ttu-id="a2264-169">Hello exemple suivant est réponse hello à partir de l’appel d’API précédente hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a2264-169">hello following example is hello response from running hello previous API call.</span></span> <span data-ttu-id="a2264-170">Comme la vérification de hello est réussie, hello `connectionStatus` propriété s’affiche en tant que **joignable**.</span><span class="sxs-lookup"><span data-stu-id="a2264-170">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="a2264-171">Vous trouverez détails hello concernant le nombre de hello de blob de stockage hello sauts tooreach requis et la latence.</span><span class="sxs-lookup"><span data-stu-id="a2264-171">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

```json
{
  "hops": [
    {
      "type": "Source",
      "id": "6adc0fe1-e384-4220-b1b1-f0d181220072",
      "address": "10.1.1.4",
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "nextHopIds": [
        "b50b7076-9ff2-4782-b40e-0b89cf758f74"
      ],
      "issues": []
    },
    {
      "type": "Internet",
      "id": "b50b7076-9ff2-4782-b40e-0b89cf758f74",
      "address": "13.71.200.248",
      "resourceId": "Internet",
      "nextHopIds": [],
      "issues": []
    }
  ],
  "connectionStatus": "Reachable",
  "avgLatencyInMs": 1,
  "minLatencyInMs": 0,
  "maxLatencyInMs": 7,
  "probesSent": 100,
  "probesFailed": 0
}
```

## <a name="next-steps"></a><span data-ttu-id="a2264-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a2264-172">Next steps</span></span>

<span data-ttu-id="a2264-173">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="a2264-173">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="a2264-174">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="a2264-174">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

<!-- Image references -->














