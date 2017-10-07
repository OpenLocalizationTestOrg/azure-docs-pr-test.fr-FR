---
title: "aaaDeploy un cluster de conteneur Docker - CLI d’Azure | Documents Microsoft"
description: "Déployer une solution Kubernetes, DC/OS ou Docker Swarm dans Azure Container Service à l’aide d’Azure CLI 2.0"
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: azurecli
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: saudas
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: cdfa4ce69de343dcc7070bc2c58b5132c4062084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-cli-20"></a>Déployer un conteneur Docker à l’aide de hello Azure CLI 2.0 de solution d’hébergement

Hello d’utilisation `az acs` hello Azure CLI 2.0 toocreate des commandes et de gérer des clusters dans le Service de conteneur Azure. Vous pouvez également déployer un cluster du Service de conteneur Azure à l’aide de hello [portail Azure](container-service-deployment.md) ou hello API de Service de conteneur Azure.

Pour une aide sur `az acs` commandes, passez hello `-h` commande tooany de paramètre. Par exemple : `az acs create -h`.



## <a name="prerequisites"></a>Composants requis
un cluster de Service de conteneur Azure à l’aide de toocreate hello Azure CLI 2.0, vous devez :
* disposer d’un compte Azure ([obtenir une version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/))
* avoir installé et configuré hello [Azure CLI 2.0](/cli/azure/install-az-cli2)

## <a name="get-started"></a>Prise en main 
### <a name="log-in-tooyour-account"></a>Connectez-vous au compte de tooyour
```azurecli
az login 
```

Suivez toolog des invites hello dans interactivement. Pour les autres toolog méthodes dans, consultez [prise en main Azure CLI 2.0](/cli/azure/get-started-with-az-cli2).

### <a name="set-your-azure-subscription"></a>Définir votre abonnement Azure

Si vous avez plusieurs abonnements Azure, définissez l’abonnement par défaut de hello. Par exemple :

```
az account set --subscription "f66xxxxx-xxxx-xxxx-xxx-zgxxxx33cha5"
```


### <a name="create-a-resource-group"></a>Créer un groupe de ressources
Nous vous recommandons de créer un groupe de ressources pour chaque cluster. Spécifiez une région Azure dans laquelle Azure Container Service est [disponible](https://azure.microsoft.com/en-us/regions/services/). Par exemple :

```azurecli
az group create -n acsrg1 -l "westus"
```
La sortie est similaire toohello suivantes :

![Créer un groupe de ressources](./media/container-service-create-acs-cluster-cli/rg-create.png)


## <a name="create-an-azure-container-service-cluster"></a>Créer un cluster Azure Container Service

toocreate un cluster, utilisez `az acs create`.
Un nom pour le cluster de hello et hello hello du groupe de ressources créé à l’étape précédente de hello sont les paramètres obligatoires. 

Autres entrées sont les valeurs toodefault (voir hello suivant écran), sauf si remplacé à l’aide de leurs commutateurs respectifs. Par exemple, les orchestrator hello a la valeur par défaut tooDC/système d’exploitation. Et si vous ne précisez aucun, un préfixe de nom DNS est créé en fonction du nom du cluster hello.

![création d’un cluster acs az](./media/container-service-create-acs-cluster-cli/create-help.png)


### <a name="quick-acs-create-using-defaults"></a>`acs create` rapide à l’aide des valeurs par défaut
Si vous avez un fichier de clé publique SSH RSA `id_rsa.pub` dans l’emplacement par défaut de hello (ou créé un pour [OS X et Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) ou [Windows](../../virtual-machines/linux/ssh-from-windows.md)), utilisez une commande semblable à hello suivante :

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789
```
Si vous n’avez pas de clé publique SSH, utilisez cette seconde commande. Cette commande avec hello `--generate-ssh-keys` commutateur crée une pour vous.

```azurecli
az acs create -n acs-cluster -g acsrg1 -d applink789 --generate-ssh-keys
```

Après avoir entré la commande hello, attendez environ 10 minutes pour hello cluster toobe est créé. sortie de la commande Hello inclut les noms de domaine complet (FQDN) de masque de hello et de des nœuds de l’agent et d’une commande SSH tooconnect toohello premier masque. Voici la sortie abrégée :

![Image création du cluster ACS](./media/container-service-create-acs-cluster-cli/cluster-create.png)

> [!TIP]
> Hello [Kubernetes procédure pas à pas](../kubernetes/container-service-kubernetes-walkthrough.md) montre comment toouse `az acs create` avec toocreate de valeurs par défaut un Kubernetes de cluster.
>

## <a name="manage-acs-clusters"></a>Gérer des clusters ACS

Utilisez supplémentaire `az acs` commandes toomanage votre cluster. Voici quelques exemples.

### <a name="list-clusters-under-a-subscription"></a>Répertorier les clusters dans un abonnement

```azurecli
az acs list --output table
```

### <a name="list-clusters-in-a-resource-group"></a>Répertorier les clusters au sein d’un groupe de ressources

```azurecli
az acs list -g acsrg1 --output table
```

![liste des clusters acs](./media/container-service-create-acs-cluster-cli/acs-list.png)


### <a name="display-details-of-a-container-service-cluster"></a>Afficher les détails d’un cluster Container Service

```azurecli
az acs show -g acsrg1 -n acs-cluster --output list
```

![affichage du cluster acs](./media/container-service-create-acs-cluster-cli/acs-show.png)


### <a name="scale-hello-cluster"></a>Cluster hello de mise à l’échelle
Vous pouvez effectuer une mise à l’échelle verticale ou horizontale des nœuds d’agent. Hello paramètre `new-agent-count` est hello nouveau nombre d’agents dans le cluster de hello ACS.

```azurecli
az acs scale -g acsrg1 -n acs-cluster --new-agent-count 4
```

![mise à l’échelle du cluster acs](./media/container-service-create-acs-cluster-cli/acs-scale.png)

## <a name="delete-a-container-service-cluster"></a>Supprimer un cluster Container Service
```azurecli
az acs delete -g acsrg1 -n acs-cluster 
```
Cette commande ne supprime pas toutes les ressources (réseau et stockage) sont créées lors de la création du service de conteneur hello. toodelete toutes les ressources facilement, il est recommandé de déployer chaque cluster dans un groupe de ressources distinct. Supprimez ensuite le groupe de ressources hello lorsque hello cluster n’est plus nécessaire.

## <a name="next-steps"></a>Étapes suivantes
À présent que vous disposez d’un cluster opérationnel, consultez les documents suivants pour obtenir des informations supplémentaires concernant la connexion et la gestion du cluster :

* [Connecter le cluster du Service de conteneur Azure tooan](../container-service-connect.md)
* [Gestion de conteneur via l’API REST](container-service-mesos-marathon-rest.md)
* [Gestion des conteneurs avec Docker Swarm](container-service-docker-swarm.md)
* [Gestion des conteneurs avec Kubernetes](../kubernetes/container-service-kubernetes-walkthrough.md)