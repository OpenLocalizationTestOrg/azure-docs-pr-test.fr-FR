---
title: aaaManage Azure Swarm cluster avec les API Docker | Documents Microsoft
description: "Déployer les conteneurs tooa Docker Swarm cluster dans le conteneur de Service Azure"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="56f00-104">Gestion des conteneurs avec Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="56f00-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="56f00-105">Docker Swarm fournit un environnement pour le déploiement de charges de travail en conteneur sur un ensemble groupé d’hôtes Docker.</span><span class="sxs-lookup"><span data-stu-id="56f00-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="56f00-106">Docker essaim utilise les API Docker native hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="56f00-107">workflow de Hello pour la gestion des conteneurs sur un Docker Swarm est presque identique toowhat qu'il serait sur un hôte de conteneur unique.</span><span class="sxs-lookup"><span data-stu-id="56f00-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="56f00-108">Ce document fournit des exemples simples de déploiement de charges de travail en conteneur dans une instance Azure Container Service de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="56f00-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="56f00-109">Pour des informations détaillées sur Docker Swarm, consultez [Docker Swarm sur Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="56f00-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="56f00-110">Exercices de toohello de conditions préalables dans ce document :</span><span class="sxs-lookup"><span data-stu-id="56f00-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="56f00-111">Création d’un cluster Swarm dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="56f00-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="56f00-112">Se connecter à un cluster d’essaim hello dans le conteneur de Service Azure</span><span class="sxs-lookup"><span data-stu-id="56f00-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="56f00-113">Déploiement d’un nouveau conteneur</span><span class="sxs-lookup"><span data-stu-id="56f00-113">Deploy a new container</span></span>
<span data-ttu-id="56f00-114">toocreate un nouveau conteneur Bonjour Docker Swarm, utilisez hello `docker run` commandes (vous être assuré que vous avez ouvert un maîtres de toohello tunnel SSH conformément aux conditions hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="56f00-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="56f00-115">Cet exemple crée un conteneur de hello `yeasy/simple-web` image :</span><span class="sxs-lookup"><span data-stu-id="56f00-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="56f00-116">Une fois le conteneur de hello a été créé, utilisez `docker ps` tooreturn plus d’informations sur le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="56f00-117">Notez ici que l’agent essaim hello qui héberge le conteneur de hello est répertorié :</span><span class="sxs-lookup"><span data-stu-id="56f00-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="56f00-118">Vous pouvez désormais accéder aux applications hello qui s’exécute dans ce conteneur via le nom DNS public de hello d’équilibrage de charge de l’agent essaim hello.</span><span class="sxs-lookup"><span data-stu-id="56f00-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="56f00-119">Vous pouvez trouver ces informations dans hello portail Azure :</span><span class="sxs-lookup"><span data-stu-id="56f00-119">You can find this information in hello Azure portal:</span></span>  

![Résultats réels des visites](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="56f00-121">Par défaut hello équilibrage de charge a les ports 80, 8080 et 443 ouvert.</span><span class="sxs-lookup"><span data-stu-id="56f00-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="56f00-122">Si vous souhaitez tooconnect sur un autre port vous devez tooopen ce port sur hello équilibrage de charge Azure pour hello Pool d’agents.</span><span class="sxs-lookup"><span data-stu-id="56f00-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="56f00-123">Déploiement de plusieurs conteneurs</span><span class="sxs-lookup"><span data-stu-id="56f00-123">Deploy multiple containers</span></span>
<span data-ttu-id="56f00-124">Plusieurs conteneurs sont lancées, en exécutant « docker run » plusieurs fois, vous pouvez utiliser hello `docker ps` toosee de commande qui héberge les conteneurs hello sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="56f00-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="56f00-125">Dans l’exemple hello ci-dessous, les trois conteneurs sont répartis uniformément sur trois agents d’essaim hello :</span><span class="sxs-lookup"><span data-stu-id="56f00-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="56f00-126">Déploiement de conteneurs avec Docker Compose</span><span class="sxs-lookup"><span data-stu-id="56f00-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="56f00-127">Vous pouvez utiliser le déploiement de hello tooautomate de Docker Compose et la configuration de plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="56f00-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="56f00-128">toodo, assurez-vous qu’un tunnel SSH (Secure Shell) a été créé et que cette variable DOCKER_HOST hello a été définie (voir hello préalables ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="56f00-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="56f00-129">Créez un fichier docker-compose.yml sur votre système local.</span><span class="sxs-lookup"><span data-stu-id="56f00-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="56f00-130">toodo, utilisez cette [exemple](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="56f00-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="56f00-131">Exécutez `docker-compose up -d` déploiements de conteneur toostart hello :</span><span class="sxs-lookup"><span data-stu-id="56f00-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="56f00-132">Enfin, liste hello de conteneurs en cours d’exécution s’affichera.</span><span class="sxs-lookup"><span data-stu-id="56f00-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="56f00-133">Cette liste répertorie les conteneurs hello qui ont été déployées à l’aide de Docker Compose :</span><span class="sxs-lookup"><span data-stu-id="56f00-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="56f00-134">Naturellement, vous pouvez utiliser `docker-compose ps` tooexamine hello uniquement les conteneurs définis dans votre `compose.yml` fichier.</span><span class="sxs-lookup"><span data-stu-id="56f00-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56f00-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="56f00-135">Next steps</span></span>
[<span data-ttu-id="56f00-136">Approfondissez vos connaissances sur Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="56f00-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

