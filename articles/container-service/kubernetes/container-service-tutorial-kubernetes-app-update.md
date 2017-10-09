---
title: "didacticiel de Service de conteneur aaaAzure - application de la mise à jour | Documents Microsoft"
description: "Didacticiel Azure Container Service - Mettre à jour une application"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Mettre à jour une application dans Kubernetes

Après avoir déployé une application dans Kubernetes, vous pouvez la mettre à jour en spécifiant une nouvelle image conteneur ou une nouvelle version de l’image. Lorsque vous mettez à jour une application, déploiement de mise à jour hello soit préparé afin que seule une partie du déploiement de hello est mis à jour simultanément. Cette mise à jour intermédiaire hello application tookeep est en cours d’exécution pendant la mise à jour hello et qui offre un mécanisme de restauration cas d’échec du déploiement. 

Dans ce didacticiel, partie 6 de sept, Azure Vote exemple hello d’application est mise à jour. Les tâches que vous effectuez sont les suivantes :

> [!div class="checklist"]
> * Mise à jour le code d’application frontale hello
> * Création d’une image conteneur mise à jour
> * En exécutant un push hello conteneur image tooAzure Registre de conteneur
> * Déploiement d’image de conteneur mis à jour hello

Dans les didacticiels suivants Operations Management Suite est le cluster de Kubernetes hello toomonitor configuré.

## <a name="before-you-begin"></a>Avant de commencer

Dans les didacticiels précédents, une application a été empaquetée dans une image de conteneur, image de hello téléchargés tooAzure Registre de conteneur et un cluster Kubernetes créé. application Hello puis exécutée sur le cluster de Kubernetes hello. 

Si vous n’avez pas effectué ces étapes et que vous souhaitez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Mettre à jour l’application

toocomplete hello étapes décrites dans ce didacticiel, vous devez ont une copie clonée d’hello application de Vote de Azure. Si nécessaire, créez cette copie clonée avec hello de commande suivante :

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Ouvrez hello `config_file.cfg` fichier avec un éditeur de code ou de texte. Vous pouvez trouver ce fichier sous hello suivant le répertoire de dépôt de hello cloné.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Modifier les valeurs hello de `VOTE1VALUE` et `VOTE2VALUE`, puis enregistrez le fichier de hello.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Utilisez [composer de docker](https://docs.docker.com/compose/) toore-créer une image frontal de hello et application hello exécution mis à jour.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Tester l’application localement

Parcourir trop`http://localhost:8080` toosee hello mis à jour l’application.

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Marquer et envoyer des images

Hello de balise *avant de vote d’azure* image avec loginServer hello du Registre de conteneur hello.

Si vous utilisez le Registre de conteneur Azure, obtenir le nom du serveur hello avec hello [liste d’acr az](/cli/azure/acr#list) commande.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Utilisez [balise de docker](https://docs.docker.com/engine/reference/commandline/tag/) image de hello tootag. Remplacez `<acrLoginServer>` par le nom de votre serveur de connexion Azure Container Registry ou par votre nom d’hôte de registre public.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Utilisez [push de docker](https://docs.docker.com/engine/reference/commandline/push/) Registre de tooyour tooupload hello image. Remplacez `<acrLoginServer>` par le nom de votre serveur de connexion Azure Container Registry ou par votre nom d’hôte de registre public.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Déployer l’application mise à jour

tooensure des temps de fonctionnement maximale, plusieurs instances du bloc d’application hello doivent être en cours d’exécution. Vérifier cette configuration avec hello [kubectl obtenir pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.

```bash
kubectl get pod
```

Output:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Si vous n’avez pas plusieurs blocs d’image d’azure-vote-front hello en cours d’exécution, à l’échelle hello *avant de vote d’azure* déploiement.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

application de hello tooupdate, utilisez hello [kubectl ensemble](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) commande. Mise à jour `<acrLoginServer>` avec le nom de serveur ou l’hôte de connexion de votre Registre de conteneur hello.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

déploiement de hello toomonitor, utilisez hello [kubectl obtenir pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande. Comme l’application hello mis à jour est déployée, votre POD terminer une commande et recréées avec la nouvelle image de conteneur hello.

```azurecli-interactive
kubectl get pod
```

Output:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Tester l’application mise à jour

Obtenir l’adresse IP externe de hello Hello *avant de vote d’azure* service.

```azurecli-interactive
kubectl get service azure-vote-front
```

Parcourir toohello IP adresse toosee hello mis à jour l’application.

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous mis à jour d’une application et transférée à ce cluster de Kubernetes tooa mise à jour. Bonjour tâches suivantes ont été effectuée :

> [!div class="checklist"]
> * Code d’application frontale hello mis à jour
> * Création d’une image conteneur mise à jour
> * Objet d’un push hello conteneur image tooAzure Registre de conteneur
> * Application déployée hello mis à jour

Toohello toolearn de didacticiel suivant sur la façon d’avance toomonitor Kubernetes avec Operations Management Suite.

> [!div class="nextstepaction"]
> [Surveiller Kubernetes avec OMS](./container-service-tutorial-kubernetes-monitor.md)