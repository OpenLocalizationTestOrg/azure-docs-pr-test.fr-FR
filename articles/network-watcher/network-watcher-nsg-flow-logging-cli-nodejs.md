---
title: "aaaManage flux de groupe de sécurité réseau se connecte avec l’Observateur réseau de Azure - Azure CLI 1.0 | Documents Microsoft"
description: "Cette page explique le fonctionnement des journaux dans l’Observateur réseau de Azure avec Azure CLI 1.0 toomanage flux de groupe de sécurité réseau"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 2dfc3112-8294-4357-b2f8-f81840da67d3
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 2535eea665a99cffe7569a8d976333435f946a80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli-10"></a><span data-ttu-id="182ac-103">Configuration des journaux des flux de groupe de sécurité réseau avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="182ac-103">Configuring Network Security Group Flow logs with Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="182ac-104">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="182ac-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="182ac-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="182ac-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="182ac-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="182ac-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="182ac-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="182ac-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="182ac-108">API REST</span><span class="sxs-lookup"><span data-stu-id="182ac-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="182ac-109">Journaux du groupe de sécurité réseau de flux sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="182ac-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="182ac-110">Ces flux de journaux est écrits au format json et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="182ac-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="182ac-111">Cet article utilise l’interface Azure CLI 1.0 interplateforme, disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="182ac-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span> <span data-ttu-id="182ac-112">Network Watcher utilise actuellement Azure CLI 1.0 pour la prise en charge d’interface CLI.</span><span class="sxs-lookup"><span data-stu-id="182ac-112">Network Watcher currently uses Azure CLI 1.0 for CLI support.</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="182ac-113">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="182ac-113">Register Insights provider</span></span>

<span data-ttu-id="182ac-114">Dans l’ordre pour le flux de journalisation toowork hello avec succès, **Microsoft.Insights** fournisseur doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="182ac-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="182ac-115">Si vous n’êtes pas sûr si hello **Microsoft.Insights** fournisseur est inscrit, hello exécution de script suivant.</span><span class="sxs-lookup"><span data-stu-id="182ac-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
azure provider register --namespace Microsoft.Insights --subscription <subscriptionid>
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="182ac-116">Activer les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="182ac-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="182ac-117">les journaux de flux de tooenable commande Hello est présenté dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="182ac-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e true
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="182ac-118">Désactiver les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="182ac-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="182ac-119">Hello utilisation suivant des journaux de flux toodisable exemple :</span><span class="sxs-lookup"><span data-stu-id="182ac-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
azure network watcher configure-flow-log -g resourceGroupName -n networkWatcherName -t nsgId -i storageAccountId -e false
```

## <a name="download-a-flow-log"></a><span data-ttu-id="182ac-120">Télécharger un journal de flux</span><span class="sxs-lookup"><span data-stu-id="182ac-120">Download a Flow log</span></span>

<span data-ttu-id="182ac-121">emplacement de stockage Hello d’un journal de flux est définie lors de la création.</span><span class="sxs-lookup"><span data-stu-id="182ac-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="182ac-122">Un tooaccess outil pratique ces compte de stockage de journaux enregistrés tooa est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="182ac-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="182ac-123">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="182ac-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="182ac-124">Pour plus d’informations sur la structure hello du journal de hello visitez [journal vue d’ensemble des flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="182ac-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="182ac-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="182ac-125">Next Steps</span></span>

<span data-ttu-id="182ac-126">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="182ac-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="182ac-127">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec les outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="182ac-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
