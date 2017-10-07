---
title: "aaaTroubleshoot passerelle de réseau virtuel et les connexions à l’aide de l’Observateur réseau de Azure - REST | Documents Microsoft"
description: "Cette page explique comment tootroubleshoot les passerelles de réseau virtuel et les connexions à l’aide de l’Observateur réseau Azure REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e4d5f195-b839-4394-94ef-a04192766e55
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: cc89b46643fdbfefe53727b45d6b7d06914b58a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="389a8-103">Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions à l’aide d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="389a8-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="389a8-104">Portail</span><span class="sxs-lookup"><span data-stu-id="389a8-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="389a8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="389a8-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="389a8-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="389a8-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="389a8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="389a8-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="389a8-108">API REST</span><span class="sxs-lookup"><span data-stu-id="389a8-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="389a8-109">Observateur réseau fournit de nombreuses fonctionnalités en matière de toounderstanding vos ressources réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="389a8-109">Network Watcher provides many capabilities as it relates toounderstanding your network resources in Azure.</span></span> <span data-ttu-id="389a8-110">Il permet notamment de résoudre les problèmes liés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="389a8-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="389a8-111">Résolution des problèmes de ressource peuvent être appelée via le portail de hello, PowerShell, CLI ou API REST.</span><span class="sxs-lookup"><span data-stu-id="389a8-111">Resource troubleshooting can be called through hello portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="389a8-112">Lorsqu’elle est appelée, Observateur réseau inspecte le contrôle d’intégrité hello d’une passerelle de réseau virtuel ou d’une connexion et retourne les résultats obtenus.</span><span class="sxs-lookup"><span data-stu-id="389a8-112">When called, Network Watcher inspects hello health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="389a8-113">Cet article vous guide tout au long de hello différentes tâches de gestion qui sont actuellement disponibles pour le dépannage de la ressource.</span><span class="sxs-lookup"><span data-stu-id="389a8-113">This article takes you through hello different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="389a8-114">**Résoudre les problèmes d’une passerelle de réseau virtuel**</span><span class="sxs-lookup"><span data-stu-id="389a8-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="389a8-115">**Résoudre les problèmes d’une connexion**</span><span class="sxs-lookup"><span data-stu-id="389a8-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="389a8-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="389a8-116">Before you begin</span></span>

<span data-ttu-id="389a8-117">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="389a8-117">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="389a8-118">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="389a8-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="389a8-119">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="389a8-119">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

<span data-ttu-id="389a8-120">Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="389a8-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="389a8-121">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="389a8-121">Overview</span></span>

<span data-ttu-id="389a8-122">Dépannage de l’Observateur réseau permet de hello résoudre les problèmes qui surviennent avec les connexions et les passerelles de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="389a8-122">Network Watcher troubleshooting provides hello ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="389a8-123">Lorsqu’une demande est faite toohello ressource résolution des problèmes, les journaux interrogent et inspecté.</span><span class="sxs-lookup"><span data-stu-id="389a8-123">When a request is made toohello resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="389a8-124">Lors de l’inspection est terminée, les résultats de hello sont retournés.</span><span class="sxs-lookup"><span data-stu-id="389a8-124">When inspection is complete, hello results are returned.</span></span> <span data-ttu-id="389a8-125">résoudre les problèmes de Hello API requêtes sont longs de requêtes, ce qui peut prendre plusieurs minutes tooreturn un résultat d’exécution.</span><span class="sxs-lookup"><span data-stu-id="389a8-125">hello troubleshoot API requests are long running requests, which could take multiple minutes tooreturn a result.</span></span> <span data-ttu-id="389a8-126">Les journaux sont stockés dans un conteneur sur un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="389a8-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="389a8-127">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="389a8-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="389a8-128">Résoudre les problèmes d’une passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="389a8-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-hello-troubleshoot-request"></a><span data-ttu-id="389a8-129">Résoudre les problèmes de hello POST demande</span><span class="sxs-lookup"><span data-stu-id="389a8-129">POST hello troubleshoot request</span></span>

<span data-ttu-id="389a8-130">Hello suivant l’état de hello exemple requêtes d’une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="389a8-130">hello following example queries hello status of a Virtual Network gateway.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$vnetGatewayName = "ContosoVNETGateway"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @"
{
'TargetResourceId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/virtualNetworkGateways/${vnetGatewayName}',
'Properties': {
'StorageId': '/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}',
'StoragePath': 'https://${storageAccountName}.blob.core.windows.net/${containerName}'
}
}
"@

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

<span data-ttu-id="389a8-131">Étant donné que cette opération est longue en cours d’exécution, hello URI pour interroger l’opération de hello et hello URI pour le résultat de hello est retourné dans l’en-tête de réponse hello comme indiqué dans hello suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="389a8-131">Since this operation is long running, hello URI for querying hello operation and hello URI for hello result is returned in hello response header as shown in hello following response:</span></span>

<span data-ttu-id="389a8-132">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="389a8-132">**Important Values**</span></span>

* <span data-ttu-id="389a8-133">**Azure-AsyncOperation** -cette propriété contient hello URI tooquery hello Async résoudre les problèmes d’opération</span><span class="sxs-lookup"><span data-stu-id="389a8-133">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="389a8-134">**Emplacement** -cette propriété contient hello URI où hello résultats sont lorsque hello l’opération est terminée</span><span class="sxs-lookup"><span data-stu-id="389a8-134">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="389a8-135">Opération asynchrone de hello pour l’exécution de requête</span><span class="sxs-lookup"><span data-stu-id="389a8-135">Query hello async operation for completion</span></span>

<span data-ttu-id="389a8-136">Utilisez hello opérations URI tooquery pour la progression de l’opération de hello hello comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="389a8-136">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="389a8-137">Lors de l’opération de hello est en cours d’exécution, hello réponse montre **InProgress** comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="389a8-137">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="389a8-138">Lorsque les opération hello sont changements d’état terminé hello trop**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="389a8-138">When hello operation is complete hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-hello-results"></a><span data-ttu-id="389a8-139">Récupérer les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="389a8-139">Retrieve hello results</span></span>

<span data-ttu-id="389a8-140">Une fois que l’état de hello retournée est **Succeeded**, appelez une méthode GET sur hello operationResult URI tooretrieve les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="389a8-140">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="389a8-141">Hello réponses suivantes sont des exemples d’une réponse détériorée classique retourné lors de l’interrogation des résultats hello de résolution des problèmes d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="389a8-141">hello following responses are examples of a typical degraded response returned when querying hello results of troubleshooting a gateway.</span></span> <span data-ttu-id="389a8-142">Consultez [présentation des résultats de hello](#understanding-the-results) tooget des précisions sur les propriétés hello dans moyenne de réponse hello.</span><span class="sxs-lookup"><span data-stu-id="389a8-142">See [Understanding hello results](#understanding-the-results) tooget clarification on what hello properties in hello response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN gateway is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```


## <a name="troubleshoot-connections"></a><span data-ttu-id="389a8-143">Résoudre les problèmes des connexions</span><span class="sxs-lookup"><span data-stu-id="389a8-143">Troubleshoot Connections</span></span>

<span data-ttu-id="389a8-144">Hello suivant l’état de hello exemple requêtes d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="389a8-144">hello following example queries hello status of a Connection.</span></span>

```powershell

$subscriptionId = "00000000-0000-0000-0000-000000000000"
$resourceGroupName = "ContosoRG"
$NWresourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$connectionName = "VNET2toVNET1Connection"
$storageAccountName = "contososa"
$containerName = "gwlogs"
$requestBody = @{
"TargetResourceId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Network/connections/${connectionName}",
"Properties": {
"StorageId": "/subscriptions/${subscriptionId}/resourceGroups/${resourceGroupName}/providers/Microsoft.Storage/storageAccounts/${storageAccountName}",
"StoragePath": "https://${storageAccountName}.blob.core.windows.net/${containerName}"
}

}
armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${NWresourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/troubleshoot?api-version=2016-03-30 "
```

> [!NOTE]
> <span data-ttu-id="389a8-145">Hello résoudre l’opération ne peut pas être exécutée en parallèle sur une connexion et ses passerelles correspondants.</span><span class="sxs-lookup"><span data-stu-id="389a8-145">hello troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="389a8-146">Hello opération doit être réalisée toorunning préalable sur la ressource précédente hello.</span><span class="sxs-lookup"><span data-stu-id="389a8-146">hello operation must complete prior toorunning it on hello previous resource.</span></span>

<span data-ttu-id="389a8-147">Puisqu’il s’agit d’une transaction à long terme, dans l’en-tête de réponse hello, hello URI pour interroger l’opération de hello et hello URI pour le résultat de hello est renvoyé comme Bonjour suivant la réponse :</span><span class="sxs-lookup"><span data-stu-id="389a8-147">Since this is a long running transaction, in hello response header, hello URI for querying hello operation and hello URI for hello result is returned as shown in hello following response:</span></span>

<span data-ttu-id="389a8-148">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="389a8-148">**Important Values**</span></span>

* <span data-ttu-id="389a8-149">**Azure-AsyncOperation** -cette propriété contient hello URI tooquery hello Async résoudre les problèmes d’opération</span><span class="sxs-lookup"><span data-stu-id="389a8-149">**Azure-AsyncOperation** - This property contains hello URI tooquery hello Async troubleshoot operation</span></span>
* <span data-ttu-id="389a8-150">**Emplacement** -cette propriété contient hello URI où hello résultats sont lorsque hello l’opération est terminée</span><span class="sxs-lookup"><span data-stu-id="389a8-150">**Location** - This property contains hello URI where hello results are when hello operation is complete</span></span>

```
HTTP/1.1 202 Accepted
Pragma: no-cache
Retry-After: 10
x-ms-request-id: 8a1167b7-6768-4ac1-85dc-703c9c9b9247
Azure-AsyncOperation: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Strict-Transport-Security: max-age=31536000; includeSubDomains
Cache-Control: no-cache
Location: https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30
Server: Microsoft-HTTPAPI/2.0; Microsoft-HTTPAPI/2.0
x-ms-ratelimit-remaining-subscription-writes: 1199
x-ms-correlation-request-id: 4364d88a-bd08-422c-a716-dbb0cdc99f7b
x-ms-routing-request-id: NORTHCENTRALUS:20170112T183202Z:4364d88a-bd08-422c-a716-dbb0cdc99f7b
Date: Thu, 12 Jan 2017 18:32:01 GMT

null
```

### <a name="query-hello-async-operation-for-completion"></a><span data-ttu-id="389a8-151">Opération asynchrone de hello pour l’exécution de requête</span><span class="sxs-lookup"><span data-stu-id="389a8-151">Query hello async operation for completion</span></span>

<span data-ttu-id="389a8-152">Utilisez hello opérations URI tooquery pour la progression de l’opération de hello hello comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="389a8-152">Use hello operations URI tooquery for hello progress of hello operation as seen in hello following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="389a8-153">Lors de l’opération de hello est en cours d’exécution, hello réponse montre **InProgress** comme Bonjour l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="389a8-153">While hello operation is in progress, hello response shows **InProgress** as seen in hello following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="389a8-154">Lors de l’opération de hello est terminée, hello devient trop**Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="389a8-154">When hello operation is complete, hello status changes too**Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="389a8-155">Hello réponses suivantes sont des exemples d’une réponse de type retourné lors de l’interrogation des résultats hello du dépannage d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="389a8-155">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

### <a name="retrieve-hello-results"></a><span data-ttu-id="389a8-156">Récupérer les résultats de hello</span><span class="sxs-lookup"><span data-stu-id="389a8-156">Retrieve hello results</span></span>

<span data-ttu-id="389a8-157">Une fois que l’état de hello retournée est **Succeeded**, appelez une méthode GET sur hello operationResult URI tooretrieve les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="389a8-157">Once hello status returned is **Succeeded**, call a GET Method on hello operationResult URI tooretrieve hello results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="389a8-158">Hello réponses suivantes sont des exemples d’une réponse de type retourné lors de l’interrogation des résultats hello du dépannage d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="389a8-158">hello following responses are examples of a typical response returned when querying hello results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time hello gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while hello Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If hello condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting hello VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by hello expected resolution time, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    },
    {
      "id": "NoFault",
      "summary": "This VPN Connection is running normally",
      "detail": "There aren't any known Azure platform problems affecting this VPN Connection",
      "recommendedActions": [
        {
          "actionText": "If you are still experience problems with hello VPN gateway, please try resetting hello VPN gateway.",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting VPN gateway"
        },
        {
          "actionText": "If you are experiencing problems you believe are caused by Azure, contact support",
          "actionUri": "http://azure.microsoft.com/support",
          "actionUriText": "contact support"
        }
      ]
    }
  ]
}
```

## <a name="understanding-hello-results"></a><span data-ttu-id="389a8-159">Présentation des résultats de hello</span><span class="sxs-lookup"><span data-stu-id="389a8-159">Understanding hello results</span></span>

<span data-ttu-id="389a8-160">texte d’action Hello fournit des indications générales sur la façon dont tooresolve hello problème.</span><span class="sxs-lookup"><span data-stu-id="389a8-160">hello action text provides general guidance on how tooresolve hello issue.</span></span> <span data-ttu-id="389a8-161">Si le problème de hello peut entreprendre une action, un lien est fourni avec des instructions supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="389a8-161">If an action can be taken for hello issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="389a8-162">Dans le cas de hello où il n’existe pas d’instructions supplémentaires, réponse de hello fournit hello url tooopen un cas de prise en charge.</span><span class="sxs-lookup"><span data-stu-id="389a8-162">In hello case where there is no additional guidance, hello response provides hello url tooopen a support case.</span></span>  <span data-ttu-id="389a8-163">Pour plus d’informations sur les propriétés de hello de réponse de hello et ce qui est inclus, visitez [vue d’ensemble de la résolution de l’Observateur réseau](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="389a8-163">For more information about hello properties of hello response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="389a8-164">Pour obtenir des instructions sur le téléchargement de fichiers à partir des comptes de stockage azure, consultez trop[prise en main le stockage Blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="389a8-164">For instructions on downloading files from azure storage accounts, refer too[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="389a8-165">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="389a8-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="389a8-166">Plus d’informations sur l’Explorateur de stockage trouverez ici hello lien : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="389a8-166">More information about Storage Explorer can be found here at hello following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="389a8-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="389a8-167">Next steps</span></span>

<span data-ttu-id="389a8-168">Si les paramètres ont été modifiés qu’arrêter la connectivité VPN, consultez [gérer les groupes de sécurité réseau](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack vers le bas hello sécurité et groupe de règles de sécurité réseau qui peuvent être en question.</span><span class="sxs-lookup"><span data-stu-id="389a8-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that may be in question.</span></span>
