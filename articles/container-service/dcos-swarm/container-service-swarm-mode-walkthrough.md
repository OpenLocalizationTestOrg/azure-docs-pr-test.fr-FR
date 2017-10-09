---
title: aaaQuickstart - cluster Azure Docker CE pour Linux | Documents Microsoft
description: "En savoir plus rapidement les toocreate un cluster Docker CE pour les conteneurs Linux dans le conteneur de Service Azure avec hello CLI d’Azure."
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
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Déployer le cluster Docker CE

Dans ce guide de démarrage rapide, un cluster de Docker CE est déployé à l’aide de hello CLI d’Azure. Une application conteneur multi composé d’un serveur web frontal et une instance de Redis est puis déployée et exécutée sur le cluster de hello. Une fois terminé, l’application hello est accessible sur internet de hello.

Docker CE est en version préliminaire sur Azure Container Service et **ne doit pas être utilisé pour des charges de travail de production**.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées.

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *ukwest* emplacement.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
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

Créer un cluster de Docker CE dans le conteneur de Service Azure avec hello [az acs créer](/cli/azure/acs#create) commande. 

Hello exemple suivant crée un cluster nommé *mySwarmCluster* avec un Linux maître nœud et trois nœuds de l’agent Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Après quelques minutes, commande hello se termine et retourne des informations au format json sur le cluster de hello.

## <a name="connect-toohello-cluster"></a>Se connecter toohello cluster

Tout au long de ce guide de démarrage rapide, vous devez hello FQDN du maître de Docker Swarm hello et pool d’agents hello Docker. Exécutez hello tooreturn deux hello principale et l’agent de noms de domaine complets de commande suivante.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Output:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Créer un SSH maître de tunnel toohello essaim. Remplacez `MasterFQDN` avec l’adresse du nom de domaine complet hello du maître d’essaim hello.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Ensemble hello `DOCKER_HOST` variable d’environnement. Ainsi, vous toorun les commandes docker sur hello Docker Swarm sans avoir le nom de hello toospecify d’hôte de hello.

```bash
export DOCKER_HOST=localhost:2374
```

Vous êtes maintenant prêt toorun des services de Docker sur hello Docker Swarm.


## <a name="run-hello-application"></a>Exécutez l’application hello

Créez un fichier nommé `azure-vote.yaml` et hello de copie suivant contenu dans celui-ci.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Exécutez hello [déployer de la pile de docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) commande du service de Azure Vote toocreate hello.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Output:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Hello d’utilisation [docker pile ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) commande l’état du déploiement hello tooreturn de l’application hello.

```bash
docker stack ps azure-vote
```

Une fois hello `CURRENT STATE` de chaque service est `Running`, application hello est prête.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Tester l’application hello

Parcourir toohello nom de domaine complet de hello essaim agent pool tootest out hello application de Vote de Azure.

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