---
title: didacticiel de Service de conteneur aaaAzure - moniteur Kubernetes | Documents Microsoft
description: "Didacticiel Azure Container Service - Surveiller Kubernetes à l’aide de Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Surveiller un cluster Kubernetes à l’aide d’Operations Management Suite

La surveillance de votre cluster Kubernetes et des conteneurs est cruciale, particulièrement lorsque vous gérez un cluster de production à grande échelle avec plusieurs applications. 

Vous pouvez tirer parti de plusieurs solutions de surveillance Kubernetes, à partir de Microsoft ou d’autres fournisseurs. Dans ce didacticiel, vous surveillez votre cluster Kubernetes à l’aide de solutions de conteneurs hello dans [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), solution de gestion informatique en nuage de Microsoft. (hello solution de conteneurs d’OMS est en version préliminaire.)

Ce didacticiel, partie 7 sept et couvre hello tâches suivantes :

> [!div class="checklist"]
> * Obtenir les paramètres de l’espace de travail OMS
> * Configurer les agents OMS sur les nœuds de Kubernetes hello
> * Accéder aux informations d’analyse dans le portail OMS est hello ou le portail Azure

## <a name="before-you-begin"></a>Avant de commencer

Dans les didacticiels précédents, une application a été empaquetée dans des images de conteneur, ces images téléchargées tooAzure Registre de conteneur et un cluster Kubernetes créé. Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md). 

Ce didacticiel nécessite au minimum un cluster Kubernetes avec des nœuds d’agent Linux, et un compte Operations Management Suite (OMS). Au besoin, inscrivez-vous à un [essai OMS gratuit](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Obtenir les paramètres de l’espace de travail

Lorsque vous pouvez accéder à hello [portail OMS](https://mms.microsoft.com), accédez trop**paramètres** > **Sources connectées** > **des serveurs Linux**. Là, vous pouvez trouver hello *ID de l’espace de travail* et principal ou secondaire *clé de l’espace de travail*. Prenez note de ces valeurs, vous devez tooset des agents OMS sur le cluster de hello.

## <a name="set-up-oms-agents"></a>Configurer les agents OMS

Voici un tooset de fichier YAML des agents OMS sur les nœuds de cluster Linux hello. Il crée un [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) Kubernetes qui exécute un seul et même pod sur chaque nœud de cluster. Hello DaemonSet ressource est idéal pour le déploiement d’un agent de surveillance. 

Enregistrer hello nommé par le fichier texte tooa suivant `oms-daemonset.yaml`et remplacez les valeurs d’espace réservé hello pour *myWorkspaceID* et *myWorkspaceKey* avec votre ID d’espace de travail OMS et la clé. (En production, vous pouvez encoder ces valeurs en tant que secrets).

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Créer hello DaemonSet avec hello de commande suivante :

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

toosee que hello DaemonSet est créé, exécutez :

```azurecli-interactive
kubectl get daemonset
```

La sortie est similaire toohello suivantes :

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Une fois que les agents hello sont en cours d’exécution, il prend plusieurs minutes avant que les données de salutation OMS tooingest et processus.

## <a name="access-monitoring-data"></a>Accéder aux données de surveillance

Afficher et analyser le conteneur d’OMS hello analyse les données avec hello [solutions de conteneur](../../log-analytics/log-analytics-containers.md) dans hello OMS portal ou hello portail Azure. 

solution de conteneur de hello tooinstall à l’aide de hello [portail OMS](https://mms.microsoft.com), accédez trop**galerie des Solutions**. Ensuite, ajoutez **Solution Containers**. Également ajouter des solutions de conteneurs hello de hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

Dans le portail OMS : hello, recherchez un **conteneurs** vignette résumé sur le tableau de bord OMS hello. Cliquez sur la vignette hello pour plus d’informations, y compris : les événements de conteneur, les erreurs, l’état, inventaire de l’image et utilisation du processeur et mémoire. Pour obtenir des informations plus précises, cliquez sur une ligne dans une vignette, ou effectuez une [recherche dans les journaux](../../log-analytics/log-analytics-log-searches.md).

![Tableau de bord Containers dans le portail OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

De même, Bonjour portail Azure, accédez trop**Analytique de journal** et sélectionnez le nom de votre espace de travail. toosee hello **conteneurs** vignette de résumé, cliquez sur **Solutions** > **conteneurs**. toosee plus d’informations, cliquez sur la vignette de hello.

Consultez hello [documentation de l’Analytique des journaux Azure](../../log-analytics/index.md) pour obtenir des instructions détaillées sur l’interrogation et l’analyse des données d’analyse.

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous surveillez votre cluster Kubernetes avec OMS. Les tâches traitées ont inclus :

> [!div class="checklist"]
> * Obtenir les paramètres de l’espace de travail OMS
> * Configurer les agents OMS sur les nœuds de Kubernetes hello
> * Accéder aux informations d’analyse dans le portail OMS est hello ou le portail Azure


Suivez cette toosee lien prégénérées des exemples de scripts pour le Service de conteneur.

> [!div class="nextstepaction"]
> [Exemples de scripts Azure Container Service](cli-samples.md)
