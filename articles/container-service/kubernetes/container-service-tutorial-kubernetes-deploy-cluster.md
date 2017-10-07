---
title: "didacticiel de Service de conteneur aaaAzure - déployer un Cluster | Documents Microsoft"
description: "Didacticiel Azure Container Service - Déployer un cluster"
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
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Déployer un cluster Kubernetes dans Azure Container Service

Kubernetes fournit une plateforme distribuée destinée aux applications en conteneur. Avec Azure Container Service, l’approvisionnement d’un cluster Kubernetes prêt pour la production est une opération simple et rapide. Dans ce didacticiel (le troisième d’une série de sept), un cluster Azure Container Service Kubernetes est déployé. Les étapes terminées sont les suivantes :

> [!div class="checklist"]
> * Déploiement d’un cluster ACS Kubernetes
> * Installation de hello Kubernetes CLI (kubectl)
> * Configuration de kubectl

Dans les didacticiels suivants hello Vote Azure application est déployée toohello cluster, à l’échelle, de mettre à jour et Operations Management Suite est le cluster de Kubernetes hello toomonitor configuré.

## <a name="before-you-begin"></a>Avant de commencer

Dans les didacticiels précédents, une image de conteneur a été créée et téléchargé l’instance du Registre de conteneur Azure tooan. Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Créer un cluster Kubernetes

Bonjour [didacticiel précédent](./container-service-tutorial-kubernetes-prepare-acr.md), un groupe de ressources nommé *myResourceGroup* a été créé. Si vous ne l’avez pas déjà fait, créez ce groupe de ressources maintenant.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Créer un cluster Kubernetes dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande. 

Hello exemple suivant crée un cluster nommé *myK8sCluster* avec un Linux maître nœud et trois nœuds de l’agent Linux.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Après quelques minutes, commande hello se termine et retourne json mis en forme les informations sur le déploiement de hello ACS.

## <a name="install-hello-kubectl-cli"></a>Installer hello kubectl CLI

tooconnect toohello Kubernetes de cluster à partir de votre ordinateur client, utilisez [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), client de ligne de commande Kubernetes hello. 

Si vous utilisez Azure CloudShell, l’outil `kubectl` est déjà installé. Si vous souhaitez tooinstall il utiliser localement, hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) commande.

Si vous en Linux ou macOS, vous devrez peut-être toorun avec sudo. Dans Windows, vérifiez que votre interpréteur de commandes a été exécuté en tant qu’administrateur.

```azurecli-interactive 
az acs kubernetes install-cli 
```

Sous Windows, installation par défaut de hello est *c:\program files (x86)\kubectl.exe*. Vous devrez peut-être tooadd ce chemin d’accès de fichier toohello Windows. 

## <a name="connect-with-kubectl"></a>Se connecter avec kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster exécuter hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

cluster de tooyour connexion tooverify hello, exécutez hello [kubectl obtenir des nœuds](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.

```azurecli-interactive
kubectl get nodes
```

Output:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

À l’issue du didacticiel, vous disposez d’un cluster ACS Kubernetes prêt pour les charges de travail. Dans les didacticiels suivants, une application conteneur multi est déployé toothis cluster monté en charge, mises à jour et analysées.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, un cluster Azure Container Service Kubernetes a été déployé. Hello suit ont été effectuée :

> [!div class="checklist"]
> * Déploiement d’un cluster ACS Kubernetes
> * Hello installé Kubernetes CLI (kubectl)
> * Configuration de kubectl

Avance toohello toolearn de didacticiel suivant sur l’application en cours d’exécution sur le cluster de hello.

> [!div class="nextstepaction"]
> [Déployer une application dans Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
