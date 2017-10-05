---
title: "Gérer un cluster Swarm Azure avec l’API Docker | Microsoft Docs"
description: "Déployez des conteneurs sur un cluster Docker Swarm dans Azure Container Service"
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
ms.openlocfilehash: 6ca2d2e49c4b7f5eb0580e7091b09209f8b73a7c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="d5a2c-104">Gestion des conteneurs avec Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="d5a2c-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="d5a2c-105">Docker Swarm fournit un environnement pour le déploiement de charges de travail en conteneur sur un ensemble groupé d’hôtes Docker.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="d5a2c-106">Docker Swarm utilise l’API Docker native.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-106">Docker Swarm uses the native Docker API.</span></span> <span data-ttu-id="d5a2c-107">Le flux de travail pour la gestion des conteneurs sur un Docker Swarm est presque identique à ce qu’elle serait sur un hôte de conteneur individuel.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-107">The workflow for managing containers on a Docker Swarm is almost identical to what it would be on a single container host.</span></span> <span data-ttu-id="d5a2c-108">Ce document fournit des exemples simples de déploiement de charges de travail en conteneur dans une instance Azure Container Service de Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="d5a2c-109">Pour des informations détaillées sur Docker Swarm, consultez [Docker Swarm sur Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="d5a2c-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="d5a2c-110">Conditions préalables pour les exercices de ce document :</span><span class="sxs-lookup"><span data-stu-id="d5a2c-110">Prerequisites to the exercises in this document:</span></span>

[<span data-ttu-id="d5a2c-111">Création d’un cluster Swarm dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d5a2c-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="d5a2c-112">Connexion avec le cluster Swarm dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="d5a2c-112">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="d5a2c-113">Déploiement d’un nouveau conteneur</span><span class="sxs-lookup"><span data-stu-id="d5a2c-113">Deploy a new container</span></span>
<span data-ttu-id="d5a2c-114">Pour créer un conteneur dans l’outil Docker Swarm, utilisez la commande `docker run` (en vous assurant d’avoir ouvert un tunnel SSH vers les maîtres, conformément aux conditions préalables décrites ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="d5a2c-114">To create a new container in the Docker Swarm, use the `docker run` command (ensuring that you have opened an SSH tunnel to the masters as per the prerequisites above).</span></span> <span data-ttu-id="d5a2c-115">Cet exemple crée un conteneur à partir de l’image `yeasy/simple-web` :</span><span class="sxs-lookup"><span data-stu-id="d5a2c-115">This example creates a container from the `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="d5a2c-116">Une fois le conteneur créé, utilisez `docker ps` pour renvoyer des informations sur le conteneur.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-116">After the container has been created, use `docker ps` to return information about the container.</span></span> <span data-ttu-id="d5a2c-117">Ici, l’agent Swarm qui héberge le conteneur est répertorié :</span><span class="sxs-lookup"><span data-stu-id="d5a2c-117">Notice here that the Swarm agent that is hosting the container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="d5a2c-118">Vous pouvez maintenant accéder à l’application en cours d’exécution dans ce conteneur via le nom DNS public de l’équilibreur de charge de l’agent Swarm.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-118">You can now access the application that is running in this container through the public DNS name of the Swarm agent load balancer.</span></span> <span data-ttu-id="d5a2c-119">Ces informations sont disponibles dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-119">You can find this information in the Azure portal:</span></span>  

![Résultats réels des visites](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="d5a2c-121">Par défaut, l’équilibreur de charge dispose des ports 80, 8080 et 443 ouverts.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-121">By default the Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="d5a2c-122">Si vous souhaitez vous connecter sur un autre port, vous devez ouvrir ce port dans Azure Load Balancer pour le pool d’agents.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-122">If you want to connect on another port you will need to open that port on the Azure Load Balancer for the Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="d5a2c-123">Déploiement de plusieurs conteneurs</span><span class="sxs-lookup"><span data-stu-id="d5a2c-123">Deploy multiple containers</span></span>
<span data-ttu-id="d5a2c-124">Plusieurs conteneurs étant démarrés, en exécutant « docker run » plusieurs fois, vous pouvez utiliser la commande `docker ps` pour afficher les hôtes sur lesquels les conteneurs sont exécutés.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-124">As multiple containers are started, by executing 'docker run' multiple times, you can use the `docker ps` command to see which hosts the containers are running on.</span></span> <span data-ttu-id="d5a2c-125">Dans l’exemple ci-dessous, trois conteneurs sont répartis uniformément entre les trois agents Swarm :</span><span class="sxs-lookup"><span data-stu-id="d5a2c-125">In the example below, three containers are spread evenly across the three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="d5a2c-126">Déploiement de conteneurs avec Docker Compose</span><span class="sxs-lookup"><span data-stu-id="d5a2c-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="d5a2c-127">Vous pouvez utiliser Docker Compose pour automatiser le déploiement et la configuration de plusieurs conteneurs.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-127">You can use Docker Compose to automate the deployment and configuration of multiple containers.</span></span> <span data-ttu-id="d5a2c-128">Pour ce faire, assurez-vous qu’un tunnel Secure Shell (SSH) a été créé et que la variable DOCKER_HOST a été définie (voir les conditions préalables ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="d5a2c-128">To do so, ensure that a Secure Shell (SSH) tunnel has been created and that the DOCKER_HOST variable has been set (see the pre-requisites above).</span></span>

<span data-ttu-id="d5a2c-129">Créez un fichier docker-compose.yml sur votre système local.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="d5a2c-130">Pour ce faire, utilisez cet [exemple](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="d5a2c-130">To do this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

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

<span data-ttu-id="d5a2c-131">Exécutez `docker-compose up -d` pour démarrer les déploiements de conteneur :</span><span class="sxs-lookup"><span data-stu-id="d5a2c-131">Run `docker-compose up -d` to start the container deployments:</span></span>

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

<span data-ttu-id="d5a2c-132">Enfin, la liste des conteneurs en cours d’exécution est retournée.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-132">Finally, the list of running containers will be returned.</span></span> <span data-ttu-id="d5a2c-133">Cette liste répertorie les conteneurs qui ont été déployés à l’aide de Docker Compose :</span><span class="sxs-lookup"><span data-stu-id="d5a2c-133">This list reflects the containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="d5a2c-134">Naturellement, vous pouvez utiliser `docker-compose ps` pour examiner uniquement les conteneurs définis dans votre fichier `compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="d5a2c-134">Naturally, you can use `docker-compose ps` to examine only the containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5a2c-135">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d5a2c-135">Next steps</span></span>
[<span data-ttu-id="d5a2c-136">Approfondissez vos connaissances sur Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="d5a2c-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

