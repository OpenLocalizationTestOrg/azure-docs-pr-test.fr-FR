---
title: "didacticiel d’Instances de conteneurs aaaAzure - préparer un Registre de conteneur Azure | Documents Microsoft"
description: "Didacticiel Azure Container Instances - Préparer Azure Container Registry"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, microservices, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 2525626125740c3c861fad36aad207d0b587ff54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-use-azure-container-registry"></a>Déployer et utiliser Azure Container Registry

Il s’agit de la deuxième partie d’un didacticiel en trois parties. Bonjour [précédemment](./container-instances-tutorial-prepare-app.md), une image de conteneur a été créée pour une application web simple écrite [Node.js](http://nodejs.org). Dans ce didacticiel, cette image est transmise tooan Registre de conteneur Azure. Si vous n’avez pas créé image de conteneur hello, retourner trop[didacticiel 1 : créer une image de conteneur](./container-instances-tutorial-prepare-app.md). 

Hello Registre de conteneur Azure est un registre basé sur Azure, privé, pour les images de conteneur Docker. Ce didacticiel Guide de déploiement d’une instance de Registre de conteneur Azure et l’envoi d’un tooit d’image de conteneur. Les étapes terminées sont les suivantes :

> [!div class="checklist"]
> * Déploiement d’une instance Azure Container Registry
> * Balisage d’image conteneur pour Azure Container Registry
> * Télécharger l’image tooAzure Registre de conteneur

Dans les didacticiels suivants vous déployez le conteneur de hello à partir de votre tooAzure Registre privé les Instances du conteneur.

## <a name="before-you-begin"></a>Avant de commencer

Ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="deploy-azure-container-registry"></a>Déployer Azure Container Registry

Lorsque vous déployez un registre de conteneurs Azure, il vous faut tout d’abord un groupe de ressources. Un groupe de ressources Azure est une collection logique dans laquelle des ressources Azure sont déployées et gérées.

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Dans cet exemple, un groupe de ressources nommé *myResourceGroup* est créé dans hello *eastus* région.

```azurecli
az group create --name myResourceGroup --location eastus
```

Créer un Registre de conteneur Azure avec hello [az acr créer](/cli/azure/acr#create) commande. nom d’un Registre de conteneur de Hello **doit être unique**. Bonjour l’exemple suivant, nous utilisons le nom de hello *mycontainerregistry082*.

```azurecli
az acr create --resource-group myResourceGroup --name mycontainerregistry082 --sku Basic --admin-enabled true
```

Dans l’ensemble de rest hello de ce didacticiel, nous utilisons `<acrname>` comme espace réservé pour le nom du Registre hello conteneur que vous avez choisi.

## <a name="container-registry-login"></a>Connexion au registre de conteneurs

Vous devez vous connecter dans l’instance ACR tooyour avant d’installer des images tooit. Hello d’utilisation [connexion d’acr az](https://docs.microsoft.com/en-us/cli/azure/acr#login) opération de hello toocomplete de commandes. Vous devez tooprovide hello unique nom Registre de conteneur toohello lors de sa création.

```azurecli
az acr login --name <acrName>
```

commande Hello renvoie un message de succès de la connexion une fois terminé.

## <a name="tag-container-image"></a>Baliser l’image de conteneur

toodeploy une image de conteneur à partir d’un Registre privé, image de hello doit toobe balisé avec hello `loginServer` nom du Registre de hello.

toosee une liste d’images en cours, utilisez hello `docker images` commande.

```bash
docker images
```

Output:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

nom de loginServer hello tooget, exécutez hello commande suivante.

```azurecli
az acr show --name <acrName> --query loginServer --output table
```

Hello de balise *aci-didacticiel-app* image avec loginServer hello du Registre de conteneur hello. En outre, ajoutez `:v1` fin toohello de nom de l’image hello. Cette balise indique le numéro de version d’image hello.

```bash
docker tag aci-tutorial-app <acrLoginServer>/aci-tutorial-app:v1
```

Une fois que balisé, exécutez `docker images` opération hello de tooverify.

```bash
docker images
```

Output:

```bash
REPOSITORY                                                TAG                 IMAGE ID            CREATED             SIZE
aci-tutorial-app                                          latest              5c745774dfa9        39 seconds ago      68.1 MB
mycontainerregistry082.azurecr.io/aci-tutorial-app        v1                  a9dace4e1a17        7 minutes ago       68.1 MB
```

## <a name="push-image-tooazure-container-registry"></a>Push image tooAzure Registre de conteneur

Push hello *aci-didacticiel-app* Registre toohello d’images.

À l’aide de hello l’exemple suivant, remplacez hello conteneur Registre loginServer par loginServer hello à partir de votre environnement.

```bash
docker push <acrLoginServer>/aci-tutorial-app:v1
```

## <a name="list-images-in-azure-container-registry"></a>Énumérer les images dans Azure Container Registry

tooreturn une liste d’images qui ont été déplacées du Registre le conteneur Azure tooyour, hello d’utilisateur [liste des référentiels az acr](/cli/azure/acr/repository#list) commande. Mettre à jour la commande hello par le nom de Registre de conteneur hello.

```azurecli
az acr repository list --name <acrName> --output table
```

Output:

```azurecli
Result
----------------
aci-tutorial-app
```

Puis les balises de hello toosee d’une image spécifique, utilisez hello [az acr référentiel afficher-balises](/cli/azure/acr/repository#show-tags) commande.

```azurecli
az acr repository show-tags --name <acrName> --repository aci-tutorial-app --output table
```

Output:

```azurecli
Result
--------
v1
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, un Registre de conteneur Azure a été préparé pour une utilisation avec les Instances du conteneur Azure et image de conteneur hello a été envoyée. Hello suit ont été effectuée :

> [!div class="checklist"]
> * Déploiement d’une instance Azure Container Registry
> * Balisage d’image conteneur pour Azure Container Registry
> * Télécharger l’image tooAzure Registre de conteneur

Avance toohello toolearn de didacticiel suivant sur le déploiement de hello tooAzure de conteneur à l’aide d’Instances de conteneurs Azure.

> [!div class="nextstepaction"]
> [Déployer des conteneurs tooAzure Instances de conteneurs](./container-instances-tutorial-deploy-app.md)
