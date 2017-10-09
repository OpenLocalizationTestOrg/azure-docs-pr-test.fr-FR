---
title: aaaQuickstart - cluster Kubernetes de Azure pour Windows | Documents Microsoft
description: "En savoir plus rapidement les toocreate un cluster Kubernetes pour les conteneurs Windows dans le Service de conteneur Azure avec hello CLI d’Azure."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Déployer un cluster Azure Kubernetes pour des conteneurs Windows

Hello CLI d’Azure est utilisé toocreate et gérer des ressources Azure à partir de la ligne de commande hello ou dans des scripts. Ce guide décrit en détail à l’aide de hello CLI d’Azure toodeploy un [Kubernetes](https://kubernetes.io/docs/home/) du cluster dans [Service de conteneur Azure](../container-service-intro.md). Une fois que le cluster de hello est déployé, vous rejoignez tooit hello Kubernetes `kubectl` outil de ligne de commande et que vous déployez votre premier conteneur Windows.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce démarrage rapide nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> Le support des conteneurs Windows sur Kubernetes dans Azure Container Service est en préversion. 
>

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Créer un groupe de ressources avec hello [création de groupe de az](/cli/azure/group#create) commande. Un groupe de ressources Azure est un groupe logique dans lequel des ressources Azure sont déployées et gérées. 

Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *eastus* emplacement.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Créer un cluster Kubernetes
Créer un cluster Kubernetes dans le Service de conteneur Azure avec hello [az acs créer](/cli/azure/acs#create) commande. 

Hello exemple suivant crée un cluster nommé *myK8sCluster* avec un Linux maître nœud et deux nœuds de l’agent de Windows. Cet exemple crée SSH maître de clés nécessaires tooconnect toohello Linux. Cet exemple utilise *azureuser* pour un nom d’utilisateur administratif et *myPassword12* comme mot de passe hello sur les nœuds de Windows hello. Mettre à jour ces environnement tooyour approprié de toosomething valeurs. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Après quelques minutes, commande hello se termine et présente des informations sur votre déploiement.

## <a name="install-kubectl"></a>Installer kubectl

tooconnect toohello Kubernetes de cluster à partir de votre ordinateur client, utilisez [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), client de ligne de commande Kubernetes hello. 

Si vous utilisez Azure CloudShell, l’outil `kubectl` est déjà installé. Si vous souhaitez tooinstall elle, vous pouvez utiliser localement hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) commande.

Hello suivant CLI d’Azure exemple installe `kubectl` tooyour système. Sur Windows, exécutez cette commande en tant qu’administrateur.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Se connecter avec kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster exécuter hello [az acs kubernetes get-informations d’identification](/cli/azure/acs/kubernetes#get-credentials) commande. Hello exemple suivant télécharge configuration du cluster pour votre cluster Kubernetes hello.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

cluster de tooyour connexion tooverify hello à partir de votre ordinateur, essayez d’exécuter :

```azurecli-interactive
kubectl get nodes
```

`kubectl`Répertorie les nœuds principal et l’agent hello.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Déployer un conteneur Windows IIS

Vous pouvez exécuter un conteneur Docker à l’intérieur d’un *pod* Kubernetes, qui contient un ou plusieurs conteneurs. 

Cet exemple de base utilise un toospecify de fichier JSON un conteneur Microsoft Internet Information Server (IIS) et crée ensuite des pod hello à l’aide de hello `kubctl apply` commande. 

Créer un fichier local nommé `iis.json` et hello de copie après le texte. Ce fichier indique Kubernetes toorun IIS sur Windows Server 2016 Nano Server, à l’aide d’une image de conteneur public [Hub Docker](https://hub.docker.com/r/nanoserver/iis/). conteneur de Hello utilise le port 80, mais initialement est uniquement accessible dans le réseau de cluster hello.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

bloc de hello toostart, type :
  
```azurecli-interactive
kubectl apply -f iis.json
```  

déploiement de hello tootrack, type :
  
```azurecli-interactive
kubectl get pods
```

Lors du déploiement de pod de hello, état de hello est `ContainerCreating`. Il peut prendre quelques minutes pour hello de hello conteneur tooenter `Running` état.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Hello d’affichage page d’accueil IIS

tooexpose pod toohello Bonjour avec une adresse IP publique, hello type commande suivante :

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

Cette commande Kubernetes crée un service et un [règle d’équilibreur de charge Azure](container-service-kubernetes-load-balancing.md) avec une adresse IP publique pour le service de hello. 

Exécutez hello suivant l’état du service de hello hello de toosee la commande.

```azurecli-interactive
kubectl get svc
```

Adresse IP de hello s’affiche initialement en tant que `pending`. Après quelques minutes, hello adresse IP externe de hello `iis` pod est définie :
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Vous pouvez utiliser un navigateur web de votre choix toosee hello par défaut IIS page d’accueil à l’adresse IP externe de hello :

![Image de navigation tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Supprimer un cluster
Lorsque le cluster de hello n’est plus nécessaire, vous pouvez utiliser hello [suppression du groupe az](/cli/azure/group#delete) groupe de ressources tooremove hello, service de conteneur et toutes les ressources de la commande.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Étapes suivantes

Par le biais de ce guide de démarrage rapide, vous avez déployé un cluster Kubernetes, vous vous êtes connecté avec `kubectl` et vous avez déployé un pod avec un conteneur IIS. toolearn en savoir plus sur le Service de conteneur Azure, continuer toohello Kubernetes didacticiel.

> [!div class="nextstepaction"]
> [Gérer un cluster Kubernetes ACS](container-service-tutorial-kubernetes-prepare-app.md)
