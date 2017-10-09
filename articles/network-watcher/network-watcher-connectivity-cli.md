---
title: "connectivité aaaCheck avec l’Observateur réseau de Azure - Azure CLI 2.0 | Documents Microsoft"
description: "Cette page explique comment vérifier des toouse connectivité avec l’Observateur réseau à l’aide d’Azure CLI 2.0"
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
ms.openlocfilehash: e94e0fad03fd36ebf4e1fdf9e3cfee934b289deb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-azure-cli-20"></a><span data-ttu-id="b9b5a-103">Vérifier la connectivité avec Azure Network Watcher à l’aide d’Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b9b5a-103">Check connectivity with Azure Network Watcher using Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="b9b5a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b9b5a-104">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="b9b5a-105">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b9b5a-105">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="b9b5a-106">API REST Azure</span><span class="sxs-lookup"><span data-stu-id="b9b5a-106">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="b9b5a-107">Découvrez comment toouse connectivité tooverify si une connexion TCP directe à partir d’un tooa de machine virtuelle donné du point de terminaison peut être établie.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-107">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b9b5a-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b9b5a-108">Before you begin</span></span>

<span data-ttu-id="b9b5a-109">Cet article suppose que vous avez hello suivant des ressources :</span><span class="sxs-lookup"><span data-stu-id="b9b5a-109">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="b9b5a-110">Une instance de l’Observateur réseau dans la région de hello souhaité toocheck connectivité.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-110">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="b9b5a-111">Machines virtuelles toocheck la connectivité avec.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-111">Virtual machines toocheck connectivity with.</span></span>

[!INCLUDE [network-watcher-preview](../../includes/network-watcher-public-preview-notice.md)]

> [!IMPORTANT]
> <span data-ttu-id="b9b5a-112">La vérification de la connectivité requiert une extension de machine virtuelle `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-112">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="b9b5a-113">Pour installer l’extension de hello sur une machine virtuelle Windows, visitez [extension de machine virtuelle d’Agent de l’Observateur réseau Azure pour Windows](../virtual-machines/windows/extensions-nwa.md) et de, visitez Linux VM [extension de machine virtuelle Azure réseau Observateur Agent pour Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="b9b5a-113">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="register-hello-preview-capability"></a><span data-ttu-id="b9b5a-114">Inscrire la fonction d’aperçu hello</span><span class="sxs-lookup"><span data-stu-id="b9b5a-114">Register hello preview capability</span></span> 

<span data-ttu-id="b9b5a-115">Vérification de la connectivité est actuellement en version préliminaire publique, toouse cette fonctionnalité, qu'il doit toobe inscrit.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-115">Connectivity check is currently in public preview, toouse this feature it needs toobe registered.</span></span> <span data-ttu-id="b9b5a-116">toodo, exécution hello suivant l’exemple de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="b9b5a-116">toodo this, run hello following CLI sample</span></span>

```azurecli 
az feature register --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck

az provider register --namespace Microsoft.Network 
``` 

<span data-ttu-id="b9b5a-117">l’inscription de hello tooverify a réussi, exécutez hello CLI commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b9b5a-117">tooverify hello registration was successful, run hello following CLI command:</span></span>

```azurecli
az feature show --namespace Microsoft.Network --name AllowNetworkWatcherConnectivityCheck 
```

<span data-ttu-id="b9b5a-118">Si la fonctionnalité de hello a été inscrit correctement, sortie de hello doit correspondre au suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="b9b5a-118">If hello feature was properly registered, hello output should match hello following:</span></span> 

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

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="b9b5a-119">Vérifiez la connectivité tooa virtual machine</span><span class="sxs-lookup"><span data-stu-id="b9b5a-119">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="b9b5a-120">Cet exemple vérifie l’ordinateur virtuel de destination de tooa connectivité via le port 80.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-120">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

### <a name="example"></a><span data-ttu-id="b9b5a-121">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9b5a-121">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-resource Database0 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="b9b5a-122">Réponse</span><span class="sxs-lookup"><span data-stu-id="b9b5a-122">Response</span></span>

<span data-ttu-id="b9b5a-123">Hello suivant la réponse est à partir de l’exemple précédent de hello.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-123">hello following response is from hello previous example.</span></span>  <span data-ttu-id="b9b5a-124">Dans cette réponse, hello `ConnectionStatus` est **inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-124">In this response, hello `ConnectionStatus` is **Unreachable**.</span></span> <span data-ttu-id="b9b5a-125">Vous pouvez voir que tous les hello sondes envoyées ayant échouées.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-125">You can see that all hello probes sent failed.</span></span> <span data-ttu-id="b9b5a-126">Échec de la connectivité de Hello au niveau de l’appliance virtuelle hello tooa échéance configurée par l’utilisateur `NetworkSecurityRule` nommé **UserRule_Port80**, configuré tooblock du trafic entrant sur le port 80.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-126">hello connectivity failed at hello virtual appliance due tooa user-configured `NetworkSecurityRule` named **UserRule_Port80**, configured tooblock incoming traffic on port 80.</span></span> <span data-ttu-id="b9b5a-127">Ces informations peuvent être utilisées tooresearch les problèmes de connexion.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-127">This information can be used tooresearch connection issues.</span></span>

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

## <a name="validate-routing-issues"></a><span data-ttu-id="b9b5a-128">Valider les problèmes de routage</span><span class="sxs-lookup"><span data-stu-id="b9b5a-128">Validate routing issues</span></span>

<span data-ttu-id="b9b5a-129">exemple de Hello vérifie la connectivité entre un ordinateur virtuel et un point de terminaison distant.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-129">hello example checks connectivity between a virtual machine and a remote endpoint.</span></span>

### <a name="example"></a><span data-ttu-id="b9b5a-130">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9b5a-130">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address 13.107.21.200 --dest-port 80
```

### <a name="response"></a><span data-ttu-id="b9b5a-131">Réponse</span><span class="sxs-lookup"><span data-stu-id="b9b5a-131">Response</span></span>

<span data-ttu-id="b9b5a-132">Dans l’exemple suivant de hello, hello `connectionStatus` est affiché comme **inaccessible**.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-132">In hello following example, hello `connectionStatus` is shown as **Unreachable**.</span></span> <span data-ttu-id="b9b5a-133">Bonjour `hops` plus d’informations, vous pouvez voir sous `issues` que le trafic de hello a été bloqué échéance tooa `UserDefinedRoute`.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-133">In hello `hops` details, you can see under `issues` that hello traffic was blocked due tooa `UserDefinedRoute`.</span></span>

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

## <a name="check-website-latency"></a><span data-ttu-id="b9b5a-134">Vérifier la latence du site Web</span><span class="sxs-lookup"><span data-stu-id="b9b5a-134">Check website latency</span></span>

<span data-ttu-id="b9b5a-135">Hello exemple suivant vérifie le site Web du tooa hello connectivité.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-135">hello following example checks hello connectivity tooa website.</span></span>

### <a name="example"></a><span data-ttu-id="b9b5a-136">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9b5a-136">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address http://bing.com --dest-port 80
```

### <a name="response"></a><span data-ttu-id="b9b5a-137">Réponse</span><span class="sxs-lookup"><span data-stu-id="b9b5a-137">Response</span></span>

<span data-ttu-id="b9b5a-138">Bonjour suivant la réponse, vous pouvez voir hello `connectionStatus` affiche sous la forme **joignable**.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-138">In hello following response, you can see hello `connectionStatus` shows as **Reachable**.</span></span> <span data-ttu-id="b9b5a-139">Lorsqu’une connexion est établie, les valeurs de latence sont fournies.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-139">When a connection is successful, latency values are provided.</span></span>

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

## <a name="check-connectivity-tooa-storage-endpoint"></a><span data-ttu-id="b9b5a-140">Vérifiez le point de terminaison de stockage de connectivité tooa</span><span class="sxs-lookup"><span data-stu-id="b9b5a-140">Check connectivity tooa storage endpoint</span></span>

<span data-ttu-id="b9b5a-141">Hello exemple suivant vérifie la hello connectivité à partir d’un compte de stockage de blog de l’ordinateur virtuel tooa.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-141">hello following example checks hello connectivity from a virtual machine tooa blog storage account.</span></span>

### <a name="example"></a><span data-ttu-id="b9b5a-142">Exemple</span><span class="sxs-lookup"><span data-stu-id="b9b5a-142">Example</span></span>

```azurecli
az network watcher test-connectivity --resource-group ContosoRG --source-resource MultiTierApp0 --dest-address https://contosoexamplesa.blob.core.windows.net/
```

### <a name="response"></a><span data-ttu-id="b9b5a-143">Réponse</span><span class="sxs-lookup"><span data-stu-id="b9b5a-143">Response</span></span>

<span data-ttu-id="b9b5a-144">Hello json suivant est hello exemple de réponse à partir de l’applet de commande précédente hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-144">hello following json is hello example response from running hello previous cmdlet.</span></span> <span data-ttu-id="b9b5a-145">Comme la vérification de hello est réussie, hello `connectionStatus` propriété s’affiche en tant que **joignable**.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-145">As hello check is successful, hello `connectionStatus` property shows as **Reachable**.</span></span>  <span data-ttu-id="b9b5a-146">Vous trouverez détails hello concernant le nombre de hello de blob de stockage hello sauts tooreach requis et la latence.</span><span class="sxs-lookup"><span data-stu-id="b9b5a-146">You are provided hello details regarding hello number of hops required tooreach hello storage blob and latency.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b9b5a-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b9b5a-147">Next steps</span></span>

<span data-ttu-id="b9b5a-148">Découvrez comment de captures de paquets de tooautomate d’alertes de l’ordinateur virtuel en consultant [créer une capture de paquets déclenchées alerte](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="b9b5a-148">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="b9b5a-149">Recherchez si certains types de trafic sont autorisés au sein ou en dehors de votre machine virtuelle en consultant [Check IP flow verify (Vérifier les flux IP)](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="b9b5a-149">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>
