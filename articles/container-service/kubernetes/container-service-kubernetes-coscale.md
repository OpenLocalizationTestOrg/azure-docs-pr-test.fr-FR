---
title: "Surveiller un cluster Azure Kubernetes avec CoScale | Microsoft Docs"
description: "Surveiller un cluster Kubernetes dans Azure Container Service à l’aide de CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f894191baced710fc0f5a8c8692df98033341a48
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Surveiller un cluster Kubernetes Azure Container Service avec CoScale

Dans cet article, nous vous montrons comment déployer l’agent [CoScale](https://www.coscale.com/) pour surveiller tous les nœuds et tous les conteneurs de votre cluster Kubernetes dans Azure Container Service. Vous avez besoin d’un compte CoScale pour cette configuration. 


## <a name="about-coscale"></a>À propos de CoScale 

CoScale est une plateforme de surveillance qui collecte les mesures et les événements de tous les conteneurs dans plusieurs plateformes d’orchestration. CoScale offre une surveillance complète pour les environnements Kubernetes. Il fournit des visualisations et des analyses pour toutes les couches de la pile : le système d’exploitation Kubernetes, Docker et les applications qui s’exécutent dans vos conteneurs. CoScale propose plusieurs tableaux de bord de surveillance intégrés, et fournit une fonctionnalité intégrée de détection des anomalies qui permet aux opérateurs et aux développeurs de détecter rapidement les problèmes liés aux infrastructures et aux applications.

![Interface utilisateur CoScale](./media/container-service-kubernetes-coscale/coscale.png)

Comme indiqué dans cet article, vous pouvez installer des agents sur un cluster Kubernetes pour exécuter CoScale en tant que solution SaaS. Si vous souhaitez conserver vos données sur site, CoScale est également disponible pour une installation locale.


## <a name="prerequisites"></a>Composants requis

Vous devez d’abord [créer un compte CoScale](https://www.coscale.com/free-trial).

Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).

Elle suppose également que vous avez installé les outils de l’interface Azure CLI `az` et `kubectl`.

Vous pouvez tester si l’outil `az` est installé en exécutant :

```azurecli
az --version
```

Si l’outil `az` n’est pas installé, suivez les instructions figurant [ici](/cli/azure/install-azure-cli).

Vous pouvez tester si l’outil `kubectl` est installé en exécutant :

```bash
kubectl version
```

Si `kubectl` n’est pas installé, vous pouvez exécuter :

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-the-coscale-agent-with-a-daemonset"></a>Installation de l’agent CoScale avec un DaemonSet
Les [DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) sont utilisés par Kubernetes pour exécuter une instance unique d’un conteneur sur chaque hôte du cluster.
Ils sont parfaits pour exécuter des agents de surveillance, tels que l’agent CoScale.

Une fois que vous êtes connecté à CoScale, accédez à la [page de l’agent](https://app.coscale.com/) pour installer les agents CoScale sur votre cluster à l’aide d’un DaemonSet. L’interface utilisateur CoScale fournit les étapes de configuration guidée pour créer un agent et entamer la surveillance de votre cluster Kubernetes complet.

![Configuration de l’agent CoScale](./media/container-service-kubernetes-coscale/installation.png)

Pour démarrer l’agent sur le cluster, exécutez la commande fournie :

![Démarrez l’agent CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

Et voilà ! Dès que les agents sont en cours d’exécution, des données s’affichent dans la console après quelques minutes. Visitez la [page de l’agent](https://app.coscale.com/) pour afficher un résumé de votre cluster, effectuer les étapes de configuration supplémentaires et consulter les tableaux de bord, comme la **vue d’ensemble du cluster Kubernetes**.

![Vue d’ensemble du cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

L’agent CoScale est déployé automatiquement sur les nouvelles machines dans le cluster. L’agent se met à jour automatiquement lorsqu’une nouvelle version est publiée.


## <a name="next-steps"></a>Étapes suivantes

Consultez la [documentation CoScale](http://docs.coscale.com/) et le [blog](https://www.coscale.com/blog) pour en savoir plus sur les solutions de surveillance CoScale. 

