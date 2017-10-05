---
title: "Gérer les journaux des flux de groupe de sécurité réseau avec Azure Network Watcher - API REST | Microsoft Docs"
description: "Cette page explique comment gérer les journaux des flux de groupe de sécurité réseau dans Azure Network Watcher avec l’API REST"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2ab25379-0fd3-4bfe-9d82-425dfc7ad6bb
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: c89a2ab4c39978771c940a819493b4e2283d5f9f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="ef01b-103">Configuration des journaux des flux de groupe de sécurité réseau avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="ef01b-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="ef01b-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef01b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="ef01b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ef01b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="ef01b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ef01b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="ef01b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ef01b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="ef01b-108">API REST</span><span class="sxs-lookup"><span data-stu-id="ef01b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="ef01b-109">Les journaux des flux de groupe de sécurité réseau désignent une fonctionnalité de Network Watcher qui vous permet de visualiser des informations sur le trafic IP d’entrée et de sortie par le biais d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ef01b-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="ef01b-110">Ces flux de journaux sont écrits au format json et affichent les flux entrants et sortants en fonction de la règle, la carte réseau à laquelle le flux s’applique, des informations à 5 tuples sur le flux (adresse IP source/de destination, port source/de destination, protocole), ainsi que l’autorisation ou le refus du trafic.</span><span class="sxs-lookup"><span data-stu-id="ef01b-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ef01b-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ef01b-111">Before you begin</span></span>

<span data-ttu-id="ef01b-112">ARMclient permet d’appeler l’API REST à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ef01b-112">ARMclient is used to call the REST API using PowerShell.</span></span> <span data-ttu-id="ef01b-113">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="ef01b-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="ef01b-114">Ce scénario repose sur l’hypothèse que vous avez déjà suivi la procédure décrite dans l’article [Create a Network Watcher (Créer une instance Network Watcher)](network-watcher-create.md) pour créer une instance Network Watcher.</span><span class="sxs-lookup"><span data-stu-id="ef01b-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="ef01b-115">Pour les appels de l’API REST de Network Watcher, le nom du groupe de ressources dans l’URI de requête correspond au groupe de ressources qui contient Network Watcher, et non les ressources sur lesquelles vous exécutez les actions de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="ef01b-115">For Network Watcher REST API calls the resource group name in the request URI is the resource group that contains the Network Watcher, not the resources you are performing the diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="ef01b-116">Scénario</span><span class="sxs-lookup"><span data-stu-id="ef01b-116">Scenario</span></span>

<span data-ttu-id="ef01b-117">Le scénario décrit dans cet article vous indique comment activer, désactiver et interroger les journaux des flux à l’aide de l’API REST.</span><span class="sxs-lookup"><span data-stu-id="ef01b-117">The scenario covered in this article shows you how to enable, disable, and query flow logs using the REST API.</span></span> <span data-ttu-id="ef01b-118">Pour plus d’informations sur la journalisation des flux de groupe de sécurité réseau, consultez l’article [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md) (Présentation de la journalisation des flux de groupe de sécurité réseau).</span><span class="sxs-lookup"><span data-stu-id="ef01b-118">To learn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="ef01b-119">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="ef01b-119">In this scenario, you will:</span></span>

* <span data-ttu-id="ef01b-120">Activer les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="ef01b-120">Enable flow logs</span></span>
* <span data-ttu-id="ef01b-121">Désactiver les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="ef01b-121">Disable flow logs</span></span>
* <span data-ttu-id="ef01b-122">Interroger l’état des journaux des flux</span><span class="sxs-lookup"><span data-stu-id="ef01b-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="ef01b-123">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="ef01b-123">Log in with ARMClient</span></span>

<span data-ttu-id="ef01b-124">Connectez-vous à armclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="ef01b-124">Log in to armclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="ef01b-125">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="ef01b-125">Register Insights provider</span></span>

<span data-ttu-id="ef01b-126">Pour que les journaux de flux puissent correctement fonctionner, le fournisseur **Microsoft.Insights** doit être inscrit.</span><span class="sxs-lookup"><span data-stu-id="ef01b-126">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="ef01b-127">Si vous ne savez pas si le fournisseur **Microsoft.Insights** est inscrit, exécutez le script suivant.</span><span class="sxs-lookup"><span data-stu-id="ef01b-127">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="ef01b-128">Activer les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ef01b-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="ef01b-129">La commande d’activation des journaux des flux est illustrée dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="ef01b-129">The command to enable flow logs is shown in the following example:</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'true',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="ef01b-130">La réponse renvoyée par l’exemple précédent est la suivante :</span><span class="sxs-lookup"><span data-stu-id="ef01b-130">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="ef01b-131">Désactiver les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="ef01b-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="ef01b-132">Utilisez l’exemple ci-après pour désactiver les journaux des flux.</span><span class="sxs-lookup"><span data-stu-id="ef01b-132">Use the following example to disable flow logs.</span></span> <span data-ttu-id="ef01b-133">L’appel est identique à l’activation des journaux des flux, à l’exception de la définition de la propriété enabled sur la valeur **false**.</span><span class="sxs-lookup"><span data-stu-id="ef01b-133">The call is the same as enabling flow logs, except **false** is set for the enabled property.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$storageId = "/subscriptions/00000000-0000-0000-0000-000000000000/{resourceGroupName/providers/Microsoft.Storage/storageAccounts/{saName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
    'properties': {
    'storageId': '${storageId}',
    'enabled': 'false',
    'retentionPolicy' : {
            days: 5,
            enabled: true
        }
    }
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/configureFlowLog?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="ef01b-134">La réponse renvoyée par l’exemple précédent est la suivante :</span><span class="sxs-lookup"><span data-stu-id="ef01b-134">The response returned from the preceding example is as follows:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": false,
    "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="query-flow-logs"></a><span data-ttu-id="ef01b-135">Interroger les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="ef01b-135">Query flow logs</span></span>

<span data-ttu-id="ef01b-136">L’appel REST ci-après interroge l’état des journaux des flux sur un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="ef01b-136">The following REST call queries the status of flow logs on a Network Security Group.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
$targetUri = "" # example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName/providers/Microsoft.Network/networkSecurityGroups/{nsgName}"
$resourceGroupName = "NetworkWatcherRG"
$networkWatcherName = "NetworkWatcher_westcentralus"
$requestBody = @"
{
    'targetResourceId': '${targetUri}',
}
"@

armclient post "https://management.azure.com/subscriptions/${subscriptionId}/ResourceGroups/${resourceGroupName}/providers/Microsoft.Network/networkWatchers/${networkWatcherName}/queryFlowLogStatus?api-version=2016-12-01" $requestBody
```

<span data-ttu-id="ef01b-137">Voici un exemple de la réponse renvoyée :</span><span class="sxs-lookup"><span data-stu-id="ef01b-137">The following is an example of the response returned:</span></span>

```json
{
  "targetResourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/networkSecurityGroups/{nsgName}",
  "properties": {
    "storageId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{saName}",
    "enabled": true,
   "retentionPolicy": {
      "days": 5,
      "enabled": true
    }
  }
}
```

## <a name="download-a-flow-log"></a><span data-ttu-id="ef01b-138">Télécharger un journal de flux</span><span class="sxs-lookup"><span data-stu-id="ef01b-138">Download a flow log</span></span>

<span data-ttu-id="ef01b-139">L’emplacement de stockage d’un journal de flux est défini au moment de la création.</span><span class="sxs-lookup"><span data-stu-id="ef01b-139">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="ef01b-140">L’explorateur de stockage Microsoft Azure est un outil très pratique pour accéder à ces journaux de flux enregistrés dans un compte de stockage. Vous pouvez le télécharger ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="ef01b-140">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="ef01b-141">Si un compte de stockage est spécifié, les fichiers de capture de paquets sont enregistrés dans un compte de stockage à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="ef01b-141">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="ef01b-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ef01b-142">Next steps</span></span>

<span data-ttu-id="ef01b-143">Découvrez comment [visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="ef01b-143">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="ef01b-144">Découvrez comment [visualiser vos journaux de flux de groupe de sécurité réseau avec des outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md).</span><span class="sxs-lookup"><span data-stu-id="ef01b-144">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
