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
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="4db14-103">Créer un conteneur pour un déploiement tooAzure Instances de conteneurs</span><span class="sxs-lookup"><span data-stu-id="4db14-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="4db14-104">Azure Container Instances permet de déployer des conteneurs Docker sur l’infrastructure Azure sans configurer de machines virtuelles ni adopter de service de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="4db14-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="4db14-105">Dans ce didacticiel, vous allez voir comment générer une application web basique dans Node.js, et comment la placer comme package dans un conteneur pouvant être exécuté avec Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="4db14-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="4db14-106">Nous aborderons :</span><span class="sxs-lookup"><span data-stu-id="4db14-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4db14-107">Le clonage de la source de l’application à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4db14-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="4db14-108">la création des images de conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="4db14-108">Creating container images from application source</span></span>
> * <span data-ttu-id="4db14-109">Test des images de hello dans un environnement de Docker local</span><span class="sxs-lookup"><span data-stu-id="4db14-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="4db14-110">Dans les didacticiels suivants vous téléchargez votre tooan image Registre de conteneur Azure et ensuite déployer les Instances de conteneurs tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4db14-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="4db14-111">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="4db14-111">Before you begin</span></span>

<span data-ttu-id="4db14-112">Ce didacticiel suppose une compréhension élémentaire des concepts Docker principaux tels que les conteneurs, les images de conteneur et les commandes Docker de base.</span><span class="sxs-lookup"><span data-stu-id="4db14-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="4db14-113">Si besoin, consultez [Bien démarrer avec Docker]( https://docs.docker.com/get-started/) pour apprendre les principes de base des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="4db14-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="4db14-114">toocomplete ce didacticiel, vous avez besoin d’un environnement de développement de Docker.</span><span class="sxs-lookup"><span data-stu-id="4db14-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="4db14-115">Docker fournit des packages qui le configurent facilement sur n’importe quel système [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) ou [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="4db14-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="4db14-116">Obtenir le code d’application</span><span class="sxs-lookup"><span data-stu-id="4db14-116">Get application code</span></span>

<span data-ttu-id="4db14-117">exemple Hello dans ce didacticiel inclut une application web simple générée dans [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="4db14-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="4db14-118">application Hello sert d’une page HTML statique et ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="4db14-118">hello app serves a static HTML page and looks like this:</span></span>

![Application du didacticiel affichée dans le navigateur][aci-tutorial-app]

<span data-ttu-id="4db14-120">Utiliser git toodownload hello, exemple :</span><span class="sxs-lookup"><span data-stu-id="4db14-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="4db14-121">Générer l’image de conteneur hello</span><span class="sxs-lookup"><span data-stu-id="4db14-121">Build hello container image</span></span>

<span data-ttu-id="4db14-122">Hello Dockerfile fourni dans le référentiel d’exemple hello montre la façon dont le conteneur de hello est construit.</span><span class="sxs-lookup"><span data-stu-id="4db14-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="4db14-123">Il démarre à partir d’un [officiel Node.js image] [ dockerhub-nodeimage] selon [Linux Alpine](https://alpinelinux.org/), une distribution petite qui est parfaitement toouse avec des conteneurs.</span><span class="sxs-lookup"><span data-stu-id="4db14-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="4db14-124">Ensuite, il copie les fichiers de l’application hello dans le conteneur de hello, installe les dépendances à l’aide de hello Node Package Manager et enfin démarre application hello.</span><span class="sxs-lookup"><span data-stu-id="4db14-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="4db14-125">Hello d’utilisation `docker build` image de conteneur de commande toocreate hello, en tant que balisage *aci-didacticiel-app*:</span><span class="sxs-lookup"><span data-stu-id="4db14-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="4db14-126">Hello d’utilisation `docker images` image hello généré de toosee :</span><span class="sxs-lookup"><span data-stu-id="4db14-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="4db14-127">Output:</span><span class="sxs-lookup"><span data-stu-id="4db14-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="4db14-128">Conteneur d’exécution hello localement</span><span class="sxs-lookup"><span data-stu-id="4db14-128">Run hello container locally</span></span>

<span data-ttu-id="4db14-129">Avant d’essayer de déploiement hello conteneur tooAzure les Instances du conteneur, l’exécuter localement tooconfirm qu’il fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4db14-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="4db14-130">Hello `-d` commutateur permet de conteneur de hello s’exécutent en arrière-plan de hello, tandis que `-p` vous permet de toomap un port arbitraire sur votre tooport calcul 80 dans le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="4db14-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="4db14-131">Ouvrez hello navigateur toohttp://localhost:8080 tooconfirm qui hello conteneur est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="4db14-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Application hello exécutée localement dans le navigateur de hello][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="4db14-133">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4db14-133">Next steps</span></span>

<span data-ttu-id="4db14-134">Dans ce didacticiel, vous avez créé une image de conteneur qui peut être des Instances de conteneurs tooAzure déployé.</span><span class="sxs-lookup"><span data-stu-id="4db14-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="4db14-135">Hello suit ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="4db14-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4db14-136">Source de l’application hello clonage à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="4db14-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="4db14-137">la création des images de conteneur à partir de la source de l’application</span><span class="sxs-lookup"><span data-stu-id="4db14-137">Creating container images from application source</span></span>
> * <span data-ttu-id="4db14-138">Test conteneur hello localement</span><span class="sxs-lookup"><span data-stu-id="4db14-138">Testing hello container locally</span></span>

<span data-ttu-id="4db14-139">Avance toohello toolearn de didacticiel suivant sur le stockage des images de conteneur dans un Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="4db14-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4db14-140">Push images tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="4db14-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png