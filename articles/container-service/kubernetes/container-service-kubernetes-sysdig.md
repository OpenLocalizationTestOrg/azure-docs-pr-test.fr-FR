---
title: Surveiller le cluster Azure Kubernetes - Sysdig | Microsoft Docs
description: "Surveillance du cluster Kubernetes dans Azure Container Service à l’aide de Sysdig"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: afe22b84015526f901111238e36baaa94694ccbf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="2ef33-103">Surveiller un cluster Kubernetes Azure Container Service avec Sysdig</span><span class="sxs-lookup"><span data-stu-id="2ef33-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ef33-104">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="2ef33-104">Prerequisites</span></span>
<span data-ttu-id="2ef33-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2ef33-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="2ef33-106">Elle suppose également que vous avez installé les outils azure cli et kubectl.</span><span class="sxs-lookup"><span data-stu-id="2ef33-106">It also assumes that you have the azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="2ef33-107">Vous pouvez tester si l’outil `az` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="2ef33-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="2ef33-108">Si l’outil `az` n’est pas installé, suivez les instructions figurant [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="2ef33-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="2ef33-109">Vous pouvez tester si l’outil `kubectl` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="2ef33-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="2ef33-110">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="2ef33-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="2ef33-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="2ef33-111">Sysdig</span></span>
<span data-ttu-id="2ef33-112">Sysdig est une société de surveillance en tant que service pouvant analyser les conteneurs de votre cluster Kubernetes exécuté dans Azure.</span><span class="sxs-lookup"><span data-stu-id="2ef33-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="2ef33-113">L’utilisation de Sysdig nécessite un compte Sysdig actif.</span><span class="sxs-lookup"><span data-stu-id="2ef33-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="2ef33-114">Vous pouvez créer un compte Azure sur leur [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="2ef33-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="2ef33-115">Une fois connecté au site web du cloud Sysdig, cliquez sur votre nom d’utilisateur. La page qui s’affiche comporte votre clé d’accès (Access Key).</span><span class="sxs-lookup"><span data-stu-id="2ef33-115">Once you're logged in to the Sysdig cloud website, click on your user name, and on the page you should see your "Access Key."</span></span> 

![Clé d’API Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-the-sysdig-agents-to-kubernetes"></a><span data-ttu-id="2ef33-117">Installation des agents Sysdig sur Kubernetes</span><span class="sxs-lookup"><span data-stu-id="2ef33-117">Installing the Sysdig agents to Kubernetes</span></span>
<span data-ttu-id="2ef33-118">Pour analyser vos conteneurs, Sysdig exécute un processus sur chaque machine à l’aide d’un `DaemonSet` Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="2ef33-118">To monitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="2ef33-119">Les DaemonSets sont des objets API Kubernetes qui exécutent une instance unique d’un conteneur par machine.</span><span class="sxs-lookup"><span data-stu-id="2ef33-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="2ef33-120">Ils sont parfaits pour installer des outils, tels que l’agent de surveillance de Sysdig.</span><span class="sxs-lookup"><span data-stu-id="2ef33-120">They're perfect for installing tools like the Sysdig's monitoring agent.</span></span>

<span data-ttu-id="2ef33-121">Pour installer le daemonset Sysdig, vous devez d’abord télécharger [le modèle](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) à partir de sysdig.</span><span class="sxs-lookup"><span data-stu-id="2ef33-121">To install the Sysdig daemonset, you should first download [the template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="2ef33-122">Enregistrez ce fichier sous `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="2ef33-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="2ef33-123">Sur Linux et OS X, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="2ef33-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="2ef33-124">Dans PowerShell :</span><span class="sxs-lookup"><span data-stu-id="2ef33-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="2ef33-125">Modifiez ensuite ce fichier pour insérer votre clé d’accès que vous avez obtenue à partir de votre compte Sysdig.</span><span class="sxs-lookup"><span data-stu-id="2ef33-125">Next edit that file to insert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="2ef33-126">Enfin, créez le DaemonSet :</span><span class="sxs-lookup"><span data-stu-id="2ef33-126">Finally, create the DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="2ef33-127">Afficher votre analyse</span><span class="sxs-lookup"><span data-stu-id="2ef33-127">View your monitoring</span></span>
<span data-ttu-id="2ef33-128">Une fois installés et en cours d’exécution, les agents doivent extraire des données depuis Sysdig.</span><span class="sxs-lookup"><span data-stu-id="2ef33-128">Once installed and running, the agents should pump data back to Sysdig.</span></span>  <span data-ttu-id="2ef33-129">Revenez au [tableau de bord](https://app.sysdigcloud.com) et vous verrez des informations sur vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="2ef33-129">Go back to the [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="2ef33-130">Vous pouvez également installer des tableaux de bords spécifiques de Kubernetes en utilisant [l’Assistant Nouveau tableau de bord](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="2ef33-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
