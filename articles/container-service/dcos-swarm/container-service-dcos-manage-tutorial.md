---
title: "didacticiel de Service de conteneur aaaAzure - gérer les contrôleurs de domaine/système d’exploitation | Documents Microsoft"
description: "Didacticiel Azure Container Service - Gérer DC/OS"
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
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Didacticiel Azure Container Service - Gérer DC/OS

DC/OS propose une plateforme distribuée destinée à exécuter des applications en conteneur modernes. Avec Azure Container Service, l’approvisionnement d’un cluster DC/OS prêt pour la production est une opération simple et rapide. Ce démarrage rapide Détails des étapes base nécessaires toodeploy un cluster de contrôleur de domaine/système d’exploitation et de la charge de travail de base exécution.

> [!div class="checklist"]
> * Créer un cluster ACS DC/OS
> * Se connecter toohello cluster
> * Installer hello CLI de contrôleur de domaine/système d’exploitation
> * Déployer un cluster de toohello d’application
> * L’échelle d’une application sur un cluster de hello
> * Mettre à l’échelle des nœuds de cluster de contrôleur de domaine/système d’exploitation hello
> * Gestion DC/OS de base
> * Supprimer le cluster de contrôleur de domaine/système d’exploitation hello

Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>Créer un cluster DC/OS

Commencez par créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westeurope* emplacement.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Ensuite, créez un cluster de contrôleur de domaine/système d’exploitation avec hello [az acs créer](/cli/azure/acs#create) commande.

Hello exemple suivant crée un cluster de contrôleur de domaine/système d’exploitation nommé *myDCOSCluster* et crée des clés SSH s’ils n’existent pas déjà. toouse un ensemble spécifique de clés, utilisez hello `--ssh-key-value` option.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Après quelques minutes, commande hello se termine et retourne des informations sur le déploiement de hello.

## <a name="connect-toodcos-cluster"></a>Connectez le cluster de tooDC/OS

Dès lors qu’un cluster DC/OS est créé, il est accessible via un tunnel SSH. Exécutez hello suivant commande tooreturn hello adresse IP publique du principal du contrôleur de domaine/système d’exploitation hello. Cette adresse IP est stockée dans une variable et utilisée à l’étape suivante de hello.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate hello tunnel SSH, exécutez hello commande suivante et suivez hello les instructions à l’écran. Si le port 80 est déjà en cours d’utilisation, la commande hello échoue. Hello de mise à jour en tunnel tooone port pas en cours d’utilisation, telles que `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>Installer l’interface de ligne de commande DC/OS

Installez hello cli de contrôleur de domaine/système d’exploitation à l’aide de hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) commande. Si vous utilisez Azure CloudShell, hello CLI de contrôleur de domaine/système d’exploitation est déjà installé. Si vous exécutez hello CLI d’Azure sur macOS ou Linux, vous devrez peut-être commande hello toorun sudo.

```azurecli
az acs dcos install-cli
```

Avant de hello que CLI peut être utilisé avec un cluster de hello, il doit être tunnel SSH de hello toouse configuré. toodo exécuter donc hello commande suivante, en ajustant le port de hello si nécessaire.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Exécuter une application

mécanisme pour un cluster ACS contrôleur de domaine/système d’exploitation de planification de la valeur par défaut Hello est Marathon. Marathon est toostart utilisé une application et gérer l’état de l’application hello sur le cluster de contrôleur de domaine/système d’exploitation hello hello. tooschedule une application via Marathon, créez un fichier nommé **marathon-app.json**, et en hello de copie suivant contenu dans celui-ci. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Exécutez hello suivant de commande tooschedule hello application toorun de cluster de contrôleur de domaine/système d’exploitation hello.

```azurecli
dcos marathon app add marathon-app.json
```

état du déploiement toosee hello pour l’application hello, exécutez hello commande suivante.

```azurecli
dcos marathon app list
```

Hello lorsque **tâches** bascule de valeur de la colonne à partir de *0/1* trop*1/1*, déploiement d’application est terminée.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Mettre à l’échelle l’application Marathon

Dans l’exemple précédent de hello, une application à instance unique a été créée. tooupdate ce déploiement afin que les trois instances de l’application hello sont disponibles, ouvrez hello **marathon-app.json** de fichiers et mettre à jour too3 de propriété d’instance hello.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Mettre à jour d’application hello utilisant hello `dcos marathon app update` commande.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

état du déploiement toosee hello pour l’application hello, exécutez hello commande suivante.

```azurecli
dcos marathon app list
```

Hello lorsque **tâches** bascule de valeur de la colonne à partir de *1/3* trop*3/1*, déploiement d’application est terminée.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Exécuter l’application accessible par Internet

Hello ACS DC/OS cluster se compose de deux ensembles de nœuds, un public qui est accessible sur hello internet et l’autre privée qui n’est pas accessible sur hello internet. ensemble par défaut de Hello est nœuds privé de hello, qui a été utilisé dans le dernier exemple de hello.

toomake une application accessible sur hello internet, déployez-les toohello nœud publique ensemble. toodo, laissez-vous hello `acceptedResourceRoles` une valeur de l’objet `slave_public`.

Créez un fichier nommé **nginx-public.json** et hello de copie suivant contenu dans celui-ci.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Exécutez hello suivant de commande tooschedule hello application toorun de cluster de contrôleur de domaine/système d’exploitation hello.

```azurecli 
dcos marathon app add nginx-public.json
```

Obtenir l’adresse IP publique de hello d’agents de clusters public hello contrôleur de domaine/système d’exploitation.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Navigation toothis adresse retourne site NGINX hello par défaut.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Mettre à l’échelle un cluster DC/OS

Dans les exemples précédents hello, une application a été mis à l’échelle toomultiple instance. infrastructure de contrôleur de domaine/système d’exploitation Hello peut également être mis à l’échelle tooprovide plus ou moins de capacité de calcul. Cette opération s’effectue par hello [mettre à l’échelle des services acs az]() commande. 

Nombre actuel de hello toosee d’agents de contrôleur de domaine/système d’exploitation, utilisez hello [afficher d’acs az](/cli/azure/acs#show) commande.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease hello nombre too5, utilisez hello [mettre à l’échelle des services acs az](/cli/azure/acs#scale) commande. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>Supprimer un cluster DC/OS

Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, cluster de contrôleur de domaine/système d’exploitation et toutes les ressources de la commande.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à propos de la tâche de gestion de contrôleur de domaine/système d’exploitation de base notamment hello suivantes. 

> [!div class="checklist"]
> * Créer un cluster ACS DC/OS
> * Se connecter toohello cluster
> * Installer hello CLI de contrôleur de domaine/système d’exploitation
> * Déployer un cluster de toohello d’application
> * L’échelle d’une application sur un cluster de hello
> * Mettre à l’échelle des nœuds de cluster de contrôleur de domaine/système d’exploitation hello
> * Supprimer le cluster de contrôleur de domaine/système d’exploitation hello

Avance toohello suivant didacticiel toolearn sur Charger équilibrage d’application dans le contrôleur de domaine/système d’exploitation sur Azure. 

> [!div class="nextstepaction"]
> [Équilibrer la charge des applications](container-service-load-balancing.md)