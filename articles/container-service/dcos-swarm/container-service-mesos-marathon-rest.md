---
title: "cluster de contrôleur de domaine/système d’exploitation Azure aaaManage avec l’API REST Marathon | Documents Microsoft"
description: "Déployer le cluster de conteneurs tooan conteneur Service contrôleur de domaine/système d’exploitation Azure à l’aide de hello Marathon REST API."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Mesos, Azure
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>Gestion des conteneurs de contrôleur de domaine/système d’exploitation via l’API REST de Marathon de hello
Contrôleur de domaine/système d’exploitation fournit un environnement de déploiement et de mise à l’échelle de charges de travail en cluster, tout en faisant abstraction du matériel sous-jacent de hello. DC/OS sous-tend un framework qui gère la planification et l’exécution des charges de travail de calcul. Bien que les infrastructures sont disponibles pour nombreuses charges de travail courantes, ce document s’obtient à commencer la création et la mise à l’échelle des déploiements de conteneur à l’aide de hello Marathon REST API. 

## <a name="prerequisites"></a>Composants requis

Avant d’étudier ces exemples, vous devez avoir un cluster DC/OS configuré dans Azure Container Service. Vous devez également le cluster de toothis toohave la connectivité à distance. Pour plus d’informations sur ces éléments, consultez hello suivant des articles :

* [Déploiement d’un cluster Azure Container Service](container-service-deployment.md)
* [Connexion de cluster du Service de conteneur Azure tooan](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Hello d’accès aux API de contrôleur de domaine/système d’exploitation
Une fois que vous êtes cluster du Service de conteneur Azure toohello connecté, vous pouvez accéder hello contrôleur de domaine/système d’exploitation et les API REST associées via le port de http://localhost:local. exemples de Hello dans ce document supposent que vous créez un tunnel sur le port 80. Par exemple, les points de terminaison hello Marathon peuvent être atteint à l’URI commençant par `http://localhost/marathon/v2/`. 

Pour plus d’informations sur hello diverses API, consultez la documentation mésosphère hello hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) et [Chronos API](https://mesos.github.io/chronos/docs/api.html)et la documentation d’Apache pour hello [API du Planificateur de Mesos ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Collecte d’informations à partir de DC/OS et de Marathon
Avant de déployer des clusters de contrôleur de domaine/système d’exploitation de conteneurs toohello, rassembler des informations sur le cluster de contrôleur de domaine/système d’exploitation hello, telles que les noms de hello et l’état des agents de contrôleur de domaine/système d’exploitation hello. toodo requête donc hello `master/slaves` point de terminaison de hello API REST de contrôleur de domaine/système d’exploitation. Si tout se passe bien, requête de hello retourne une liste des agents de contrôleur de domaine/système d’exploitation et de plusieurs propriétés pour chacun.

```bash
curl http://localhost/mesos/master/slaves
```

À présent, utiliser hello Marathon `/apps` toocheck de point de terminaison de cluster du contrôleur de domaine/système d’exploitation toohello de déploiements application actuel. S’il s’agit d’un nouveau cluster, un tableau vide s’affiche pour les applications.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Déployer un conteneur au format Docker
Vous déployez au format Docker de conteneurs via hello Marathon REST API à l’aide d’un fichier JSON qui décrit le déploiement de hello destiné. Hello exemple suivant déploie un agent Nginx conteneur tooa privé dans un cluster de hello. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy un conteneur au format Docker, stocker le fichier JSON de hello dans un emplacement accessible. Ensuite, toodeploy hello conteneur exécuter hello commande suivante. Spécifiez le nom hello du fichier JSON de hello (`marathon.json` dans cet exemple).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

sortie de Hello est similaire toohello suivantes :

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Maintenant, si vous interrogez Marathon pour les applications, cette nouvelle application s’affiche dans la sortie de hello.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Atteindre le conteneur de hello

Vous pouvez vérifier que hello que nginx est en cours d’exécution dans un conteneur sur l’un des agents de hello privé dans un cluster de hello. hôte de hello toofind et port où le conteneur de hello est en cours d’exécution, requête Marathon pourquoi les tâches en cours d’exécution : 

```bash
curl localhost/marathon/v2/tasks
```

Rechercher la valeur hello `host` dans la sortie de hello (une adresse IP similaire trop`10.32.0.x`) et la valeur hello de `ports`.


Maintenant vous une gestion toohello des connexions Terminal Server (et non pas une connexion tunnel) SSH nom de domaine complet du cluster de hello. Une fois connecté, rendre hello demande, en remplaçant les valeurs correctes de hello de `host` et `ports`:

```bash
curl http://host:ports
```

Hello Nginx résultat du serveur est semblable toohello suivantes :

![Nginx à partir d’un conteneur](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Mettre vos conteneurs à l’échelle
Vous pouvez utiliser tooscale de Marathon API hello out ou d’échelle dans les déploiements d’applications. Dans l’exemple précédent de hello, vous avez déployé une instance d’une application. Nous allons mettre à l’échelle cela toothree des instances d’une application. toodo par conséquent, créer un fichier JSON à l’aide de hello suivant le texte JSON et stockez-le dans un emplacement accessible.

```json
{ "instances": 3 }
```

À partir de votre connexion tunnel, exécutez hello suivant tooscale de commande d’application hello.

> [!NOTE]
> Hello URI est http://localhost/marathon/v2/apps/ suivi par ID hello de hello application tooscale. Si vous utilisez l’exemple hello Nginx fourni ici, hello URI serait http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Enfin, requête de point de terminaison de Marathon hello pour les applications. Vous constatez qu’il existe désormais trois conteneurs Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Commandes PowerShell équivalentes
Vous pouvez effectuer les mêmes opérations sur un système Windows à l’aide des commandes PowerShell.

toogather plus d’informations sur le cluster de contrôleur de domaine/système d’exploitation hello, tels que les noms d’agent et l’état de l’agent, exécutez hello de commande suivante :

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Vous déployez des mises en forme de Docker de conteneurs via Marathon à l’aide d’un fichier JSON qui décrit le déploiement de hello destinée. Hello exemple suivant déploie conteneur Nginx de hello, lier le port 80 de hello DC/OS agent tooport 80 du conteneur de hello.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy un conteneur au format Docker, stocker le fichier JSON de hello dans un emplacement accessible. Ensuite, toodeploy hello conteneur exécuter hello commande suivante. Spécifier le fichier JSON de hello chemin d’accès toohello (`marathon.json` dans cet exemple).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

Vous pouvez également utiliser tooscale de Marathon API hello out ou d’échelle dans les déploiements d’applications. Dans l’exemple précédent de hello, vous avez déployé une instance d’une application. Nous allons mettre à l’échelle cela toothree des instances d’une application. toodo par conséquent, créer un fichier JSON à l’aide de hello suivant le texte JSON et stockez-le dans un emplacement accessible.

```json
{ "instances": 3 }
```

Exécutez hello suivant tooscale de commande d’application hello :

> [!NOTE]
> Hello URI est http://localhost/marathon/v2/apps/ suivi par ID hello de hello application tooscale. Si vous utilisez hello Nginx exemple fourni ici, hello URI serait http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur les points de terminaison hello Mesos HTTP](http://mesos.apache.org/documentation/latest/endpoints/)
* [En savoir plus sur l’API REST de Marathon de hello](https://mesosphere.github.io/marathon/docs/rest-api.html)

