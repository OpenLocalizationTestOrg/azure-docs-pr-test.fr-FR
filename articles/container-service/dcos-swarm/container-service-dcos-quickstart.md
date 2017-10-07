---
title: "aaaAzure démarrage rapide du conteneur de Service - déployer un Cluster de contrôleur de domaine/système d’exploitation | Documents Microsoft"
description: "Démarrage rapide avec Azure Container Service - Déployer un cluster DC/OS"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Déployer un cluster DC/OS

DC/OS propose une plateforme distribuée destinée à exécuter des applications en conteneur modernes. Avec Azure Container Service, l’approvisionnement d’un cluster DC/OS prêt pour la production est une opération simple et rapide. Cette détails de démarrage rapide hello des étapes de base nécessaires toodeploy un cluster de contrôleur de domaine/système d’exploitation et de la charge de travail de base exécution.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure 

Connectez-vous à tooyour abonnement Azure avec hello [ouverture de session az](/cli/azure/#login) commande et suivez hello à l’écran.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un conteneur logique dans lequel les ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Créer un cluster DC/OS

Créez un cluster de contrôleur de domaine/système d’exploitation avec hello [az acs créer](/cli/azure/acs#create) commande.

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

tunnel SSH de Hello peut être testée en parcourant trop`http://localhost`. Si un port autre que 80 a été utilisé, ajuster hello emplacement toomatch. 

Tunnel SSH de hello a été créé avec succès, portail de contrôleur de domaine/système d’exploitation hello est retournée.

![Interface utilisateur DC/OS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Installer l’interface de ligne de commande DC/OS

interface de ligne de commande de contrôleur de domaine/système d’exploitation Hello est toomanage utilisé un cluster de contrôleur de domaine/système d’exploitation à partir de hello de ligne de commande. Installez hello cli de contrôleur de domaine/système d’exploitation à l’aide de hello [az acs dcos install-cli](/azure/acs/dcos#install-cli) commande. Si vous utilisez Azure CloudShell, hello CLI de contrôleur de domaine/système d’exploitation est déjà installé. 

Si vous exécutez hello CLI d’Azure sur macOS ou Linux, vous devrez peut-être commande hello toorun sudo.

```azurecli
az acs dcos install-cli
```

Avant de hello que CLI peut être utilisé avec un cluster de hello, il doit être tunnel SSH de hello toouse configuré. toodo exécuter donc hello commande suivante, en ajustant le port de hello si nécessaire.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Exécuter une application

mécanisme pour un cluster ACS contrôleur de domaine/système d’exploitation de planification de la valeur par défaut Hello est Marathon. Marathon est toostart utilisé une application et gérer l’état de l’application hello sur le cluster de contrôleur de domaine/système d’exploitation hello hello. tooschedule une application via Marathon, créez un fichier nommé *marathon-app.json*, et en hello de copie suivant contenu dans celui-ci. 

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
dcos marathon app add marathon-app.json
```

état du déploiement toosee hello pour l’application hello, exécutez hello commande suivante.

```azurecli
dcos marathon app list
```

Hello lorsque **attente** bascule de valeur de la colonne à partir de *True* trop*False*, déploiement d’application est terminée.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Obtenir l’adresse IP publique de hello d’agents de cluster de contrôleur de domaine/système d’exploitation hello.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Navigation toothis adresse retourne site NGINX hello par défaut.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Supprimer un cluster DC/OS

Lorsque vous n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, cluster de contrôleur de domaine/système d’exploitation et toutes les ressources de la commande.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez déployé un cluster de contrôleur de domaine/système d’exploitation et exécutez un simple conteneur Docker sur le cluster de hello. toolearn en savoir plus sur le Service de conteneur Azure, continuer toohello ACS didacticiels.

> [!div class="nextstepaction"]
> [Gérer un cluster ACS DC/OS](container-service-dcos-manage-tutorial.md)