---
title: cluster de Azure Kubernetes aaaMonitor avec Datadog | Documents Microsoft
description: "Surveillance du cluster Kubernetes dans Azure Container Service à l’aide de Datadog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="7b155-103">Surveiller un cluster Azure Container Service avec Datadog</span><span class="sxs-lookup"><span data-stu-id="7b155-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b155-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7b155-104">Prerequisites</span></span>
<span data-ttu-id="7b155-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="7b155-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="7b155-106">Il suppose également que vous avez hello `az` cli Azure et `kubectl` outils sont installés.</span><span class="sxs-lookup"><span data-stu-id="7b155-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="7b155-107">Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="7b155-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="7b155-108">Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="7b155-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="7b155-109">Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="7b155-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="7b155-110">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="7b155-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="7b155-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="7b155-111">DataDog</span></span>
<span data-ttu-id="7b155-112">Datadog est un service de surveillance qui regroupe les données de surveillance provenant de vos conteneurs dans votre cluster Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="7b155-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="7b155-113">Datadog intègre un tableau de bord Docker Integration qui affiche des mesures spécifiques dans vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="7b155-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="7b155-114">Les mesures recueillies à partir de vos conteneurs sont classées par processeur, mémoire, réseau et E/S.</span><span class="sxs-lookup"><span data-stu-id="7b155-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="7b155-115">Datadog fractionne les mesures en conteneurs et images.</span><span class="sxs-lookup"><span data-stu-id="7b155-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="7b155-116">Vous devez tout d’abord trop[créer un compte](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="7b155-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="7b155-117">L’installation de hello Datadog Agent avec un DaemonSet</span><span class="sxs-lookup"><span data-stu-id="7b155-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="7b155-118">DaemonSets sont utilisés par Kubernetes toorun une instance unique d’un conteneur sur chaque hôte de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="7b155-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="7b155-119">Ils sont parfaits pour exécuter des agents de surveillance.</span><span class="sxs-lookup"><span data-stu-id="7b155-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="7b155-120">Une fois que vous êtes connecté à Datadog, vous pouvez suivre hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) agents de Datadog tooinstall sur votre cluster à l’aide d’un DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="7b155-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="7b155-121">Conclusion</span><span class="sxs-lookup"><span data-stu-id="7b155-121">Conclusion</span></span>
<span data-ttu-id="7b155-122">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="7b155-122">That's it!</span></span> <span data-ttu-id="7b155-123">Une fois que les agents hello sont activés et en cours d’exécution vous devez voir des données dans la console hello dans quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7b155-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="7b155-124">Vous pouvez visiter hello intégré [kubernetes le tableau de bord](https://app.datadoghq.com/screen/integration/kubernetes) toosee un résumé de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="7b155-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
