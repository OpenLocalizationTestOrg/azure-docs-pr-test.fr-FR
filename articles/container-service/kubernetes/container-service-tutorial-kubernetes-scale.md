---
title: "Didacticiel Azure Container Service - Mettre à l’échelle une application | Microsoft Docs"
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
ms.openlocfilehash: 62e70e34d06f5220734ff85c70a0c9b475f9579b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a><span data-ttu-id="39d92-104">Mettre à l’échelle des pods Kubernetes et l’infrastructure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="39d92-104">Scale Kubernetes pods and Kubernetes infrastructure</span></span>

<span data-ttu-id="39d92-105">Si vous avez suivi les didacticiels, vous disposez d’un cluster Kubernetes opérationnel dans Azure Container Service et vous avez déployé l’application Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="39d92-105">If you've been following the tutorials, you have a working Kubernetes cluster in Azure Container Service and you deployed the Azure Voting app.</span></span> 

<span data-ttu-id="39d92-106">Dans ce didacticiel (issu d’une série de sept didacticiels), vous allez augmenter le nombre de pods dans l’application et essayer la mise à l’échelle automatique des pods.</span><span class="sxs-lookup"><span data-stu-id="39d92-106">In this tutorial, part five of seven, you scale out the pods in the app and try pod autoscaling.</span></span> <span data-ttu-id="39d92-107">Vous allez également apprendre à mettre à l’échelle le nombre de nœuds d’agents de machine virtuelle Azure afin de modifier la capacité du cluster pour l’hébergement des charges de travail.</span><span class="sxs-lookup"><span data-stu-id="39d92-107">You also learn how to scale the number of Azure VM agent nodes to change the cluster's capacity for hosting workloads.</span></span> <span data-ttu-id="39d92-108">Les tâches accomplies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="39d92-108">Tasks completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39d92-109">Mise à l’échelle manuelle des pods Kubernetes</span><span class="sxs-lookup"><span data-stu-id="39d92-109">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="39d92-110">Configuration de la mise à l’échelle automatique des pods qui exécutent le front-end de l’application</span><span class="sxs-lookup"><span data-stu-id="39d92-110">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="39d92-111">Mettre à l’échelle les nœuds d’agents Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="39d92-111">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="39d92-112">Dans les didacticiels suivants, l’application Azure Vote est mise à jour et Operations Management Suite est configuré pour la surveillance du cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="39d92-112">In subsequent tutorials, the Azure Vote application is updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="39d92-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="39d92-113">Before you begin</span></span>

<span data-ttu-id="39d92-114">Dans les didacticiels précédents, une application a été empaquetée dans une image conteneur, l’image a été chargée dans Azure Container Registry et un cluster Kubernetes a été créé.</span><span class="sxs-lookup"><span data-stu-id="39d92-114">In previous tutorials, an application was packaged into a container image, this image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="39d92-115">L’application a ensuite été exécutée sur le cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="39d92-115">The application was then run on the Kubernetes cluster.</span></span> <span data-ttu-id="39d92-116">Si vous n’avez pas accompli ces étapes et que vous souhaitez suivre cette procédure, revenez au [Didacticiel 1 – Créer des images conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="39d92-116">If you have not done these steps, and would like to follow along, return to the [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="39d92-117">Ce didacticiel nécessite au minimum un cluster Kubernetes avec une application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="39d92-117">At minimum, this tutorial requires a Kubernetes cluster with a running application.</span></span>

## <a name="manually-scale-pods"></a><span data-ttu-id="39d92-118">Mettre à l’échelle des pods manuellement</span><span class="sxs-lookup"><span data-stu-id="39d92-118">Manually scale pods</span></span>

<span data-ttu-id="39d92-119">Jusqu’à maintenant, le front-end Azure Vote et l’instance de Redis ont été déployés, chacun avec un réplica unique.</span><span class="sxs-lookup"><span data-stu-id="39d92-119">Thus far, the Azure Vote front-end and Redis instance have been deployed, each with a single replica.</span></span> <span data-ttu-id="39d92-120">À des fins de vérification, exécutez la commande [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="39d92-120">To verify, run the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="39d92-121">Output:</span><span class="sxs-lookup"><span data-stu-id="39d92-121">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

<span data-ttu-id="39d92-122">Modifiez manuellement le nombre de pods dans le déploiement `azure-vote-front` à l’aide de la commande [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale).</span><span class="sxs-lookup"><span data-stu-id="39d92-122">Manually change the number of pods in the `azure-vote-front` deployment using the [kubectl scale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) command.</span></span> <span data-ttu-id="39d92-123">Cet exemple augmente le nombre à 5.</span><span class="sxs-lookup"><span data-stu-id="39d92-123">This example increases the number to 5.</span></span>

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

<span data-ttu-id="39d92-124">Exécutez [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) pour vérifier que Kubernetes crée les pods.</span><span class="sxs-lookup"><span data-stu-id="39d92-124">Run [kubectl get pods](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) to verify that Kubernetes is creating the pods.</span></span> <span data-ttu-id="39d92-125">Au bout d’une minute environ, les pods supplémentaires sont en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="39d92-125">After a minute or so, the additional pods are running:</span></span>

```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="39d92-126">Output:</span><span class="sxs-lookup"><span data-stu-id="39d92-126">Output:</span></span>

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a><span data-ttu-id="39d92-127">Mettre à l’échelle les pods automatiquement</span><span class="sxs-lookup"><span data-stu-id="39d92-127">Autoscale pods</span></span>

<span data-ttu-id="39d92-128">Kubernetes prend en charge la [mise à l’échelle automatique des pods horizontaux](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) pour ajuster le nombre de pods dans un déploiement en fonction de l’utilisation du processeur ou d’autres métriques.</span><span class="sxs-lookup"><span data-stu-id="39d92-128">Kubernetes supports [horizontal pod autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) to adjust the number of pods in a deployment depending on CPU utilization or other select metrics.</span></span> 

<span data-ttu-id="39d92-129">Pour utiliser la mise à l’échelle automatique, vos pods doivent avoir des demandes et limites de processeur définies.</span><span class="sxs-lookup"><span data-stu-id="39d92-129">To use the autoscaler, your pods must have CPU requests and limits defined.</span></span> <span data-ttu-id="39d92-130">Dans le déploiement `azure-vote-front`, le conteneur frontal demande 0,25 processeur, avec une limite de 0,5 processeur.</span><span class="sxs-lookup"><span data-stu-id="39d92-130">In the `azure-vote-front` deployment, the front-end container requests 0.25 CPU, with a limit of 0.5 CPU.</span></span> <span data-ttu-id="39d92-131">Les paramètres s’apparentent aux suivants :</span><span class="sxs-lookup"><span data-stu-id="39d92-131">The settings look like:</span></span>

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

<span data-ttu-id="39d92-132">L’exemple suivant utilise la commande [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) pour mettre automatiquement à l’échelle le nombre de pods dans le déploiement `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="39d92-132">The following example uses the [kubectl autoscale](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) command to autoscale the number of pods in the `azure-vote-front` deployment.</span></span> <span data-ttu-id="39d92-133">Ici, si l’utilisation du processeur dépasse 50 %, le nombre de pods augmente jusqu’à un maximum de 10.</span><span class="sxs-lookup"><span data-stu-id="39d92-133">Here, if CPU utilization exceeds 50%, the autoscaler increases the pods to a maximum of 10.</span></span>


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

<span data-ttu-id="39d92-134">Pour voir l’état de la mise à l’échelle automatique, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="39d92-134">To see the status of the autoscaler, run the following command:</span></span>

```azurecli-interactive
kubectl get hpa
```

<span data-ttu-id="39d92-135">Output:</span><span class="sxs-lookup"><span data-stu-id="39d92-135">Output:</span></span>

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

<span data-ttu-id="39d92-136">Au bout de quelques minutes, avec une charge minimale sur l’application Azure Vote, le nombre de réplicas de pods descend automatiquement à 3.</span><span class="sxs-lookup"><span data-stu-id="39d92-136">After a few minutes, with minimal load on the Azure Vote app, the number of pod replicas decreases automatically to 3.</span></span>

## <a name="scale-the-agents"></a><span data-ttu-id="39d92-137">Mettre à l’échelle les agents</span><span class="sxs-lookup"><span data-stu-id="39d92-137">Scale the agents</span></span>

<span data-ttu-id="39d92-138">Si vous avez créé votre cluster Kubernetes à l’aide des commandes par défaut dans le didacticiel précédent, il comporte trois nœuds agents.</span><span class="sxs-lookup"><span data-stu-id="39d92-138">If you created your Kubernetes cluster using default commands in the previous tutorial, it has three agent nodes.</span></span> <span data-ttu-id="39d92-139">Vous pouvez ajuster le nombre d’agents manuellement si vous prévoyez davantage ou moins de charges de travail de conteneur sur votre cluster.</span><span class="sxs-lookup"><span data-stu-id="39d92-139">You can adjust the number of agents manually if you plan more or fewer container workloads on your cluster.</span></span> <span data-ttu-id="39d92-140">Utilisez la commande [az acs scale](/cli/azure/acs#scale), puis spécifiez le nombre d’agents avec le paramètre `--new-agent-count`.</span><span class="sxs-lookup"><span data-stu-id="39d92-140">Use the [az acs scale](/cli/azure/acs#scale) command, and specify the number of agents with the `--new-agent-count` parameter.</span></span>

<span data-ttu-id="39d92-141">L’exemple suivant permet d’augmenter le nombre de nœuds agents à 4 dans le cluster Kubernetes nommé *myK8sCluster*.</span><span class="sxs-lookup"><span data-stu-id="39d92-141">The following example increases the number of agent nodes to 4 in the Kubernetes cluster named *myK8sCluster*.</span></span> <span data-ttu-id="39d92-142">Quelques minutes sont nécessaires pour exécuter la commande.</span><span class="sxs-lookup"><span data-stu-id="39d92-142">The command takes a couple of minutes to complete.</span></span>

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

<span data-ttu-id="39d92-143">La sortie de la commande indique le nombre de nœuds agents dans la valeur de `agentPoolProfiles:count` :</span><span class="sxs-lookup"><span data-stu-id="39d92-143">The command output shows the number of agent nodes in the value of `agentPoolProfiles:count`:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="39d92-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="39d92-144">Next steps</span></span>

<span data-ttu-id="39d92-145">Dans ce didacticiel, vous avez utilisé différentes fonctionnalités de mise à l’échelle dans votre cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="39d92-145">In this tutorial, you used different scaling features in your Kubernetes cluster.</span></span> <span data-ttu-id="39d92-146">Les tâches traitées ont inclus :</span><span class="sxs-lookup"><span data-stu-id="39d92-146">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="39d92-147">Mise à l’échelle manuelle des pods Kubernetes</span><span class="sxs-lookup"><span data-stu-id="39d92-147">Manually scaling Kubernetes pods</span></span>
> * <span data-ttu-id="39d92-148">Configuration de la mise à l’échelle automatique des pods qui exécutent le front-end de l’application</span><span class="sxs-lookup"><span data-stu-id="39d92-148">Configuring Autoscale pods running the app front end</span></span>
> * <span data-ttu-id="39d92-149">Mettre à l’échelle les nœuds d’agents Azure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="39d92-149">Scale the Kubernetes Azure agent nodes</span></span>

<span data-ttu-id="39d92-150">Passez au didacticiel suivant pour en savoir plus sur la mise à jour d’une application dans Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="39d92-150">Advance to the next tutorial to learn about updating application in Kubernetes.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="39d92-151">Mettre à jour une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="39d92-151">Update an application in Kubernetes</span></span>](./container-service-tutorial-kubernetes-app-update.md)

