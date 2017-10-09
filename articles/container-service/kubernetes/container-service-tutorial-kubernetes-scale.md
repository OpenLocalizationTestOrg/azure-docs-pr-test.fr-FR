---
title: "didacticiel de Service de conteneur aaaAzure - Application de la mise à l’échelle | Documents Microsoft"
description: "Didacticiel Azure Container Service - Mettre à l’échelle une application"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="e8f42-104">Mettre à l’échelle des pods Kubernetes et l’infrastructure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e8f42-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="e8f42-105">Si vous avez effectué les didacticiels de hello, vous avez une Kubernetes cluster dans le conteneur de Service Azure et que vous avez déployé l’application Azure vote de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f42-105">If you've been following hello tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed hello Azure Voting app.</span></span> 

<span data-ttu-id="e8f42-106">Dans ce didacticiel, partie 5, 7, vous montée en puissance parallèle POD hello dans l’application hello et essayez d’échelle de pod.</span><span class="sxs-lookup"><span data-stu-id="e8f42-106">In this tutorial, part five of seven, you scale out hello pods in hello app and try pod autoscaling.</span></span> <span data-ttu-id="e8f42-107">Vous apprendrez également comment le nombre de hello tooscale de toochange de nœuds de l’agent de machine virtuelle Azure hello capacité du cluster pour l’hébergement des charges de travail.</span><span class="sxs-lookup"><span data-stu-id="e8f42-107">You also learn how tooscale hello number of Azure VM agent nodes toochange hello cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="e8f42-108">Les tâches accomplies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8f42-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8f42-109">Mise à l’échelle manuelle des pods Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e8f42-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="e8f42-110">Configuration des blocs de mise à l’échelle le frontal application hello en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="e8f42-110">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="e8f42-111">Mettre à l’échelle des nœuds de l’agent Azure hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e8f42-111">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="e8f42-112">Dans les didacticiels suivants hello application de Vote de Azure est mis à jour et Operations Management Suite configuré le cluster de Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="e8f42-112">In subsequent tutorials, hello Azure Vote application is updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e8f42-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e8f42-113">Before you begin</span></span>

<span data-ttu-id="e8f42-114">Dans les didacticiels précédents, une application a été empaquetée dans une image de conteneur, cette image téléchargée tooAzure Registre de conteneur et un cluster Kubernetes créé.</span><span class="sxs-lookup"><span data-stu-id="e8f42-114">In previous tutorials, an application was packaged into a container image, this image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="e8f42-115">application Hello puis exécutée sur le cluster de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="e8f42-115">hello application was then run on hello Kubernetes cluster.</span></span> <span data-ttu-id="e8f42-116">Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner toohello [didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="e8f42-116">If you have not done these steps, and would like toofollow along, return toohello [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="e8f42-117">Ce didacticiel nécessite au minimum un cluster Kubernetes avec une application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="e8f42-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="e8f42-118">Mettre à l’échelle des pods manuellement</span><span class="sxs-lookup"><span data-stu-id="e8f42-118">Manually scale pods</span></span>

<span data-ttu-id="e8f42-119">Jusqu'à présent, hello Vote Azure frontal et instance Redis ont été déployées, chacune avec un seul réplica.</span><span class="sxs-lookup"><span data-stu-id="e8f42-119">Thus far, hello Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="e8f42-120">tooverify, exécutez hello [kubectl obtenir](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.</span><span class="sxs-lookup"><span data-stu-id="e8f42-120">tooverify, run hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="e8f42-121">Output:</span><span class="sxs-lookup"><span data-stu-id="e8f42-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="e8f42-122">Modifier manuellement le nombre de hello de POD Bonjour `azure-vote-front` déploiement à l’aide de hello [kubectl échelle](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) commande.</span><span class="sxs-lookup"><span data-stu-id="e8f42-122">Manually change hello number of pods in hello `azure-vote-front` deployment using hello [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="e8f42-123">Cet exemple augmente too5 numéro de hello.</span><span class="sxs-lookup"><span data-stu-id="e8f42-123">This example increases hello number too5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="e8f42-124">Exécutez [kubectl obtenir POD](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify que Kubernetes crée les POD hello.</span><span class="sxs-lookup"><span data-stu-id="e8f42-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify that Kubernetes is creating hello pods.</span></span> <span data-ttu-id="e8f42-125">Après environ une minute, POD supplémentaires de hello est en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="e8f42-125">After a minute or so, hello additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="e8f42-126">Output:</span><span class="sxs-lookup"><span data-stu-id="e8f42-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="e8f42-127">Mettre à l’échelle les pods automatiquement</span><span class="sxs-lookup"><span data-stu-id="e8f42-127">Autoscale pods</span></span>

<span data-ttu-id="e8f42-128">Prend en charge les Kubernetes [pod horizontal échelle](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) nombre de hello tooadjust de blocs dans un déploiement en fonction de l’utilisation du processeur ou d’autres sélectionner des mesures.</span><span class="sxs-lookup"><span data-stu-id="e8f42-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="e8f42-129">toouse hello autoscaler, votre POD doit avoir des demandes de l’UC et les limites définies.</span><span class="sxs-lookup"><span data-stu-id="e8f42-129">toouse hello autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="e8f42-130">Bonjour `azure-vote-front` déploiement, hello du processeur de requêtes 0,25 conteneur frontal, avec une limite de 0,5 UC.</span><span class="sxs-lookup"><span data-stu-id="e8f42-130">In hello `azure-vote-front` deployment, hello front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="e8f42-131">paramètres de Hello ressembler à :</span><span class="sxs-lookup"><span data-stu-id="e8f42-131">hello settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="e8f42-132">exemple Hello utilise hello [kubectl mise à l’échelle](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) commande le nombre de hello tooautoscale de POD Bonjour `azure-vote-front` déploiement.</span><span class="sxs-lookup"><span data-stu-id="e8f42-132">hello following example uses hello [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command tooautoscale hello number of pods in hello `azure-vote-front` deployment.</span></span> <span data-ttu-id="e8f42-133">Ici, si l’utilisation du processeur dépasse 50 %, hello autoscaler augmente hello POD tooa 10 au maximum.</span><span class="sxs-lookup"><span data-stu-id="e8f42-133">Here, if CPU utilization exceeds 50%, hello autoscaler increases hello pods tooa maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="e8f42-134">état de hello toosee d’autoscaler hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e8f42-134">toosee hello status of hello autoscaler, run hello following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="e8f42-135">Output:</span><span class="sxs-lookup"><span data-stu-id="e8f42-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="e8f42-136">Après quelques minutes, avec une charge minimale sur l’application de Vote de Azure hello, hello nombre de réplicas de pod diminue automatiquement too3.</span><span class="sxs-lookup"><span data-stu-id="e8f42-136">After a few minutes, with minimal load on hello Azure Vote app, hello number of pod replicas decreases automatically too3.</span></span>

## <a name="scale-hello-agents"></a><span data-ttu-id="e8f42-137">Agents de mise à l’échelle hello</span><span class="sxs-lookup"><span data-stu-id="e8f42-137">Scale hello agents</span></span>

<span data-ttu-id="e8f42-138">Si vous avez créé votre cluster Kubernetes à l’aide des commandes par défaut dans le cadre du didacticiel précédent hello, il a trois nœuds de l’agent.</span><span class="sxs-lookup"><span data-stu-id="e8f42-138">If you created your Kubernetes cluster using default commands in hello previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="e8f42-139">Vous pouvez ajuster nombre hello d’agents manuellement si vous envisagez de charges de travail plus ou moins de conteneur sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="e8f42-139">You can adjust hello number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="e8f42-140">Hello d’utilisation [mettre à l’échelle des services acs az](/cli/azure/acs#scale) de commandes et spécifiez le nombre hello d’agents avec hello `--new-agent-count` paramètre.</span><span class="sxs-lookup"><span data-stu-id="e8f42-140">Use hello [az acs scale](/cli/azure/acs#scale) command, and specify hello number of agents with hello `--new-agent-count` parameter.</span></span>

<span data-ttu-id="e8f42-141">Hello exemple suivant augmente nombre hello de too4 de nœuds de l’agent dans le cluster de Kubernetes hello nommé *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="e8f42-141">hello following example increases hello number of agent nodes too4 in hello Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="e8f42-142">commande Hello prend quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e8f42-142">hello command takes a couple of minutes toocomplete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="e8f42-143">Hello sortie de la commande affiche hello numéro de l’agent de nœuds de valeur hello `agentPoolProfiles:count`:</span><span class="sxs-lookup"><span data-stu-id="e8f42-143">hello command output shows hello number of agent nodes in hello value of `agentPoolProfiles:count`:</span></span>

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a><span data-ttu-id="e8f42-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8f42-144">Next steps</span></span>

<span data-ttu-id="e8f42-145">Dans ce didacticiel, vous avez utilisé différentes fonctionnalités de mise à l’échelle dans votre cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e8f42-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="e8f42-146">Les tâches traitées ont inclus :</span><span class="sxs-lookup"><span data-stu-id="e8f42-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e8f42-147">Mise à l’échelle manuelle des pods Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e8f42-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="e8f42-148">Configuration des blocs de mise à l’échelle le frontal application hello en cours d’exécution</span><span class="sxs-lookup"><span data-stu-id="e8f42-148">Configuring Autoscale pods running hello app front end</span></span>
> * <span data-ttu-id="e8f42-149">Mettre à l’échelle des nœuds de l’agent Azure hello Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e8f42-149">Scale hello Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="e8f42-150">Toohello toolearn de didacticiel suivant sur la mise à jour d’application dans Kubernetes d’avance.</span><span class="sxs-lookup"><span data-stu-id="e8f42-150">Advance toohello next tutorial toolearn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8f42-151">Mettre à jour une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e8f42-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

