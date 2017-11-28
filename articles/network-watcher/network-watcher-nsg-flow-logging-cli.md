---
title: "Gérer les journaux des flux de groupe de sécurité réseau avec Azure Network Watcher - Azure CLI | Microsoft Docs"
description: "Cette page explique comment gérer les journaux des flux de groupe de sécurité réseau dans Azure Network Watcher avec l’interface de ligne de commande Azure"
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
ms.openlocfilehash: d5a8aa0cd274132798a0d8484a950926761dae7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-network-security-group-flow-logs-with-azure-cli"></a><span data-ttu-id="5bac0-103">Configuration des journaux des flux de groupe de sécurité réseau avec l’interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="5bac0-103">Configuring Network Security Group Flow logs with Azure CLI</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="5bac0-104">portail Azure</span><span class="sxs-lookup"><span data-stu-id="5bac0-104">Azure portal</span></span>](network-watcher-nsg-flow-logging-portal.md)
> - [<span data-ttu-id="5bac0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bac0-105">PowerShell</span></span>](network-watcher-nsg-flow-logging-powershell.md)
> - [<span data-ttu-id="5bac0-106">CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5bac0-106">CLI 1.0</span></span>](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [<span data-ttu-id="5bac0-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5bac0-107">CLI 2.0</span></span>](network-watcher-nsg-flow-logging-cli.md)
> - [<span data-ttu-id="5bac0-108">API REST</span><span class="sxs-lookup"><span data-stu-id="5bac0-108">REST API</span></span>](network-watcher-nsg-flow-logging-rest.md)

<span data-ttu-id="5bac0-109">Les journaux des flux de groupe de sécurité réseau désignent une fonctionnalité de Network Watcher qui vous permet de visualiser des informations sur le trafic IP d’entrée et de sortie par le biais d’un groupe de sécurité réseau.</span><span class="sxs-lookup"><span data-stu-id="5bac0-109">Network Security Group flow logs are a feature of Network Watcher that allows you to view information about ingress and egress IP traffic through a Network Security Group.</span></span> <span data-ttu-id="5bac0-110">Ces flux de journaux sont écrits au format json et affichent les flux entrants et sortants en fonction de la règle, la carte réseau à laquelle le flux s’applique, des informations à 5 tuples sur le flux (adresse IP source/de destination, port source/de destination, protocole), ainsi que l’autorisation ou le refus du trafic.</span><span class="sxs-lookup"><span data-stu-id="5bac0-110">These flow logs are written in json format and show outbound and inbound flows on a per rule basis, the NIC the flow applies to, 5-tuple information about the flow (Source/Destination IP, Source/Destination Port, Protocol), and if the traffic was allowed or denied.</span></span>

<span data-ttu-id="5bac0-111">Dans cet article, notre CLI nouvelle génération, Azure CLI 2.0, est utilisée pour le modèle de déploiement de gestion des ressources. Celle-ci est disponible pour Windows, Mac et Linux.</span><span class="sxs-lookup"><span data-stu-id="5bac0-111">This article uses our next generation CLI for the resource management deployment model, Azure CLI 2.0, which is available for Windows, Mac and Linux.</span></span>

<span data-ttu-id="5bac0-112">Pour exécuter la procédure indiquée dans cet article, vous devez [installer l’interface de ligne de commande Azure pour Mac, Linux et Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="5bac0-112">To perform the steps in this article, you need to [install the Azure Command-Line Interface for Mac, Linux, and Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).</span></span>

## <a name="register-insights-provider"></a><span data-ttu-id="5bac0-113">Inscription du fournisseur Insights</span><span class="sxs-lookup"><span data-stu-id="5bac0-113">Register Insights provider</span></span>

<span data-ttu-id="5bac0-114">Pour que les journaux de flux puissent correctement fonctionner, le fournisseur **Microsoft.Insights** doit être inscrit.</span><span class="sxs-lookup"><span data-stu-id="5bac0-114">In order for flow logging to work successfully, the **Microsoft.Insights** provider must be registered.</span></span> <span data-ttu-id="5bac0-115">Si vous ne savez pas si le fournisseur **Microsoft.Insights** est inscrit, exécutez le script suivant.</span><span class="sxs-lookup"><span data-stu-id="5bac0-115">If you are not sure if the **Microsoft.Insights** provider is registered, run the following script.</span></span>

```azurecli
az provider register --namespace Microsoft.Insights
```

## <a name="enable-network-security-group-flow-logs"></a><span data-ttu-id="5bac0-116">Activer les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="5bac0-116">Enable Network Security Group Flow logs</span></span>

<span data-ttu-id="5bac0-117">La commande d’activation des journaux de flux est illustrée dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="5bac0-117">The command to enable flow logs is shown in the following example:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled true --nsg nsgName --storage-account storageAccountName
```

## <a name="disable-network-security-group-flow-logs"></a><span data-ttu-id="5bac0-118">Désactiver les journaux des flux de groupe de sécurité réseau</span><span class="sxs-lookup"><span data-stu-id="5bac0-118">Disable Network Security Group Flow logs</span></span>

<span data-ttu-id="5bac0-119">Utilisez l’exemple suivant pour désactiver les journaux de flux :</span><span class="sxs-lookup"><span data-stu-id="5bac0-119">Use the following example to disable flow logs:</span></span>

```azurecli
az network watcher flow-log configure --resource-group resourceGroupName --enabled false --nsg nsgName
```

## <a name="download-a-flow-log"></a><span data-ttu-id="5bac0-120">Télécharger un journal de flux</span><span class="sxs-lookup"><span data-stu-id="5bac0-120">Download a Flow log</span></span>

<span data-ttu-id="5bac0-121">L’emplacement de stockage d’un journal de flux est défini au moment de la création.</span><span class="sxs-lookup"><span data-stu-id="5bac0-121">The storage location of a flow log is defined at creation.</span></span> <span data-ttu-id="5bac0-122">L’explorateur de stockage Microsoft Azure est un outil très pratique pour accéder à ces journaux de flux enregistrés dans un compte de stockage. Vous pouvez le télécharger ici : http://storageexplorer.com/</span><span class="sxs-lookup"><span data-stu-id="5bac0-122">A convenient tool to access these flow logs saved to a storage account is Microsoft Azure Storage Explorer, which can be downloaded here:  http://storageexplorer.com/</span></span>

<span data-ttu-id="5bac0-123">Si un compte de stockage est spécifié, les fichiers de capture de paquets sont enregistrés dans un compte de stockage à l’emplacement suivant :</span><span class="sxs-lookup"><span data-stu-id="5bac0-123">If a storage account is specified, packet capture files are saved to a storage account at the following location:</span></span>

```
https://{storageAccountName}.blob.core.windows.net/insights-logs-networksecuritygroupflowevent/resourceId%3D/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/microsoft.network/networksecuritygroups/{nsgName}/{year}/{month}/{day}/PT1H.json
```

<span data-ttu-id="5bac0-124">Pour plus d’informations sur la structure du journal, consultez [Network Security Group Flow log Overview (Présentation de la journalisation des flux de groupe de sécurité réseau)](network-watcher-nsg-flow-logging-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bac0-124">For information about the structure of the log visit [Network Security Group Flow log Overview](network-watcher-nsg-flow-logging-overview.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bac0-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5bac0-125">Next Steps</span></span>

<span data-ttu-id="5bac0-126">Découvrez comment [visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="5bac0-126">Learn how to [Visualize your NSG flow logs with PowerBI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>

<span data-ttu-id="5bac0-127">Découvrez comment [visualiser vos journaux de flux de groupe de sécurité réseau avec des outils open source](network-watcher-visualize-nsg-flow-logs-open-source-tools.md).</span><span class="sxs-lookup"><span data-stu-id="5bac0-127">Learn how to [Visualize your NSG flow logs with open source tools](network-watcher-visualize-nsg-flow-logs-open-source-tools.md)</span></span>