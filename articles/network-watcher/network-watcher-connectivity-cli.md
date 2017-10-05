---
title: "Vérifier la connectivité avec Azure Network Watcher - API CLI2.0 | Microsoft Docs"
description: "Cette page explique comment vérifier la connectivité avec Network Watcher à l’aide d’Azure CLI 2.0"
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
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: c1deaa40bfda0bf3858ad56d3d6a90df34351278
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="5bf4b-103">Vérifier la connectivité avec Azure Network Watcher à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5bf4b-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5bf4b-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bf4b-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="5bf4b-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5bf4b-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="5bf4b-106">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="5bf4b-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="5bf4b-107">Découvrez comment utiliser la connectivité pour vérifier si une connexion TCP directe entre une machine virtuelle et un point de terminaison donné peut être établie.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-107">Learn how to use connectivity to verify if a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5bf4b-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="5bf4b-108">Before you begin</span></span>

<span data-ttu-id="5bf4b-109">Cet article part du principe que vous disposez des ressources suivantes :</span><span class="sxs-lookup"><span data-stu-id="5bf4b-109">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="5bf4b-110">Une instance de Network Watcher dans la région où vous souhaitez vérifier la connectivité.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-110">An instance of Network Watcher in the region you want to check connectivity.</span></span>

* <span data-ttu-id="5bf4b-111">Des machines virtuelles avec lesquelles vérifier la connectivité.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-111">Virtual machines to check connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="5bf4b-112">La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="5bf4b-113">Pour installer l’extension sur une machine virtuelle Windows, consultez la page [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Windows). Pour une machine virtuelle Linux, consultez la page [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md) (Extension de machine virtuelle Azure Network Watcher Agent pour Linux).</span><span class="sxs-lookup"><span data-stu-id="5bf4b-113">For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-the-preview-capability"></a><span data-ttu-id="5bf4b-114">Inscrire la fonction de version préliminaire</span><span class="sxs-lookup"><span data-stu-id="5bf4b-114">Register the preview capability</span></span> 

<span data-ttu-id="5bf4b-115">La vérification de connectivité est actuellement en préversion publique. Pour l’utiliser, cette fonctionnalité doit être inscrite.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-115">Connectivity check is currently in public preview, to use this feature it needs to be registered.</span></span> <span data-ttu-id="5bf4b-116">Pour ce faire, exécutez l’exemple de commande CLI suivant :</span><span class="sxs-lookup"><span data-stu-id="5bf4b-116">To do this, run the following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="5bf4b-117">Pour vérifier que l’inscription s’est bien déroulée, exécutez la commande de l’interface de ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5bf4b-117">To verify the registration was successful, run the following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="5bf4b-118">Si la fonctionnalité a été correctement inscrite, vous devez obtenir la sortie suivante :</span><span class="sxs-lookup"><span data-stu-id="5bf4b-118">If the feature was properly registered, the output should match the following:</span></span> 

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Features/providers/Microsoft.Network/features/AllowNetworkWatcherConnectivityCheck",
  "name": "Microsoft.Network/AllowNetworkWatcherConnectivityCheck",
  "properties": {
    "state": "Registered"
  },
  "type": "Microsoft.Features/providers/features"
}
``` 

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="5bf4b-119">Vérifier la connectivité à une machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="5bf4b-119">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="5bf4b-120">Cet exemple vérifie la connectivité à une machine virtuelle de destination sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-120">This example checks connectivity to a destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="5bf4b-121">Exemple</span><span class="sxs-lookup"><span data-stu-id="5bf4b-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="5bf4b-122">Réponse</span><span class="sxs-lookup"><span data-stu-id="5bf4b-122">Response</span></span>

<span data-ttu-id="5bf4b-123">La réponse suivante est tirée de l’exemple précédent.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-123">The following response is from the previous example.</span></span>  <span data-ttu-id="5bf4b-124">Dans cette réponse, `ConnectionStatus` est **Inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-124">In this response, the `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="5bf4b-125">Vous pouvez constater que toutes les sondes envoyées ont échoué.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-125">You can see that all the probes sent failed.</span></span> <span data-ttu-id="5bf4b-126">La connectivité a échoué au niveau de l’appliance virtuelle en raison de `NetworkSecurityRule`, configuré par l’utilisateur et nommé **UserRule_Port80**, destiné à bloquer le trafic entrant sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-126">The connectivity failed at the virtual appliance due to a user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured to block incoming traffic on port 80.</span></span> <span data-ttu-id="5bf4b-127">Ces informations peuvent être utilisées pour mener des recherches sur les problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-127">This information can be used to research connection issues.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "bb01d336-d881-4808-9fbc-72f091974d68",
      "issues": [],
      "nextHopIds": [
        "f8b074e9-9980-496b-a35e-619f9bcbf648"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "10.1.2.4",
      "id": "f8b074e9-9980-496b-a35e-619f9bcbf648",
      "issues": [],
      "nextHopIds": [
        "8a5857f3-6ab8-4b11-b9bf-a046d66b8696"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/fw
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.3.4",
      "id": "8a5857f3-6ab8-4b11-b9bf-a046d66b8696",
      "issues": [
        {
          "context": [
            {
              "key": "RuleName",
              "value": "UserRule_Port80"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "NetworkSecurityRule"
        }
      ],
      "nextHopIds": [
        "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/au
Nic/ipConfigurations/ipconfig1",
      "type": "VirtualAppliance"
    },
    {
      "address": "10.1.4.4",
      "id": "6ce2f7a2-ceb4-4145-80e8-5d9f661655d6",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/db
Nic0/ipConfigurations/ipconfig1",
      "type": "VnetLocal"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="validate-routing-issues"></a><span data-ttu-id="5bf4b-128">Valider les problèmes de routage</span><span class="sxs-lookup"><span data-stu-id="5bf4b-128">Validate routing issues</span></span>

<span data-ttu-id="5bf4b-129">Cet exemple vérifie la connectivité entre une machine virtuelle et un point de terminaison distant.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-129">The example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="5bf4b-130">Exemple</span><span class="sxs-lookup"><span data-stu-id="5bf4b-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="5bf4b-131">Réponse</span><span class="sxs-lookup"><span data-stu-id="5bf4b-131">Response</span></span>

<span data-ttu-id="5bf4b-132">Dans l’exemple suivant, `connectionStatus` est **Inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-132">In the following example, the `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="5bf4b-133">Dans les informations relatives à `hops`, vous pouvez constater sous `issues` que le trafic a été bloqué par `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-133">In the `hops` details, you can see under `issues` that the traffic was blocked due to a `UserDefinedRoute`.</span></span>

```json
{
  "avgLatencyInMs": null,
  "connectionStatus": "Unreachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "f2cb1868-2049-4839-b8ed-57a480d06f95",
      "issues": [
        {
          "context": [
            {
              "key": "RouteType",
              "value": "User"
            }
          ],
          "origin": "Outbound",
          "severity": "Error",
          "type": "UserDefinedRoute"
        }
      ],
      "nextHopIds": [
        "da4022db-0ab0-48c4-a507-dd4c03561ca5"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "13.107.21.200",
      "id": "da4022db-0ab0-48c4-a507-dd4c03561ca5",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Unknown",
      "type": "Destination"
    }
  ],
  "maxLatencyInMs": null,
  "minLatencyInMs": null,
  "probesFailed": 100,
  "probesSent": 100
}
```

## <a name="check-website-latency"></a><span data-ttu-id="5bf4b-134">Vérifier la latence du site Web</span><span class="sxs-lookup"><span data-stu-id="5bf4b-134">Check website latency</span></span>

<span data-ttu-id="5bf4b-135">L’exemple suivant vérifie la connectivité à un site Web.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-135">The following example checks the connectivity to a website.</span></span>

### <a name="example"></a><span data-ttu-id="5bf4b-136">Exemple</span><span class="sxs-lookup"><span data-stu-id="5bf4b-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="5bf4b-137">Réponse</span><span class="sxs-lookup"><span data-stu-id="5bf4b-137">Response</span></span>

<span data-ttu-id="5bf4b-138">Dans la réponse suivante, vous pouvez constater que `connectionStatus` apparaît **Joignable**.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-138">In the following response, you can see the `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="5bf4b-139">Lorsqu’une connexion est établie, les valeurs de latence sont fournies.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-139">When a connection is successful, latency values are provided.</span></span>

```json
{
  "avgLatencyInMs": 2,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "639c2d19-e163-4dfd-8737-5018dd1168ae",
      "issues": [],
      "nextHopIds": [
        "fd43a6e7-c758-4f48-90aa-8db99105a4a3"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/ap
pNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "204.79.197.200",
      "id": "fd43a6e7-c758-4f48-90aa-8db99105a4a3",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="check-connectivity-to-a-storage-endpoint"></a><span data-ttu-id="5bf4b-140">Vérifier la connectivité à un point de terminaison de stockage</span><span class="sxs-lookup"><span data-stu-id="5bf4b-140">Check connectivity to a storage endpoint</span></span>

<span data-ttu-id="5bf4b-141">L’exemple suivant vérifie la connectivité entre une machine virtuelle et un compte de stockage blob.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-141">The following example checks the connectivity from a virtual machine to a blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="5bf4b-142">Exemple</span><span class="sxs-lookup"><span data-stu-id="5bf4b-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="5bf4b-143">Réponse</span><span class="sxs-lookup"><span data-stu-id="5bf4b-143">Response</span></span>

<span data-ttu-id="5bf4b-144">Le code json suivant est un exemple de réponse tiré de l’exécution de la cmdlet précédente.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-144">The following json is the example response from running the previous cmdlet.</span></span> <span data-ttu-id="5bf4b-145">Si la vérification est réussie, la propriété `connectionStatus` apparaît **Joignable**.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-145">As the check is successful, the `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="5bf4b-146">Les détails concernant le nombre de tronçons nécessaires pour accéder à l’objet blob de stockage et la latence vous sont fournis.</span><span class="sxs-lookup"><span data-stu-id="5bf4b-146">You are provided the details regarding the number of hops required to reach the storage blob and latency.</span></span>

```json
{
  "avgLatencyInMs": 1,
  "connectionStatus": "Reachable",
  "hops": [
    {
      "address": "10.1.1.4",
      "id": "5136acff-bf26-4c93-9966-4edb7dd40353",
      "issues": [],
      "nextHopIds": [
        "f8d958b7-3636-4d63-9441-602c1eb2fd56"
      ],
      "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/ContosoRG/providers/Microsoft.Network/networkInterfaces/appNic0/ipConfigurations/ipconfig1",
      "type": "Source"
    },
    {
      "address": "1.2.3.4",
      "id": "f8d958b7-3636-4d63-9441-602c1eb2fd56",
      "issues": [],
      "nextHopIds": [],
      "resourceId": "Internet",
      "type": "Internet"
    }
  ],
  "maxLatencyInMs": 7,
  "minLatencyInMs": 0,
  "probesFailed": 0,
  "probesSent": 100
}
```

## <a name="next-steps"></a><span data-ttu-id="5bf4b-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5bf4b-147">Next steps</span></span>

<span data-ttu-id="5bf4b-148">Découvrez comment automatiser les captures de paquets avec des alertes de machine virtuelle en consultant [Create an alert triggered packet capture (Créer une capture de paquets déclenchée par alerte)](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="5bf4b-148">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="5bf4b-149">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="5bf4b-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
