---
title: "aaaManage flux du groupe de sécurité réseau se connecte avec l’Observateur réseau de Azure - API REST | Documents Microsoft"
description: "Cette page explique le fonctionnement des journaux dans l’Observateur réseau de Azure avec l’API REST toomanage flux du groupe de sécurité réseau"
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
ms.openlocfilehash: be81e35f4d01c67efef99773e9b4e2ae4b8e209e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-using-rest-api"></a><span data-ttu-id="1f953-103">Configuration des journaux des flux de groupe de sécurité réseau avec l’API REST</span><span class="sxs-lookup"><span data-stu-id="1f953-103">Configuring Network Security Group flow logs using REST API</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="1f953-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="1f953-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="1f953-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1f953-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="1f953-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="1f953-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="1f953-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1f953-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="1f953-108">API REST</span><span class="sxs-lookup"><span data-stu-id="1f953-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="1f953-109">Journaux du groupe de sécurité réseau de flux sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1f953-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="1f953-110">Ces flux de journaux est écrits au format json et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="1f953-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1f953-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="1f953-111">Before you begin</span></span>

<span data-ttu-id="1f953-112">ARMclient est utilisé toocall hello REST API à l’aide de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1f953-112">ARMclient is used toocall hello REST API using PowerShell.</span></span> <span data-ttu-id="1f953-113">ARMClient est accessible sur le site chocolatey à partir de la page [ARMClient sur Chocolatey](https://chocolatey.org/packages/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="1f953-113">ARMClient is found on chocolatey at [ARMClient on Chocolatey](https://chocolatey.org/packages/ARMClient)</span></span>

<span data-ttu-id="1f953-114">Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer un observateur réseau](network-watcher-create.md) toocreate un observateur réseau.</span><span class="sxs-lookup"><span data-stu-id="1f953-114">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span>

> [!Important]
> <span data-ttu-id="1f953-115">Pour l’API REST de l’Observateur réseau appels hello nom de groupe de ressources dans la demande de hello QU'URI est le groupe de ressources hello contient hello Observateur réseau, pas les ressources hello vous effectuez des actions de diagnostic hello sur.</span><span class="sxs-lookup"><span data-stu-id="1f953-115">For Network Watcher REST API calls hello resource group name in hello request URI is hello resource group that contains hello Network Watcher, not hello resources you are performing hello diagnostic actions on.</span></span>

## <a name="scenario"></a><span data-ttu-id="1f953-116">Scénario</span><span class="sxs-lookup"><span data-stu-id="1f953-116">Scenario</span></span>

<span data-ttu-id="1f953-117">scénario Hello abordée dans cet article vous montre comment tooenable, désactiver et requête de flux de journaux à l’aide des API REST de hello.</span><span class="sxs-lookup"><span data-stu-id="1f953-117">hello scenario covered in this article shows you how tooenable, disable, and query flow logs using hello REST API.</span></span> <span data-ttu-id="1f953-118">toolearn en savoir plus sur les enregistrements de flux de groupe de sécurité réseau, visitez [enregistrement de flux de groupe de sécurité réseau - vue d’ensemble](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f953-118">toolearn more about Network Security Group flow loggings, visit [Network Security Group flow logging - Overview](network-watcher-nsg-flow-logging-overview.md).</span></span>

<span data-ttu-id="1f953-119">Dans ce scénario, vous allez :</span><span class="sxs-lookup"><span data-stu-id="1f953-119">In this scenario, you will:</span></span>

* <span data-ttu-id="1f953-120">Activer les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="1f953-120">Enable flow logs</span></span>
* <span data-ttu-id="1f953-121">Désactiver les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="1f953-121">Disable flow logs</span></span>
* <span data-ttu-id="1f953-122">Interroger l’état des journaux des flux</span><span class="sxs-lookup"><span data-stu-id="1f953-122">Query flow logs status</span></span>

## <a name="log-in-with-armclient"></a><span data-ttu-id="1f953-123">Se connecter à ARMClient</span><span class="sxs-lookup"><span data-stu-id="1f953-123">Log in with ARMClient</span></span>

<span data-ttu-id="1f953-124">Ouvrez une session dans tooarmclient avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="1f953-124">Log in tooarmclient with your Azure credentials.</span></span>

```PowerShell
armclient login
```

## <a name="register-insights-provider"></a><span data-ttu-id="1f953-125">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="1f953-125">Register Insights provider</span></span>

<span data-ttu-id="1f953-126">Dans l’ordre pour le flux de journalisation toowork hello avec succès, **Microsoft.Insights** fournisseur doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="1f953-126">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="1f953-127">Si vous n’êtes pas sûr si hello **Microsoft.Insights** fournisseur est inscrit, hello exécution de script suivant.</span><span class="sxs-lookup"><span data-stu-id="1f953-127">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```powershell
$subscriptionId = "00000000-0000-0000-0000-000000000000"
armclient post "https://management.azure.com//subscriptions/${subscriptionId}/providers/Microsoft.Insights/register?api-version=2016-09-01"
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="1f953-128">Activer les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="1f953-128">Enable Network Security Group flow logs</span></span>

<span data-ttu-id="1f953-129">les journaux de flux de tooenable commande Hello est présenté dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="1f953-129">hello command tooenable flow logs is shown in hello following example:</span></span>

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

<span data-ttu-id="1f953-130">réponse de Hello retournée à partir de hello précédent exemple est la suivante :</span><span class="sxs-lookup"><span data-stu-id="1f953-130">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="1f953-131">Désactiver les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="1f953-131">Disable Network Security Group flow logs</span></span>

<span data-ttu-id="1f953-132">Hello utilisez suit exemple toodisable flux se connecte.</span><span class="sxs-lookup"><span data-stu-id="1f953-132">Use hello following example toodisable flow logs.</span></span> <span data-ttu-id="1f953-133">Bonjour appel est même hello à activer les journaux de flux, à l’exception de **false** est définie pour la propriété de hello activée.</span><span class="sxs-lookup"><span data-stu-id="1f953-133">hello call is hello same as enabling flow logs, except **false** is set for hello enabled property.</span></span>

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

<span data-ttu-id="1f953-134">réponse de Hello retournée à partir de hello précédent exemple est la suivante :</span><span class="sxs-lookup"><span data-stu-id="1f953-134">hello response returned from hello preceding example is as follows:</span></span>

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

## <a name="query-flow-logs"></a><span data-ttu-id="1f953-135">Interroger les journaux des flux</span><span class="sxs-lookup"><span data-stu-id="1f953-135">Query flow logs</span></span>

<span data-ttu-id="1f953-136">Hello après appel REST requêtes hello état du flux de journaux sur un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="1f953-136">hello following REST call queries hello status of flow logs on a Network Security Group.</span></span>

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

<span data-ttu-id="1f953-137">Hello Voici un exemple de réponse hello retournée :</span><span class="sxs-lookup"><span data-stu-id="1f953-137">hello following is an example of hello response returned:</span></span>

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

## <a name="download-a-flow-log"></a><span data-ttu-id="1f953-138">Télécharger un journal de flux</span><span class="sxs-lookup"><span data-stu-id="1f953-138">Download a flow log</span></span>

<span data-ttu-id="1f953-139">emplacement de stockage Hello d’un journal de flux est définie lors de la création.</span><span class="sxs-lookup"><span data-stu-id="1f953-139">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="1f953-140">Un tooaccess outil pratique ces compte de stockage de journaux enregistrés tooa est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="1f953-140">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="1f953-141">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="1f953-141">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

## <a name="next-steps"></a><span data-ttu-id="1f953-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="1f953-142">Next steps</span></span>

<span data-ttu-id="1f953-143">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="1f953-143">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="1f953-144">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec les outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="1f953-144">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
