---
title: aaaQuickstart - Swarm de Docker Azure de cluster pour Linux | Documents Microsoft
description: "En savoir plus rapidement les toocreate un cluster Docker Swarm pour les conteneurs Linux dans le conteneur de Service Azure avec hello CLI d’Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a>Déployer le cluster Docker Swarm

Dans ce guide de démarrage rapide, un cluster Docker Swarm est déployé à l’aide de hello CLI d’Azure. Une application conteneur multi composé d’un serveur web frontal et une instance de Redis est puis déployée et exécutée sur le cluster de hello. Une fois terminé, l’application hello est accessible sur internet de hello.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

Ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Output:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Créer le cluster Docker Swarm

Créer un cluster de Docker Swarm dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande. 

Hello exemple suivant crée un cluster nommé *mySwarmCluster* avec un Linux maître nœud et trois nœuds de l’agent Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

Après quelques minutes, commande hello se termine et retourne des informations au format json sur le cluster de hello.

## <a name="connect-toohello-cluster"></a>Se connecter toohello cluster

Tout au long de ce guide de démarrage rapide, vous avez besoin de l’adresse IP hello principale de Docker Swarm hello et pool d’agents hello Docker. La commande suivante d’exécution hello tooreturn les deux adresses IP.


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

Output:

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

Créer un SSH maître de tunnel toohello essaim. Remplacez `IPAddress` avec adresse IP principale d’essaim hello hello.

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

Ensemble hello `DOCKER_HOST` variable d’environnement. Ainsi, vous toorun les commandes docker sur hello Docker Swarm sans avoir le nom de hello toospecify d’hôte de hello.

```bash
export DOCKER_HOST=:2375
```

Vous êtes maintenant prêt toorun des services de Docker sur hello Docker Swarm.


## <a name="run-hello-application"></a>Exécutez l’application hello

Créez un fichier nommé `docker-compose.yaml` et hello de copie suivant contenu dans celui-ci.

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Exécutez hello après commande toocreate hello Azure Vote service.

```bash
docker-compose up -d
```

Output:

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a>Tester l’application hello

Parcourir l’adresse IP toohello hello essaim agent pool tootest d’application Azure Vote hello.

![Image de navigation tooAzure Vote](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Supprimer un cluster
Lorsque le cluster de hello n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, service de conteneur et toutes les ressources de la commande.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Obtenir le code de hello

Dans ce guide de démarrage rapide, les images de conteneur précréés ont été toocreate utilisé un service de Docker. Hello liés le code d’application, fichier Dockerfile, et le fichier de message sont disponibles sur GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous déployé un cluster Docker Swarm et déployé une application conteneur multiples de tooit.

toolearn sur l’intégration de Docker à chaud avec Visual Studio Team Services, continuer toohello CI/CD avec Docker Swarm et VSTS.

> [!div class="nextstepaction"]
> [CI/CD avec Docker Swarm et VSTS](./container-service-docker-swarm-setup-ci-cd.md)