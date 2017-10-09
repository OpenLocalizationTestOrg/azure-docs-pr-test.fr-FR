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
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Mettre à l’échelle des pods Kubernetes et l’infrastructure Kubernetes

Si vous avez effectué les didacticiels de hello, vous avez une Kubernetes cluster dans le conteneur de Service Azure et que vous avez déployé l’application Azure vote de hello. 

Dans ce didacticiel, partie 5, 7, vous montée en puissance parallèle POD hello dans l’application hello et essayez d’échelle de pod. Vous apprendrez également comment le nombre de hello tooscale de toochange de nœuds de l’agent de machine virtuelle Azure hello capacité du cluster pour l’hébergement des charges de travail. Les tâches accomplies sont les suivantes :

> [!div class="checklist"]
> * Mise à l’échelle manuelle des pods Kubernetes
> * Configuration des blocs de mise à l’échelle le frontal application hello en cours d’exécution
> * Mettre à l’échelle des nœuds de l’agent Azure hello Kubernetes

Dans les didacticiels suivants hello application de Vote de Azure est mis à jour et Operations Management Suite configuré le cluster de Kubernetes toomonitor hello.

## <a name="before-you-begin"></a>Avant de commencer

Dans les didacticiels précédents, une application a été empaquetée dans une image de conteneur, cette image téléchargée tooAzure Registre de conteneur et un cluster Kubernetes créé. application Hello puis exécutée sur le cluster de Kubernetes hello. Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner toohello [didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md). 

Ce didacticiel nécessite au minimum un cluster Kubernetes avec une application en cours d’exécution.

## <a name="manually-scale-pods"></a>Mettre à l’échelle des pods manuellement

Jusqu'à présent, hello Vote Azure frontal et instance Redis ont été déployées, chacune avec un seul réplica. tooverify, exécutez hello [kubectl obtenir](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.

```azurecli-interactive
kubectl get pods
```

Output:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Modifier manuellement le nombre de hello de POD Bonjour `azure-vote-front` déploiement à l’aide de hello [kubectl échelle](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) commande. Cet exemple augmente too5 numéro de hello.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Exécutez [kubectl obtenir POD](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify que Kubernetes crée les POD hello. Après environ une minute, POD supplémentaires de hello est en cours d’exécution :

```azurecli-interactive
kubectl get pods
```

Output:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Mettre à l’échelle les pods automatiquement

Prend en charge les Kubernetes [pod horizontal échelle](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) nombre de hello tooadjust de blocs dans un déploiement en fonction de l’utilisation du processeur ou d’autres sélectionner des mesures. 

toouse hello autoscaler, votre POD doit avoir des demandes de l’UC et les limites définies. Bonjour `azure-vote-front` déploiement, hello du processeur de requêtes 0,25 conteneur frontal, avec une limite de 0,5 UC. paramètres de Hello ressembler à :

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

exemple Hello utilise hello [kubectl mise à l’échelle](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) commande le nombre de hello tooautoscale de POD Bonjour `azure-vote-front` déploiement. Ici, si l’utilisation du processeur dépasse 50 %, hello autoscaler augmente hello POD tooa 10 au maximum.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

état de hello toosee d’autoscaler hello, exécutez hello de commande suivante :

```azurecli-interactive
kubectl get hpa
```

Output:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Après quelques minutes, avec une charge minimale sur l’application de Vote de Azure hello, hello nombre de réplicas de pod diminue automatiquement too3.

## <a name="scale-hello-agents"></a>Agents de mise à l’échelle hello

Si vous avez créé votre cluster Kubernetes à l’aide des commandes par défaut dans le cadre du didacticiel précédent hello, il a trois nœuds de l’agent. Vous pouvez ajuster nombre hello d’agents manuellement si vous envisagez de charges de travail plus ou moins de conteneur sur votre cluster. Hello d’utilisation [mettre à l’échelle des services acs az](/cli/azure/acs#scale) de commandes et spécifiez le nombre hello d’agents avec hello `--new-agent-count` paramètre.

Hello exemple suivant augmente nombre hello de too4 de nœuds de l’agent dans le cluster de Kubernetes hello nommé *myK8sCluster*. commande Hello prend quelques minutes toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Hello sortie de la commande affiche hello numéro de l’agent de nœuds de valeur hello `agentPoolProfiles:count`:

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

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez utilisé différentes fonctionnalités de mise à l’échelle dans votre cluster Kubernetes. Les tâches traitées ont inclus :

> [!div class="checklist"]
> * Mise à l’échelle manuelle des pods Kubernetes
> * Configuration des blocs de mise à l’échelle le frontal application hello en cours d’exécution
> * Mettre à l’échelle des nœuds de l’agent Azure hello Kubernetes

Toohello toolearn de didacticiel suivant sur la mise à jour d’application dans Kubernetes d’avance.

> [!div class="nextstepaction"]
> [Mettre à jour une application dans Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

