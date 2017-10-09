---
title: "aaaAzure didacticiel d’Instances de conteneurs - préparer votre application | Documentation Azure"
description: "Préparer une application pour le déploiement tooAzure Instances de conteneurs"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a>Créer un conteneur pour un déploiement tooAzure Instances de conteneurs

Azure Container Instances permet de déployer des conteneurs Docker sur l’infrastructure Azure sans configurer de machines virtuelles ni adopter de service de niveau supérieur. Dans ce didacticiel, vous allez voir comment générer une application web basique dans Node.js, et comment la placer comme package dans un conteneur pouvant être exécuté avec Azure Container Instances. Nous aborderons :

> [!div class="checklist"]
> * Le clonage de la source de l’application à partir de GitHub  
> * la création des images de conteneur à partir de la source de l’application
> * Test des images de hello dans un environnement de Docker local

Dans les didacticiels suivants vous téléchargez votre tooan image Registre de conteneur Azure et ensuite déployer les Instances de conteneurs tooAzure.

## <a name="before-you-begin"></a>Avant de commencer

Ce didacticiel suppose une compréhension élémentaire des concepts Docker principaux tels que les conteneurs, les images de conteneur et les commandes Docker de base. Si besoin, consultez [Bien démarrer avec Docker]( https://docs.docker.com/get-started/) pour apprendre les principes de base des conteneurs. 

toocomplete ce didacticiel, vous avez besoin d’un environnement de développement de Docker. Docker fournit des packages qui le configurent facilement sur n’importe quel système [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obtenir le code d’application

exemple Hello dans ce didacticiel inclut une application web simple générée dans [Node.js](http://nodejs.org). application Hello sert d’une page HTML statique et ressemble à ceci :

![Application du didacticiel affichée dans le navigateur][aci-tutorial-app]

Utiliser git toodownload hello, exemple :

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a>Générer l’image de conteneur hello

Hello Dockerfile fourni dans le référentiel d’exemple hello montre la façon dont le conteneur de hello est construit. Il démarre à partir d’un [officiel Node.js image] [ dockerhub-nodeimage] selon [Linux Alpine](https://alpinelinux.org/), une distribution petite qui est parfaitement toouse avec des conteneurs. Ensuite, il copie les fichiers de l’application hello dans le conteneur de hello, installe les dépendances à l’aide de hello Node Package Manager et enfin démarre application hello.

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

Hello d’utilisation `docker build` image de conteneur de commande toocreate hello, en tant que balisage *aci-didacticiel-app*:

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

Hello d’utilisation `docker images` image hello généré de toosee :

```bash
docker images
```

Output:

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a>Conteneur d’exécution hello localement

Avant d’essayer de déploiement hello conteneur tooAzure les Instances du conteneur, l’exécuter localement tooconfirm qu’il fonctionne. Hello `-d` commutateur permet de conteneur de hello s’exécutent en arrière-plan de hello, tandis que `-p` vous permet de toomap un port arbitraire sur votre tooport calcul 80 dans le conteneur de hello.

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

Ouvrez hello navigateur toohttp://localhost:8080 tooconfirm qui hello conteneur est en cours d’exécution.

![Application hello exécutée localement dans le navigateur de hello][aci-tutorial-app-local]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez créé une image de conteneur qui peut être des Instances de conteneurs tooAzure déployé. Hello suit ont été effectuée :

> [!div class="checklist"]
> * Source de l’application hello clonage à partir de GitHub  
> * la création des images de conteneur à partir de la source de l’application
> * Test conteneur hello localement

Avance toohello toolearn de didacticiel suivant sur le stockage des images de conteneur dans un Registre de conteneur Azure.

> [!div class="nextstepaction"]
> [Push images tooAzure Registre de conteneur](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png