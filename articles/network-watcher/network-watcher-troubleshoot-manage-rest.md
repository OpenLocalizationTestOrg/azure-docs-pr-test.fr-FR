---
title: "Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions par le biais d’Azure Network Watcher - REST | Microsoft Docs"
description: "Cette page explique comment résoudre les problèmes liés aux passerelles de réseau virtuel et aux connexions avec Azure Network Watcher à l’aide de REST"
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
ms.openlocfilehash: bc61be74d85a309c158716460b918baaf4fa94dc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher"></a><span data-ttu-id="6a364-103">Résoudre les problèmes liés à la passerelle de réseau virtuel et aux connexions à l’aide d’Azure Network Watcher</span><span class="sxs-lookup"><span data-stu-id="6a364-103">Troubleshoot Virtual Network gateway and Connections using Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="6a364-104">Portail</span><span class="sxs-lookup"><span data-stu-id="6a364-104">Portal</span></span>](network-watcher-troubleshoot-manage-portal.md)
> - [<span data-ttu-id="6a364-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6a364-105">PowerShell</span></span>](network-watcher-troubleshoot-manage-powershell.md)
> - [<span data-ttu-id="6a364-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="6a364-106">CLI 1.0</span></span>](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [<span data-ttu-id="6a364-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6a364-107">CLI 2.0</span></span>](network-watcher-troubleshoot-manage-cli.md)
> - [<span data-ttu-id="6a364-108">API REST</span><span class="sxs-lookup"><span data-stu-id="6a364-108">REST API</span></span>](network-watcher-troubleshoot-manage-rest.md)

<span data-ttu-id="6a364-109">Le service Network Watcher offre de nombreuses fonctionnalités en lien avec la bonne compréhension de vos ressources réseau dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6a364-109">Network Watcher provides many capabilities as it relates to understanding your network resources in Azure.</span></span> <span data-ttu-id="6a364-110">Il permet notamment de résoudre les problèmes liés aux ressources.</span><span class="sxs-lookup"><span data-stu-id="6a364-110">One of these capabilities is resource troubleshooting.</span></span> <span data-ttu-id="6a364-111">Vous pouvez appeler la solution de résolution des problèmes de ressources par le biais du portail, de PowerShell, de l’interface de ligne de commande ou de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="6a364-111">Resource troubleshooting can be called through the portal, PowerShell, CLI, or REST API.</span></span> <span data-ttu-id="6a364-112">Lorsque cette fonctionnalité est appelée, Network Watcher inspecte l’intégrité d’une passerelle de réseau virtuel ou d’une connexion et renvoie ses résultats.</span><span class="sxs-lookup"><span data-stu-id="6a364-112">When called, Network Watcher inspects the health of a Virtual Network Gateway or a Connection and returns its findings.</span></span>

<span data-ttu-id="6a364-113">Cet article passe en revue les différentes tâches de gestion actuellement disponibles pour la résolution des problèmes de ressources.</span><span class="sxs-lookup"><span data-stu-id="6a364-113">This article takes you through the different management tasks that are currently available for resource troubleshooting.</span></span>

- [<span data-ttu-id="6a364-114">**Résoudre les problèmes d’une passerelle de réseau virtuel**</span><span class="sxs-lookup"><span data-stu-id="6a364-114">**Troubleshoot a Virtual Network gateway**</span></span>](#troubleshoot-a-virtual-network-gateway)
- [<span data-ttu-id="6a364-115">**Résoudre les problèmes d’une connexion**</span><span class="sxs-lookup"><span data-stu-id="6a364-115">**Troubleshoot a Connection**</span></span>](#troubleshoot-connections)

## <a name="before-you-begin"></a><span data-ttu-id="6a364-116">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6a364-116">Before you begin</span></span>

<span data-ttu-id="6a364-117">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a364-117">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="6a364-118">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="6a364-118">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="6a364-119">Ce scénario suppose que vous ayez déjà suivi la procédure décrite dans [Créer une instance d’Azure Network Watcher](network-watcher-create.md) pour créer un Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="6a364-119">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

<span data-ttu-id="6a364-120">Vous trouverez la liste des types de passerelles pris en charge sur la page [Types de passerelles pris en charge](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span><span class="sxs-lookup"><span data-stu-id="6a364-120">For a list of supported gateway types visit, [Supported Gateway types](network-watcher-troubleshoot-overview.md#supported-gateway-types).</span></span>

## <a name="overview"></a><span data-ttu-id="6a364-121">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6a364-121">Overview</span></span>

<span data-ttu-id="6a364-122">Les fonctionnalités de dépannage de Network Watcher permettent de résoudre les problèmes qui surviennent avec les passerelles de réseau virtuel et les connexions.</span><span class="sxs-lookup"><span data-stu-id="6a364-122">Network Watcher troubleshooting provides the ability troubleshoot issues that arise with Virtual Network gateways and Connections.</span></span> <span data-ttu-id="6a364-123">Lorsqu’une demande de résolution des problèmes liés aux ressources est effectuée, les journaux sont interrogés et inspectés.</span><span class="sxs-lookup"><span data-stu-id="6a364-123">When a request is made to the resource troubleshooting, logs are querying and inspected.</span></span> <span data-ttu-id="6a364-124">Lorsque l’inspection est terminée, les résultats sont renvoyés.</span><span class="sxs-lookup"><span data-stu-id="6a364-124">When inspection is complete, the results are returned.</span></span> <span data-ttu-id="6a364-125">L’exécution des demandes de l’API de résolution des problèmes nécessite un certain temps : vous devrez peut-être patienter plusieurs minutes avant d’obtenir un résultat.</span><span class="sxs-lookup"><span data-stu-id="6a364-125">The troubleshoot API requests are long running requests, which could take multiple minutes to return a result.</span></span> <span data-ttu-id="6a364-126">Les journaux sont stockés dans un conteneur sur un compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="6a364-126">Logs are stored in a container on a storage account.</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="6a364-127">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="6a364-127">Log in with ARMClient</span></span>

```PowerShell
armclient login
```

## <a name="troubleshoot-a-virtual-network-gateway"></a><span data-ttu-id="6a364-128">Résoudre les problèmes d’une passerelle de réseau virtuel</span><span class="sxs-lookup"><span data-stu-id="6a364-128">Troubleshoot a Virtual Network gateway</span></span>


### <a name="post-the-troubleshoot-request"></a><span data-ttu-id="6a364-129">Publier la demande de résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="6a364-129">POST the troubleshoot request</span></span>

<span data-ttu-id="6a364-130">L’exemple ci-après interroge l’état d’une passerelle de réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="6a364-130">The following example queries the status of a Virtual Network gateway.</span></span>

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

<span data-ttu-id="6a364-131">Étant donné que l’exécution de cette opération demande un certain temps, l’URI d’interrogation de l’opération et l’URI du résultat sont renvoyés dans l’en-tête de réponse, comme indiqué dans la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="6a364-131">Since this operation is long running, the URI for querying the operation and the URI for the result is returned in the response header as shown in the following response:</span></span>

<span data-ttu-id="6a364-132">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="6a364-132">**Important Values**</span></span>

* <span data-ttu-id="6a364-133">**Azure-AsyncOperation** : cette propriété contient l’URI d’interrogation de l’opération de résolution des problèmes Async.</span><span class="sxs-lookup"><span data-stu-id="6a364-133">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="6a364-134">**Location** : cette propriété contient l’URI de l’emplacement des résultats une fois que l’opération a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a364-134">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="6a364-135">Interroger l’état d’achèvement de l’opération asynchrone</span><span class="sxs-lookup"><span data-stu-id="6a364-135">Query the async operation for completion</span></span>

<span data-ttu-id="6a364-136">Utilisez l’URI operations pour connaître l’état d’avancement de l’opération, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6a364-136">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="6a364-137">Lorsque l’opération est en cours, la réponse indique la valeur **InProgress**, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6a364-137">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="6a364-138">Lorsque l’opération est terminée, elle prend l’état **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="6a364-138">When the operation is complete the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

### <a name="retrieve-the-results"></a><span data-ttu-id="6a364-139">Récupérer les résultats</span><span class="sxs-lookup"><span data-stu-id="6a364-139">Retrieve the results</span></span>

<span data-ttu-id="6a364-140">Une fois que l’état **Succeeded** est renvoyé, appelez une méthode GET sur l’URI operationResult pour récupérer les résultats.</span><span class="sxs-lookup"><span data-stu-id="6a364-140">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/8a1167b7-6768-4ac1-85dc-703c9c9b9247?api-version=2016-03-30"
```

<span data-ttu-id="6a364-141">Les réponses ci-après sont des exemples de réponses dégradées classiques renvoyées lors de l’interrogation des résultats de la résolution des problèmes d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="6a364-141">The following responses are examples of a typical degraded response returned when querying the results of troubleshooting a gateway.</span></span> <span data-ttu-id="6a364-142">Pour obtenir des précisions sur la signification des propriétés figurant dans la réponse, consultez la section [Compréhension des résultats](#understanding-the-results).</span><span class="sxs-lookup"><span data-stu-id="6a364-142">See [Understanding the results](#understanding-the-results) to get clarification on what the properties in the response mean.</span></span>

```json
{
  "startTime": "2017-01-12T10:31:41.562646-08:00",
  "endTime": "2017-01-12T18:31:48.677Z",
  "code": "Degraded",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN Gateway"
        },
        {
          "actionText": "If your VPN gateway isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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


## <a name="troubleshoot-connections"></a><span data-ttu-id="6a364-143">Résoudre les problèmes des connexions</span><span class="sxs-lookup"><span data-stu-id="6a364-143">Troubleshoot Connections</span></span>

<span data-ttu-id="6a364-144">L’exemple ci-après interroge l’état d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="6a364-144">The following example queries the status of a Connection.</span></span>

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
> <span data-ttu-id="6a364-145">L’opération de résolution des problèmes ne peut pas s’exécuter en parallèle sur une connexion et sur ses passerelles correspondantes.</span><span class="sxs-lookup"><span data-stu-id="6a364-145">The troubleshoot operation cannot be run in parallel on a Connection and its corresponding gateways.</span></span> <span data-ttu-id="6a364-146">L’opération doit être achevée avant d’être exécutée sur la ressource précédente.</span><span class="sxs-lookup"><span data-stu-id="6a364-146">The operation must complete prior to running it on the previous resource.</span></span>

<span data-ttu-id="6a364-147">Étant donné que cette transaction demande un certain temps, l’URI d’interrogation de l’opération et l’URI du résultat sont renvoyés dans l’en-tête de réponse comme indiqué dans la réponse suivante :</span><span class="sxs-lookup"><span data-stu-id="6a364-147">Since this is a long running transaction, in the response header, the URI for querying the operation and the URI for the result is returned as shown in the following response:</span></span>

<span data-ttu-id="6a364-148">**Valeurs importantes**</span><span class="sxs-lookup"><span data-stu-id="6a364-148">**Important Values**</span></span>

* <span data-ttu-id="6a364-149">**Azure-AsyncOperation** : cette propriété contient l’URI d’interrogation de l’opération de résolution des problèmes Async.</span><span class="sxs-lookup"><span data-stu-id="6a364-149">**Azure-AsyncOperation** - This property contains the URI to query the Async troubleshoot operation</span></span>
* <span data-ttu-id="6a364-150">**Location** : cette propriété contient l’URI de l’emplacement des résultats une fois que l’opération a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="6a364-150">**Location** - This property contains the URI where the results are when the operation is complete</span></span>

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

### <a name="query-the-async-operation-for-completion"></a><span data-ttu-id="6a364-151">Interroger l’état d’achèvement de l’opération asynchrone</span><span class="sxs-lookup"><span data-stu-id="6a364-151">Query the async operation for completion</span></span>

<span data-ttu-id="6a364-152">Utilisez l’URI operations pour connaître l’état d’avancement de l’opération, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6a364-152">Use the operations URI to query for the progress of the operation as seen in the following example:</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operations/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="6a364-153">Lorsque l’opération est en cours, la réponse indique la valeur **InProgress**, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6a364-153">While the operation is in progress, the response shows **InProgress** as seen in the following example:</span></span>

```json
{
  "status": "InProgress"
}
```

<span data-ttu-id="6a364-154">Lorsque l’opération est terminée, elle prend l’état **Succeeded**.</span><span class="sxs-lookup"><span data-stu-id="6a364-154">When the operation is complete, the status changes to **Succeeded**.</span></span>

```json
{
  "status": "Succeeded"
}
```

<span data-ttu-id="6a364-155">Les réponses ci-après sont des exemples de réponses classiques renvoyées lors de l’interrogation des résultats de la résolution des problèmes d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="6a364-155">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

### <a name="retrieve-the-results"></a><span data-ttu-id="6a364-156">Récupérer les résultats</span><span class="sxs-lookup"><span data-stu-id="6a364-156">Retrieve the results</span></span>

<span data-ttu-id="6a364-157">Une fois que l’état **Succeeded** est renvoyé, appelez une méthode GET sur l’URI operationResult pour récupérer les résultats.</span><span class="sxs-lookup"><span data-stu-id="6a364-157">Once the status returned is **Succeeded**, call a GET Method on the operationResult URI to retrieve the results.</span></span>

```powershell
armclient get "https://management.azure.com/subscriptions/00000000-0000-0000-0000-000000000000/providers/Microsoft.Network/locations/westcentralus/operationResults/843b1c31-4717-4fdd-b7a6-4c786ca9c501?api-version=2016-03-30"
```

<span data-ttu-id="6a364-158">Les réponses ci-après sont des exemples de réponses classiques renvoyées lors de l’interrogation des résultats de la résolution des problèmes d’une connexion.</span><span class="sxs-lookup"><span data-stu-id="6a364-158">The following responses are examples of a typical response returned when querying the results of troubleshooting a Connection.</span></span>

```json
{
  "startTime": "2017-01-12T14:09:19.1215346-08:00",
  "endTime": "2017-01-12T22:09:23.747Z",
  "code": "UnHealthy",
  "results": [
    {
      "id": "PlatformInActive",
      "summary": "We are sorry, your VPN gateway is in standby mode",
      "detail": "During this time the gateway will not initiate or accept VPN connections with on premises VPN devices or other Azure VPN Gateways. This 
is a transient state while the Azure platform is being updated.",
      "recommendedActions": [
        {
          "actionText": "If the condition persists, please try resetting your Azure VPN gateway",
          "actionUri": "https://azure.microsoft.com/en-us/documentation/articles/vpn-gateway-resetgw-classic/",
          "actionUriText": "resetting the VPN gateway"
        },
        {
          "actionText": "If your VPN Connection isn't up and running by the expected resolution time, contact support",
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
          "actionText": "If you are still experience problems with the VPN gateway, please try resetting the VPN gateway.",
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

## <a name="understanding-the-results"></a><span data-ttu-id="6a364-159">Compréhension des résultats</span><span class="sxs-lookup"><span data-stu-id="6a364-159">Understanding the results</span></span>

<span data-ttu-id="6a364-160">Le texte d’action fournit des indications générales sur la façon de résoudre le problème.</span><span class="sxs-lookup"><span data-stu-id="6a364-160">The action text provides general guidance on how to resolve the issue.</span></span> <span data-ttu-id="6a364-161">Si une action peut être entreprise pour résoudre le problème, un lien est fourni avec des indications supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="6a364-161">If an action can be taken for the issue, a link is provided with additional guidance.</span></span> <span data-ttu-id="6a364-162">En l’absence d’indications supplémentaires, la réponse fournit l’URL permettant d’ouvrir un dossier de support.</span><span class="sxs-lookup"><span data-stu-id="6a364-162">In the case where there is no additional guidance, the response provides the url to open a support case.</span></span>  <span data-ttu-id="6a364-163">Pour plus d’informations sur les propriétés de la réponse et sur ce qu’elle contient, consultez [Network Watcher Troubleshoot overview (Vue d’ensemble de la résolution des problèmes Network Watcher)](network-watcher-troubleshoot-overview.md)</span><span class="sxs-lookup"><span data-stu-id="6a364-163">For more information about the properties of the response and what is included, visit [Network Watcher Troubleshoot overview](network-watcher-troubleshoot-overview.md)</span></span>

<span data-ttu-id="6a364-164">Pour obtenir des instructions de téléchargement des fichiers à partir des comptes de stockage Azure, consultez [Prise en main du stockage d’objets blob Azure à l’aide de .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="6a364-164">For instructions on downloading files from azure storage accounts, refer to [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="6a364-165">L’explorateur de stockage peut aussi être utilisé.</span><span class="sxs-lookup"><span data-stu-id="6a364-165">Another tool that can be used is Storage Explorer.</span></span> <span data-ttu-id="6a364-166">Pour en savoir plus sur l’explorateur de stockage, cliquez sur le lien suivant : [Explorateur de stockage](http://storageexplorer.com/)</span><span class="sxs-lookup"><span data-stu-id="6a364-166">More information about Storage Explorer can be found here at the following link: [Storage Explorer](http://storageexplorer.com/)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a364-167">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6a364-167">Next steps</span></span>

<span data-ttu-id="6a364-168">Si les paramètres ont été modifiés et arrêtent la connectivité VPN, consultez la page [Gérer les groupes de sécurité réseau à partir du portail](../virtual-network/virtual-network-manage-nsg-arm-portal.md) afin d’effectuer le suivi du groupe de sécurité réseau et des règles de sécurité pouvant être concernés.</span><span class="sxs-lookup"><span data-stu-id="6a364-168">If settings have been changed that stop VPN connectivity, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) to track down the network security group and security rules that may be in question.</span></span>
