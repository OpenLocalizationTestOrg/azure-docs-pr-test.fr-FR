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
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="4334b-104">Créer toobe d’images de conteneur utilisé avec le Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="4334b-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="4334b-105">Dans ce didacticiel (le premier d’une série de sept), vous allez préparer une application à plusieurs conteneurs à son utilisation dans Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4334b-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="4334b-106">Les étapes effectuées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4334b-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="4334b-107">Le clonage de la source de l’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4334b-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="4334b-108">Création d’une image de conteneur à partir de la source de l’application hello</span><span class="sxs-lookup"><span data-stu-id="4334b-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="4334b-109">Test d’application hello dans un environnement de Docker local</span><span class="sxs-lookup"><span data-stu-id="4334b-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="4334b-110">Une fois terminé, hello suite de l’application est accessible dans votre environnement de développement local.</span><span class="sxs-lookup"><span data-stu-id="4334b-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="4334b-112">Dans les didacticiels suivants, image de conteneur hello est téléchargé tooan Registre de conteneur Azure, et puis exécutez dans Azure hébergés Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="4334b-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4334b-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4334b-113">Before you begin</span></span>

<span data-ttu-id="4334b-114">Ce didacticiel suppose une compréhension élémentaire des concepts Docker principaux tels que les conteneurs, les images de conteneur et les commandes Docker de base.</span><span class="sxs-lookup"><span data-stu-id="4334b-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="4334b-115">Si besoin, consultez [Bien démarrer avec Docker]( https://docs.docker.com/get-started/) pour apprendre les principes de base des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="4334b-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="4334b-116">toocomplete ce didacticiel, vous avez besoin d’un environnement de développement de Docker.</span><span class="sxs-lookup"><span data-stu-id="4334b-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="4334b-117">Docker fournit des packages qui le configurent facilement sur n’importe quel système [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="4334b-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="4334b-118">Obtenir le code d’application</span><span class="sxs-lookup"><span data-stu-id="4334b-118">Get application code</span></span>

<span data-ttu-id="4334b-119">exemple d’application Hello utilisé dans ce didacticiel est une application de base vote.</span><span class="sxs-lookup"><span data-stu-id="4334b-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="4334b-120">application Hello se compose d’un composant web frontal et une instance de Redis back-end.</span><span class="sxs-lookup"><span data-stu-id="4334b-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="4334b-121">le composant web Hello est empaqueté dans une image de conteneur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="4334b-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="4334b-122">instance de Redis Hello utilise une image non modifiée à partir de Hub d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="4334b-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="4334b-123">Utiliser git toodownload une copie de l’environnement de développement tooyour hello application.</span><span class="sxs-lookup"><span data-stu-id="4334b-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="4334b-124">Répertoire cloné de hello à l’intérieur est le code source de l’application hello, une Docker créée au préalable composer de fichiers et un fichier manifeste Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4334b-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="4334b-125">Ces fichiers sont actifs toocreate utilisés dans tout jeu de didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="4334b-126">Créer des images de conteneur</span><span class="sxs-lookup"><span data-stu-id="4334b-126">Create container images</span></span>

<span data-ttu-id="4334b-127">[Composition de docker](https://docs.docker.com/compose/) peut être utilisé de build de hello tooautomate en dehors des images de conteneur et de déploiement hello du conteneur de plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="4334b-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="4334b-128">Exécuter l’image de conteneur du fichier toocreate hello hello compose.yml de docker, téléchargement hello Redis image et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="4334b-129">Lorsque vous terminé, utilisez hello [images docker](https://docs.docker.com/engine/reference/commandline/images/) commande toosee les images hello créé.</span><span class="sxs-lookup"><span data-stu-id="4334b-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="4334b-130">Notez que les trois images ont été téléchargées ou créées.</span><span class="sxs-lookup"><span data-stu-id="4334b-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="4334b-131">Hello *avant de vote d’azure* image contient l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="4334b-132">Il a été dérivé hello *nginx-ballon* image.</span><span class="sxs-lookup"><span data-stu-id="4334b-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="4334b-133">image de Redis Hello a été téléchargé à partir du Hub d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="4334b-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="4334b-134">Exécutez hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) commande toosee hello conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4334b-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="4334b-135">Output:</span><span class="sxs-lookup"><span data-stu-id="4334b-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="4334b-136">Tester l’application localement</span><span class="sxs-lookup"><span data-stu-id="4334b-136">Test application locally</span></span>

<span data-ttu-id="4334b-137">Parcourir hello de toosee toohttp://localhost:8080 application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4334b-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="4334b-139">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="4334b-139">Clean up resources</span></span>

<span data-ttu-id="4334b-140">Maintenant que la fonctionnalité de l’application a été validée, hello conteneurs en cours d’exécution peut être arrêté et supprimé.</span><span class="sxs-lookup"><span data-stu-id="4334b-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="4334b-141">Ne supprimez pas les images de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-141">Do not delete hello container images.</span></span> <span data-ttu-id="4334b-142">Hello *avant de vote d’azure* image est l’instance de Registre de conteneur Azure tooan téléchargé dans l’étape suivante du didacticiel hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="4334b-143">Exécutez hello suivant hello toostop conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4334b-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="4334b-144">Supprimez les conteneurs de hello s’est arrêté avec hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="4334b-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="4334b-145">Une fois terminée, vous disposez d’une image de conteneur qui contient l’application Azure Vote hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4334b-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4334b-146">Next steps</span></span>

<span data-ttu-id="4334b-147">Dans ce didacticiel, une application a été testée et les images de conteneur est créé pour l’application hello.</span><span class="sxs-lookup"><span data-stu-id="4334b-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="4334b-148">Hello suit ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="4334b-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4334b-149">Source de l’application hello clonage à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4334b-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="4334b-150">La création d’une image conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="4334b-150">Created a container image from application source</span></span>
> * <span data-ttu-id="4334b-151">Application hello testée dans un environnement local de Docker</span><span class="sxs-lookup"><span data-stu-id="4334b-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="4334b-152">Avance toohello toolearn de didacticiel suivant sur le stockage des images de conteneur dans un Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="4334b-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4334b-153">Push images tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="4334b-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
