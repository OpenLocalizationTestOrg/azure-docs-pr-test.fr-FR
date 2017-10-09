---
title: "didacticiel de Service de conteneur aaaAzure - déployer une Application | Documents Microsoft"
description: "Didacticiel Azure Container Service - Déployer une application"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Exécuter des applications dans Kubernetes

Dans ce didacticiel (le quatrième d’une série de sept), un exemple d’application est déployé dans un cluster Kubernetes. Les étapes terminées sont les suivantes :

> [!div class="checklist"]
> * Télécharger les fichiers manifeste Kubernetes
> * Exécuter une application dans Kubernetes
> * Tester l’application hello

Dans les didacticiels suivants, cette application est monté en charge, mises à jour, et Operations Management Suite configuré le cluster de Kubernetes toomonitor hello.

Ce didacticiel suppose une compréhension élémentaire des concepts de Kubernetes, pour plus d’informations sur Kubernetes voir hello [Kubernetes documentation](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Avant de commencer

Dans les didacticiels précédents, une application a été empaquetée dans une image de conteneur, cette image a été téléchargé tooAzure Registre de conteneur et un cluster Kubernetes a été créé. Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md). 

Au minimum, ce didacticiel nécessite un cluster Kubernetes.

## <a name="get-manifest-file"></a>Obtenir un fichier manifeste

Pour ce didacticiel, les [objets Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) sont déployés à l’aide d’un manifeste Kubernetes. Un manifeste Kubernetes est un fichier YAML ou JSON contenant des instructions de configuration et de déploiement pour l’objet Kubernetes.

fichier manifeste d’application Hello pour ce didacticiel est disponible dans le référentiel d’application hello Vote de Azure, qui a été cloné dans un didacticiel précédent. Si vous ne le n'avez pas déjà fait, cloner le référentiel de hello avec hello de commande suivante : 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

fichier de manifeste Hello se trouve dans hello suivant le répertoire de dépôt de hello cloné.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Mettre à jour le fichier manifeste

Si vous utilisez des images de conteneur de Registre de conteneur Azure toostore hello, hello toobe besoins manifeste mis à jour avec le nom de loginServer l’ACR hello.

Obtenir le nom de serveur hello ACR connexion avec hello [liste d’acr az](/cli/azure/acr#list) commande.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Hello exemple manifeste a été créé au préalable avec un nom de référentiel de *microsoft*. Ouvrir le fichier de hello avec n’importe quel éditeur de texte et remplacez hello *microsoft* valeur avec le nom du serveur de connexion de votre instance ACR hello.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Déployer l’application

Hello d’utilisation [kubectl créer](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) application hello de toorun de commande. Cette commande analyse hello fichier manifeste et créer des objets de Kubernetes de hello défini.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Output:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Tester l’application

A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) est créé qui expose hello application toohello internet. Ce processus peut prendre plusieurs minutes. 

cours toomonitor, utilisez hello [kubectl obtenir service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) avec hello `--watch` argument.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Au départ, hello **IP externe** pour hello *avant de vote d’azure* service apparaît sous la forme *en attente*. Une fois que l’adresse de hello IP externe a été modifiée à partir de *en attente* tooan *adresse IP*, utilisez `CTRL-C` processus d’observation kubectl toostop hello.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

application hello toosee, parcourir toohello une adresse IP externe.

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, hello application de vote Azure a été déployé tooan Azure conteneur Service Kubernetes cluster. Les tâches accomplies sont les suivantes :  

> [!div class="checklist"]
> * Téléchargement des fichiers manifeste Kubernetes
> * Exécutez l’application hello dans Kubernetes
> * Application hello testée

Toohello toolearn de didacticiel suivant sur la mise à l’échelle une application de Kubernetes et le hello sous-jacent Kubernetes infrastructure d’avance. 

> [!div class="nextstepaction"]
> [Mettre à l’échelle l’application et l’infrastructure Kubernetes](./container-service-tutorial-kubernetes-scale.md)