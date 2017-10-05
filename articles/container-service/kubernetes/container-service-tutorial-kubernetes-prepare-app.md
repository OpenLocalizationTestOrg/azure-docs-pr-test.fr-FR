---
title: "Didacticiel Azure Container Service - Préparer l’application | Microsoft Docs"
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
ms.openlocfilehash: f02ee61ef1cd3b3dfaa051cfabe52866e3e7e838
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a><span data-ttu-id="6dcf4-104">Créer des images de conteneur à utiliser avec Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="6dcf4-104">Create container images to be used with Azure Container Service</span></span>

<span data-ttu-id="6dcf4-105">Dans ce didacticiel (le premier d’une série de sept), vous allez préparer une application à plusieurs conteneurs à son utilisation dans Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="6dcf4-106">Les étapes effectuées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6dcf4-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="6dcf4-107">Clonage de la source de l’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="6dcf4-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="6dcf4-108">Création d’une image conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="6dcf4-108">Creating a container image from the application source</span></span>
> * <span data-ttu-id="6dcf4-109">Test de l’application dans un environnement Docker local</span><span class="sxs-lookup"><span data-stu-id="6dcf4-109">Testing the application in a local Docker environment</span></span>

<span data-ttu-id="6dcf4-110">Une fois ces étapes effectuées, l’application suivante est accessible dans votre environnement de développement local.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-110">Once completed, the following application is accessible in your local development environment.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="6dcf4-112">Dans les didacticiels suivants, l’image conteneur est chargée dans Azure Container Registry, puis exécutée dans le cluster Kubernetes hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6dcf4-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6dcf4-113">Before you begin</span></span>

<span data-ttu-id="6dcf4-114">Ce didacticiel suppose une compréhension élémentaire des concepts Docker principaux tels que les conteneurs, les images de conteneur et les commandes Docker de base.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="6dcf4-115">Si besoin, consultez [Bien démarrer avec Docker]( https://docs.docker.com/get-started/) pour apprendre les principes de base des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="6dcf4-116">Pour terminer ce didacticiel, il vous faut un environnement de développement Docker.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-116">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="6dcf4-117">Docker fournit des packages qui le configurent facilement sur n’importe quel système [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="6dcf4-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="6dcf4-118">Obtenir le code d’application</span><span class="sxs-lookup"><span data-stu-id="6dcf4-118">Get application code</span></span>

<span data-ttu-id="6dcf4-119">L’exemple d’application utilisé dans ce didacticiel est une application de votes de base.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-119">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="6dcf4-120">L’application est constituée d’un composant web frontal et d’une instance Redis principale.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-120">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="6dcf4-121">Le composant web est empaqueté dans une image conteneur personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-121">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="6dcf4-122">L’instance Redis utilise une image non modifiée de Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-122">The Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="6dcf4-123">Utilisez git pour télécharger une copie de l’application dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-123">Use git to download a copy of the application to your development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="6dcf4-124">Dans le répertoire cloné se trouvent le code source de l’application, un fichier Docker Compose précréé et un fichier manifeste Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-124">Inside the cloned directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="6dcf4-125">Ces fichiers sont utilisés pour créer des ressources tout au long de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-125">These files are used to create assets throughout the tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="6dcf4-126">Créer des images de conteneur</span><span class="sxs-lookup"><span data-stu-id="6dcf4-126">Create container images</span></span>

<span data-ttu-id="6dcf4-127">[Docker Compose](https://docs.docker.com/compose/) peut être utilisé pour automatiser la génération à partir des images conteneur, ainsi que le déploiement des applications à plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-127">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="6dcf4-128">Exécutez le fichier docker-compose.yml pour créer l’image conteneur, télécharger l’image Redis, puis démarrez l’application.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-128">Run the docker-compose.yml file to create the container image, download the Redis image, and start the application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="6dcf4-129">Une fois terminé, utilisez la commande [docker images](https://docs.docker.com/engine/reference/commandline/images/) pour afficher les images créées.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-129">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span></span>

```bash
docker images
```

<span data-ttu-id="6dcf4-130">Notez que les trois images ont été téléchargées ou créées.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="6dcf4-131">L’image *azure-vote-front* contient l’application.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-131">The *azure-vote-front* image contains the application.</span></span> <span data-ttu-id="6dcf4-132">Cette image est dérivée de l’image *nginx-flask*.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-132">It was derived from the *nginx-flask* image.</span></span> <span data-ttu-id="6dcf4-133">L’image Redis a été téléchargée à partir de Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-133">The Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="6dcf4-134">Exécutez la commande [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) pour voir les conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-134">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="6dcf4-135">Output:</span><span class="sxs-lookup"><span data-stu-id="6dcf4-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="6dcf4-136">Tester l’application localement</span><span class="sxs-lookup"><span data-stu-id="6dcf4-136">Test application locally</span></span>

<span data-ttu-id="6dcf4-137">Accédez à http://localhost:8080 pour afficher le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-137">Browse to http://localhost:8080 to see the running application.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="6dcf4-139">Supprimer des ressources</span><span class="sxs-lookup"><span data-stu-id="6dcf4-139">Clean up resources</span></span>

<span data-ttu-id="6dcf4-140">Maintenant que la fonctionnalité de l’application a été validée, les conteneurs en cours d’exécution peuvent être arrêtés et supprimés.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-140">Now that application functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="6dcf4-141">Ne supprimez pas les images de conteneur.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-141">Do not delete the container images.</span></span> <span data-ttu-id="6dcf4-142">Dans le didacticiel suivant, l’image *azure-vote-front* est chargée dans une instance Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-142">The *azure-vote-front* image is uploaded to an Azure Container Registry instance in the next tutorial.</span></span>

<span data-ttu-id="6dcf4-143">Exécutez le code suivant pour arrêter les conteneurs en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-143">Run the following to stop the running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="6dcf4-144">Supprimez les conteneurs arrêtés avec la commande suivante.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-144">Delete the stopped containers with the following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="6dcf4-145">Une fois terminé, vous disposez de deux images conteneur contenant l’application Azure Vote.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-145">At completion, you have a container image that contains the Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6dcf4-146">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6dcf4-146">Next steps</span></span>

<span data-ttu-id="6dcf4-147">Dans ce didacticiel, une application a été testée et les images de conteneur créées pour l’application.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-147">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="6dcf4-148">Les étapes suivantes ont été effectuées :</span><span class="sxs-lookup"><span data-stu-id="6dcf4-148">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6dcf4-149">Le clonage de la source de l’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="6dcf4-149">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="6dcf4-150">La création d’une image conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="6dcf4-150">Created a container image from application source</span></span>
> * <span data-ttu-id="6dcf4-151">Le test de l’application dans un environnement Docker local</span><span class="sxs-lookup"><span data-stu-id="6dcf4-151">Tested the application in a local Docker environment</span></span>

<span data-ttu-id="6dcf4-152">Passez au didacticiel suivant pour en savoir plus sur le stockage d’images de conteneur dans Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6dcf4-152">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6dcf4-153">Envoyer des images à Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6dcf4-153">Push images to Azure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)