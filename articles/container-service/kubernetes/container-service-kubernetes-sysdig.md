---
title: cluster de Azure Kubernetes aaaMonitor - Sysdig | Documents Microsoft
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
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="58968-103">Surveiller un cluster Kubernetes Azure Container Service avec Sysdig</span><span class="sxs-lookup"><span data-stu-id="58968-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58968-104">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="58968-104">Prerequisites</span></span>
<span data-ttu-id="58968-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="58968-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="58968-106">Il suppose également que vous disposez des outils cli et kubectl hello azure installés.</span><span class="sxs-lookup"><span data-stu-id="58968-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="58968-107">Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="58968-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="58968-108">Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="58968-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="58968-109">Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="58968-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="58968-110">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="58968-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="58968-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="58968-111">Sysdig</span></span>
<span data-ttu-id="58968-112">Sysdig est une société de surveillance en tant que service pouvant analyser les conteneurs de votre cluster Kubernetes exécuté dans Azure.</span><span class="sxs-lookup"><span data-stu-id="58968-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="58968-113">L’utilisation de Sysdig nécessite un compte Sysdig actif.</span><span class="sxs-lookup"><span data-stu-id="58968-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="58968-114">Vous pouvez créer un compte Azure sur leur [site](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="58968-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="58968-115">Une fois que vous êtes connecté dans le site Web du cloud toohello Sysdig, cliquez sur votre nom d’utilisateur et sur la page de hello, vous devez voir votre « clé d’accès ».</span><span class="sxs-lookup"><span data-stu-id="58968-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Clé d’API Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="58968-117">L’installation hello Sysdig agents tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="58968-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="58968-118">toomonitor vos conteneurs, et s’exécute de Sysdig un processus sur chaque ordinateur à l’aide d’un Kubernetes `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="58968-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="58968-119">Les DaemonSets sont des objets API Kubernetes qui exécutent une instance unique d’un conteneur par machine.</span><span class="sxs-lookup"><span data-stu-id="58968-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="58968-120">Ils conviennent parfaitement pour l’installation des outils comme hello agent d’analyse de Sysdig.</span><span class="sxs-lookup"><span data-stu-id="58968-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="58968-121">tooinstall hello Sysdig daemonset, vous devez tout d’abord télécharger [modèle de hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) à partir de sysdig.</span><span class="sxs-lookup"><span data-stu-id="58968-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="58968-122">Enregistrez ce fichier sous `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="58968-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="58968-123">Sur Linux et OS X, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="58968-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="58968-124">Dans PowerShell :</span><span class="sxs-lookup"><span data-stu-id="58968-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="58968-125">Ensuite modifier ce fichier tooinsert votre clé d’accès, que vous avez obtenue à partir de votre compte Sysdig.</span><span class="sxs-lookup"><span data-stu-id="58968-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="58968-126">Enfin, créez hello DaemonSet :</span><span class="sxs-lookup"><span data-stu-id="58968-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="58968-127">Afficher votre analyse</span><span class="sxs-lookup"><span data-stu-id="58968-127">View your monitoring</span></span>
<span data-ttu-id="58968-128">Une fois installé et en cours d’exécution, les agents hello doivent pump tooSysdig précédent de données.</span><span class="sxs-lookup"><span data-stu-id="58968-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="58968-129">Revenir en arrière toothe [sysdig le tableau de bord](https://app.sysdigcloud.com) et vous devez obtenir des informations sur vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="58968-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="58968-130">Vous pouvez également installer des tableaux de bords spécifiques de Kubernetes en utilisant [l’Assistant Nouveau tableau de bord](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="58968-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
