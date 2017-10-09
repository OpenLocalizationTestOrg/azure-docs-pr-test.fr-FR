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
# <a name="container-management-with-docker-swarm"></a>Gestion des conteneurs avec Docker Swarm
Docker Swarm fournit un environnement pour le déploiement de charges de travail en conteneur sur un ensemble groupé d’hôtes Docker. Docker essaim utilise les API Docker native hello. workflow de Hello pour la gestion des conteneurs sur un Docker Swarm est presque identique toowhat qu'il serait sur un hôte de conteneur unique. Ce document fournit des exemples simples de déploiement de charges de travail en conteneur dans une instance Azure Container Service de Docker Swarm. Pour des informations détaillées sur Docker Swarm, consultez [Docker Swarm sur Docker.com](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Exercices de toohello de conditions préalables dans ce document :

[Création d’un cluster Swarm dans Azure Container Service](container-service-deployment.md)

[Se connecter à un cluster d’essaim hello dans le conteneur de Service Azure](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Déploiement d’un nouveau conteneur
toocreate un nouveau conteneur Bonjour Docker Swarm, utilisez hello `docker run` commandes (vous être assuré que vous avez ouvert un maîtres de toohello tunnel SSH conformément aux conditions hello ci-dessus). Cet exemple crée un conteneur de hello `yeasy/simple-web` image :

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Une fois le conteneur de hello a été créé, utilisez `docker ps` tooreturn plus d’informations sur le conteneur de hello. Notez ici que l’agent essaim hello qui héberge le conteneur de hello est répertorié :

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

Vous pouvez désormais accéder aux applications hello qui s’exécute dans ce conteneur via le nom DNS public de hello d’équilibrage de charge de l’agent essaim hello. Vous pouvez trouver ces informations dans hello portail Azure :  

![Résultats réels des visites](./media/container-service-docker-swarm/real-visit.jpg)  

Par défaut hello équilibrage de charge a les ports 80, 8080 et 443 ouvert. Si vous souhaitez tooconnect sur un autre port vous devez tooopen ce port sur hello équilibrage de charge Azure pour hello Pool d’agents.

## <a name="deploy-multiple-containers"></a>Déploiement de plusieurs conteneurs
Plusieurs conteneurs sont lancées, en exécutant « docker run » plusieurs fois, vous pouvez utiliser hello `docker ps` toosee de commande qui héberge les conteneurs hello sont en cours d’exécution. Dans l’exemple hello ci-dessous, les trois conteneurs sont répartis uniformément sur trois agents d’essaim hello :  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Déploiement de conteneurs avec Docker Compose
Vous pouvez utiliser le déploiement de hello tooautomate de Docker Compose et la configuration de plusieurs conteneurs. toodo, assurez-vous qu’un tunnel SSH (Secure Shell) a été créé et que cette variable DOCKER_HOST hello a été définie (voir hello préalables ci-dessus).

Créez un fichier docker-compose.yml sur votre système local. toodo, utilisez cette [exemple](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

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

Exécutez `docker-compose up -d` déploiements de conteneur toostart hello :

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

Enfin, liste hello de conteneurs en cours d’exécution s’affichera. Cette liste répertorie les conteneurs hello qui ont été déployées à l’aide de Docker Compose :

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Naturellement, vous pouvez utiliser `docker-compose ps` tooexamine hello uniquement les conteneurs définis dans votre `compose.yml` fichier.

## <a name="next-steps"></a>Étapes suivantes
[Approfondissez vos connaissances sur Docker Swarm](https://docs.docker.com/swarm/)

