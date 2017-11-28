---
title: "Didacticiel Azure Container Instances - Préparer votre application | Azure Docs"
description: "Préparer une application pour le déploiement vers Azure Container Instances"
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
ms.openlocfilehash: 167297e10eed11833623ff797e676ad43c65f9ad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-container-for-deployment-to-azure-container-instances"></a><span data-ttu-id="fea29-103">Créer un conteneur à déployer dans Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="fea29-103">Create container for deployment to Azure Container Instances</span></span>

<span data-ttu-id="fea29-104">Azure Container Instances permet de déployer des conteneurs Docker sur l’infrastructure Azure sans configurer de machines virtuelles ni adopter de service de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="fea29-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="fea29-105">Dans ce didacticiel, vous allez voir comment générer une application web basique dans Node.js, et comment la placer comme package dans un conteneur pouvant être exécuté avec Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="fea29-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="fea29-106">Nous aborderons :</span><span class="sxs-lookup"><span data-stu-id="fea29-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fea29-107">Le clonage de la source de l’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="fea29-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="fea29-108">la création des images de conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="fea29-108">Creating container images from application source</span></span>
> * <span data-ttu-id="fea29-109">Le test des images dans un environnement Docker local</span><span class="sxs-lookup"><span data-stu-id="fea29-109">Testing the images in a local Docker environment</span></span>

<span data-ttu-id="fea29-110">Dans les didacticiels suivants, vous aller voir comment charger votre image dans un registre Azure Container Registry, et comment la déployer dans Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="fea29-110">In subsequent tutorials, you will upload your image to an Azure Container Registry, and then deploy them to Azure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fea29-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="fea29-111">Before you begin</span></span>

<span data-ttu-id="fea29-112">Ce didacticiel suppose une compréhension élémentaire des concepts Docker principaux tels que les conteneurs, les images de conteneur et les commandes Docker de base.</span><span class="sxs-lookup"><span data-stu-id="fea29-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="fea29-113">Si besoin, consultez [Bien démarrer avec Docker]( https://docs.docker.com/get-started/) pour apprendre les principes de base des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="fea29-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="fea29-114">Pour terminer ce didacticiel, il vous faut un environnement de développement Docker.</span><span class="sxs-lookup"><span data-stu-id="fea29-114">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="fea29-115">Docker fournit des packages qui le configurent facilement sur n’importe quel système [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="fea29-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="fea29-116">Obtenir le code de l’application</span><span class="sxs-lookup"><span data-stu-id="fea29-116">Get application code</span></span>

<span data-ttu-id="fea29-117">L’exemple dans ce didacticiel inclut une application web basique générée dans [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="fea29-117">The sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="fea29-118">L’application se présente sous forme de page HTML statique et ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="fea29-118">The app serves a static HTML page and looks like this:</span></span>

![Application du didacticiel affichée dans le navigateur][aci-tutorial-app]

<span data-ttu-id="fea29-120">Utilisez Git pour télécharger l’exemple :</span><span class="sxs-lookup"><span data-stu-id="fea29-120">Use git to download the sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-the-container-image"></a><span data-ttu-id="fea29-121">Générer l’image de conteneur</span><span class="sxs-lookup"><span data-stu-id="fea29-121">Build the container image</span></span>

<span data-ttu-id="fea29-122">Le fichier Dockerfile fourni dans le référentiel de l’exemple montre comment le conteneur est généré.</span><span class="sxs-lookup"><span data-stu-id="fea29-122">The Dockerfile provided in the sample repo shows how the container is built.</span></span> <span data-ttu-id="fea29-123">La génération du conteneur commence par une [image officielle Node.js][dockerhub-nodeimage] sur [Linux Alpine](https://alpinelinux.org/), une petite distribution parfaitement adaptée aux conteneurs.</span><span class="sxs-lookup"><span data-stu-id="fea29-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited to use with containers.</span></span> <span data-ttu-id="fea29-124">Les fichiers d’application sont ensuite copiés dans le conteneur, les dépendances sont installées à l’aide de Node Package Manager, et l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="fea29-124">It then copies the application files into the container, installs dependencies using the Node Package Manager, and finally starts the application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="fea29-125">Utilisez la commande `docker build` pour créer l’image de conteneur, et balisez-la *aci-tutorial-app* :</span><span class="sxs-lookup"><span data-stu-id="fea29-125">Use the `docker build` command to create the container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="fea29-126">Utilisez `docker images` pour voir l’image ainsi générée :</span><span class="sxs-lookup"><span data-stu-id="fea29-126">Use the `docker images` to see the built image:</span></span>

```bash
docker images
```

<span data-ttu-id="fea29-127">Output:</span><span class="sxs-lookup"><span data-stu-id="fea29-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-the-container-locally"></a><span data-ttu-id="fea29-128">Exécutez localement le conteneur</span><span class="sxs-lookup"><span data-stu-id="fea29-128">Run the container locally</span></span>

<span data-ttu-id="fea29-129">Avant d’essayer de déployer le conteneur dans Azure Container Instances, exécutez-le localement pour vous assurer qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="fea29-129">Before you try deploying the container to Azure Container Instances, run it locally to confirm that it works.</span></span> <span data-ttu-id="fea29-130">Le commutateur `-d` permet l’exécution du conteneur en arrière-plan, tandis que `-p` vous permet de mapper un port arbitraire sur votre ordinateur vers le port 80 du conteneur.</span><span class="sxs-lookup"><span data-stu-id="fea29-130">The `-d` switch lets the container run in the background, while `-p` allows you to map an arbitrary port on your compute to port 80 in the container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="fea29-131">Allez à l’adresse http://localhost:8080 dans votre navigateur pour confirmer l’exécution du conteneur.</span><span class="sxs-lookup"><span data-stu-id="fea29-131">Open the browser to http://localhost:8080 to confirm that the container is running.</span></span>

![Exécution locale de l’application dans le navigateur][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="fea29-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fea29-133">Next steps</span></span>

<span data-ttu-id="fea29-134">Dans ce didacticiel, vous avez créé une image de conteneur qui peut être déployée dans Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="fea29-134">In this tutorial, you created a container image that can be deployed to Azure Container Instances.</span></span> <span data-ttu-id="fea29-135">Les étapes suivantes ont été effectuées :</span><span class="sxs-lookup"><span data-stu-id="fea29-135">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="fea29-136">le clonage de la source de l’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="fea29-136">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="fea29-137">La création des images de conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="fea29-137">Creating container images from application source</span></span>
> * <span data-ttu-id="fea29-138">Le test de l’exécution locale du conteneur</span><span class="sxs-lookup"><span data-stu-id="fea29-138">Testing the container locally</span></span>

<span data-ttu-id="fea29-139">Passez au didacticiel suivant pour en savoir plus sur le stockage d’images de conteneur dans un registre Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="fea29-139">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fea29-140">Envoyer des images à Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="fea29-140">Push images to Azure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png