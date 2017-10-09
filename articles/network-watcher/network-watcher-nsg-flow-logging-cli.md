---
title: "aaaManage flux de groupe de sécurité réseau se connecte avec l’Observateur réseau de Azure - CLI d’Azure | Documents Microsoft"
description: "Cette page explique le fonctionnement des journaux toomanage flux de groupe de sécurité réseau dans l’Observateur réseau de Azure avec Azure CLI"
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
ms.openlocfilehash: 2d0b02e7d0a5a9ab20beb491d49a5747f976a079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="d832b-103">Configuration des journaux des flux de groupe de sécurité réseau avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="d832b-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="d832b-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="d832b-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="d832b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d832b-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="d832b-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="d832b-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="d832b-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="d832b-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="d832b-108">API REST</span><span class="sxs-lookup"><span data-stu-id="d832b-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="d832b-109">Journaux du groupe de sécurité réseau de flux sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="d832b-109">Network Security Group flow logs are a feature of Network Watcher that allows you tooview information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="d832b-110">Ces flux de journaux est écrits au format json et affiche sortant des flux entrants sur une base par la règle, hello flux hello de carte réseau s’applique, 5-tuple d’informations sur le flux hello (protocole IP Source et de Destination, Port Source et de Destination) et si hello le trafic a été autorisé ou refusé.</span><span class="sxs-lookup"><span data-stu-id="d832b-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, hello NIC hello flow applies to, 5-tuple information about hello flow (Source/Destination IP, Source/Destination Port, Protocol), and if hello traffic was allowed or denied.</span></span>

<span data-ttu-id="d832b-111">Cet article utilise notre prochaine génération CLI pour le modèle de déploiement de la gestion des ressources d’hello, Azure CLI 2.0, qui est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="d832b-111">This article uses our next generation CLI for hello resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="d832b-112">les étapes tooperform hello dans cet article, vous devez trop[installer hello Interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="d832b-112">tooperform hello steps in this article, you need too[install hello Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="d832b-113">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="d832b-113">Register Insights provider</span></span>

<span data-ttu-id="d832b-114">Dans l’ordre pour le flux de journalisation toowork hello avec succès, **Microsoft.Insights** fournisseur doit être enregistré.</span><span class="sxs-lookup"><span data-stu-id="d832b-114">In order for flow logging toowork successfully, hello **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="d832b-115">Si vous n’êtes pas sûr si hello **Microsoft.Insights** fournisseur est inscrit, hello exécution de script suivant.</span><span class="sxs-lookup"><span data-stu-id="d832b-115">If you are not sure if hello **Microsoft.Insights** provider is registered, run hello following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="d832b-116">Activer les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d832b-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="d832b-117">les journaux de flux de tooenable commande Hello est présenté dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="d832b-117">hello command tooenable flow logs is shown in hello following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="d832b-118">Désactiver les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="d832b-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="d832b-119">Hello utilisation suivant des journaux de flux toodisable exemple :</span><span class="sxs-lookup"><span data-stu-id="d832b-119">Use hello following example toodisable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="d832b-120">Télécharger un journal de flux</span><span class="sxs-lookup"><span data-stu-id="d832b-120">Download a Flow log</span></span>

<span data-ttu-id="d832b-121">emplacement de stockage Hello d’un journal de flux est définie lors de la création.</span><span class="sxs-lookup"><span data-stu-id="d832b-121">hello storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="d832b-122">Un tooaccess outil pratique ces compte de stockage de journaux enregistrés tooa est Microsoft Azure Storage Explorer, qui peut être téléchargée ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="d832b-122">A convenient tool tooaccess these flow logs saved tooa storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="d832b-123">Si un compte de stockage est spécifié, les fichiers de capture de paquet sont enregistrés compte de stockage tooa hello l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="d832b-123">If a storage account is specified, packet capture files are saved tooa storage account at hello following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="d832b-124">Pour plus d’informations sur la structure hello du journal de hello visitez [journal vue d’ensemble des flux de groupe de sécurité réseau](network-watcher-nsg-flow-logging-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d832b-124">For information about hello structure of hello log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d832b-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d832b-125">Next Steps</span></span>

<span data-ttu-id="d832b-126">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="d832b-126">Learn how too[Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="d832b-127">Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec les outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span><span class="sxs-lookup"><span data-stu-id="d832b-127">Learn how too[Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>
