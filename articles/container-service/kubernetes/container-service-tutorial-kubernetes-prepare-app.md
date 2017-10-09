---
title: "didacticiel de Service de conteneur aaaAzure - préparer une application | Documents Microsoft"
description: "Didacticiel Azure Container Service - Préparer l’application"
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
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Créer toobe d’images de conteneur utilisé avec le Service de conteneur Azure

Dans ce didacticiel (le premier d’une série de sept), vous allez préparer une application à plusieurs conteneurs à son utilisation dans Kubernetes. Les étapes effectuées sont les suivantes :  

> [!div class="checklist"]
> * Le clonage de la source de l’application à partir de GitHub  
> * Création d’une image de conteneur à partir de la source de l’application hello
> * Test d’application hello dans un environnement de Docker local

Une fois terminé, hello suite de l’application est accessible dans votre environnement de développement local.

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

Dans les didacticiels suivants, image de conteneur hello est téléchargé tooan Registre de conteneur Azure, et puis exécutez dans Azure hébergés Kubernetes cluster.

## <a name="before-you-begin"></a>Avant de commencer

Ce didacticiel suppose une compréhension élémentaire des concepts Docker principaux tels que les conteneurs, les images de conteneur et les commandes Docker de base. Si besoin, consultez [Bien démarrer avec Docker]( https://docs.docker.com/get-started/) pour apprendre les principes de base des conteneurs. 

toocomplete ce didacticiel, vous avez besoin d’un environnement de développement de Docker. Docker fournit des packages qui le configurent facilement sur n’importe quel système [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Obtenir le code d’application

exemple d’application Hello utilisé dans ce didacticiel est une application de base vote. application Hello se compose d’un composant web frontal et une instance de Redis back-end. le composant web Hello est empaqueté dans une image de conteneur personnalisée. instance de Redis Hello utilise une image non modifiée à partir de Hub d’ancrage.  

Utiliser git toodownload une copie de l’environnement de développement tooyour hello application.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Répertoire cloné de hello à l’intérieur est le code source de l’application hello, une Docker créée au préalable composer de fichiers et un fichier manifeste Kubernetes. Ces fichiers sont actifs toocreate utilisés dans tout jeu de didacticiel hello. 

## <a name="create-container-images"></a>Créer des images de conteneur

[Composition de docker](https://docs.docker.com/compose/) peut être utilisé de build de hello tooautomate en dehors des images de conteneur et de déploiement hello du conteneur de plusieurs applications.

Exécuter l’image de conteneur du fichier toocreate hello hello compose.yml de docker, téléchargement hello Redis image et démarrer l’application hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Lorsque vous terminé, utilisez hello [images docker](https://docs.docker.com/engine/reference/commandline/images/) commande toosee les images hello créé.

```bash
docker images
```

Notez que les trois images ont été téléchargées ou créées. Hello *avant de vote d’azure* image contient l’application hello. Il a été dérivé hello *nginx-ballon* image. image de Redis Hello a été téléchargé à partir du Hub d’ancrage.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Exécutez hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) commande toosee hello conteneurs en cours d’exécution.

```bash
docker ps
```

Output:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Tester l’application localement

Parcourir hello de toosee toohttp://localhost:8080 application en cours d’exécution.

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Supprimer des ressources

Maintenant que la fonctionnalité de l’application a été validée, hello conteneurs en cours d’exécution peut être arrêté et supprimé. Ne supprimez pas les images de conteneur hello. Hello *avant de vote d’azure* image est l’instance de Registre de conteneur Azure tooan téléchargé dans l’étape suivante du didacticiel hello.

Exécutez hello suivant hello toostop conteneurs en cours d’exécution.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Supprimez les conteneurs de hello s’est arrêté avec hello commande suivante.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Une fois terminée, vous disposez d’une image de conteneur qui contient l’application Azure Vote hello.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, une application a été testée et les images de conteneur est créé pour l’application hello. Hello suit ont été effectuée :

> [!div class="checklist"]
> * Source de l’application hello clonage à partir de GitHub  
> * La création d’une image conteneur à partir de la source de l’application
> * Application hello testée dans un environnement local de Docker

Avance toohello toolearn de didacticiel suivant sur le stockage des images de conteneur dans un Registre de conteneur Azure.

> [!div class="nextstepaction"]
> [Push images tooAzure Registre de conteneur](./container-service-tutorial-kubernetes-prepare-acr.md)
