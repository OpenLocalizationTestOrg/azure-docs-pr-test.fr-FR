---
title: "didacticiel de Service de conteneur aaaAzure - préparer un ACR | Documents Microsoft"
description: "Didacticiel Azure Container Service - Préparer l’ACR"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 3980e5ce4eb9836f83c761a2f76c944bb3f13060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Déployer et utiliser Azure Container Registry

Azure Container Registry (ACR) est un registre privé Azure pour les images de conteneur Docker. Ce didacticiel, la partie deux des sept, Guide de déploiement d’une instance de Registre de conteneur Azure et l’envoi d’un tooit d’image de conteneur. Les étapes terminées sont les suivantes :

> [!div class="checklist"]
> * Déploiement d’une instance Azure Container Registry (ACR)
> * Marquage d’une image conteneur pour ACR
> * Téléchargement hello image tooACR

Dans les didacticiels suivants, cette instance ACR est intégrée à un cluster Azure Container Service Kubernetes, pour l’exécution des images de conteneur en toute sécurité. 

## <a name="before-you-begin"></a>Avant de commencer

Bonjour [didacticiel précédent](./container-service-tutorial-kubernetes-prepare-app.md), une image de conteneur a été créée pour une application Azure vote simple. Dans ce didacticiel, cette image est transmise tooan Registre de conteneur Azure. Si vous n’avez pas créé image des application Azure vote hello, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md). Vous pouvez également hello étapes détaillées ici fonctionnent avec n’importe quelle image de conteneur.

Ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="deploy-azure-container-registry"></a>Déployer Azure Container Registry

Lorsque vous déployez un registre de conteneurs Azure, il vous faut tout d’abord un groupe de ressources. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées.

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Dans cet exemple, un groupe de ressources nommé *myResourceGroup* est créé dans hello *westeurope* région.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Créer un Registre de conteneur Azure avec hello [az acr créer](/cli/azure/acr#create) commande. nom d’un Registre de conteneur de Hello **doit être unique**.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Basic --admin-enabled true
```

Dans l’ensemble de rest hello de ce didacticiel, nous utilisons « acrname » comme espace réservé pour le nom du Registre hello conteneur que vous avez choisi.

## <a name="container-registry-login"></a>Connexion au registre de conteneurs

Vous devez vous connecter dans l’instance ACR tooyour avant d’installer des images tooit. Hello d’utilisation [connexion d’acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) opération de hello toocomplete de commandes. Vous devez tooprovide hello unique nom Registre de conteneur toohello lors de sa création.

```azurecli
az acr login --name <acrName>
```

commande Hello renvoie un message de succès de la connexion une fois terminé.

## <a name="tag-container-images"></a>Marquer les images de conteneur

Chaque image de conteneur doit toobe balisé avec le nom de loginServer hello du Registre de hello. Cette balise est utilisée pour le routage lors de la distribution du Registre de conteneur images tooan image.

toosee une liste d’images en cours, utilisez hello [images docker](https://docs.docker.com/engine/reference/commandline/images/) commande.

```bash
docker images
```

Output:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front             latest              4675398c9172        13 minutes ago      694MB
redis                        latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask               788ca94b2313        9 months ago        694MB
```

nom de loginServer hello tooget, exécutez hello commande suivante.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Maintenant, hello de balise *avant de vote d’azure* image avec loginServer hello du Registre de conteneur hello. En outre, ajoutez `:redis-v1` fin toohello de nom de l’image hello. Cette balise indique la version de l’image hello.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v1
```

Une fois balisé, réexécutez [images docker] (https://docs.docker.com/engine/reference/commandline/images/) tooverify hello.

```bash
docker images
```

Output:

```bash
REPOSITORY                                           TAG                 IMAGE ID            CREATED             SIZE
azure-vote-front                                     latest              eaf2b9c57e5e        8 minutes ago       716 MB
mycontainerregistry082.azurecr.io/azure-vote-front   redis-v1            eaf2b9c57e5e        8 minutes ago       716 MB
redis                                                latest              a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask                           flask               788ca94b2313        8 months ago        694 MB
```

## <a name="push-images-tooregistry"></a>Push tooregistry d’images

Push hello *avant de vote d’azure* Registre toohello d’images. 

À l’aide de hello l’exemple suivant, remplacez hello ACR loginServer par loginServer hello à partir de votre environnement.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v1
```

Cette opération prend quelques minutes toocomplete.

## <a name="list-images-in-registry"></a>Créer la liste des images du registre

tooreturn une liste d’images qui ont été déplacées du Registre le conteneur Azure tooyour, hello d’utilisateur [liste des référentiels az acr](/cli/azure/acr/repository#list) commande. Mettre à jour la commande hello avec le nom de l’instance ACR hello.

```azurecli
az acr repository list --name <acrName> --output table
```

Output:

```azurecli
Result
----------------
azure-vote-front
```

Puis les balises de hello toosee d’une image spécifique, utilisez hello [az acr référentiel afficher-balises](/cli/azure/acr/repository#show-tags) commande.

```azurecli
az acr repository show-tags --name <acrName> --repository azure-vote-front --output table
```

Output:

```azurecli
Result
--------
redis-v1
```

À l’achèvement de didacticiel, image de conteneur hello ayant été stockée dans une instance de Registre de conteneur Azure privée. Cette image est déployée à partir du cluster ACR tooa Kubernetes dans les didacticiels suivants.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, un registre de conteneurs Azure a été préparé pour une utilisation dans un cluster ACS Kubernetes. Hello suit ont été effectuée :

> [!div class="checklist"]
> * Déploiement d’une instance Azure Container Registry
> * Marquage d’une image conteneur pour ACR
> * Hello téléchargé image tooACR

Avance toohello toolearn de didacticiel suivant sur le déploiement d’un cluster Kubernetes dans Azure.

> [!div class="nextstepaction"]
> [Déployer un cluster Kubernetes](./container-service-tutorial-kubernetes-deploy-cluster.md)