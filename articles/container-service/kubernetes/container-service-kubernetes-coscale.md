---
title: aaaMonitor un Kubernetes Azure cluster avec CoScale | Documents Microsoft
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
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Surveiller un cluster Kubernetes Azure Container Service avec CoScale

Dans cet article, nous vous indiquons comment toodeploy hello [CoScale](https://www.coscale.com/) toomonitor agent tous les nœuds et les conteneurs dans votre Kubernetes de cluster dans le conteneur de Service Azure. Vous avez besoin d’un compte CoScale pour cette configuration. 


## <a name="about-coscale"></a>À propos de CoScale 

CoScale est une plateforme de surveillance qui collecte les mesures et les événements de tous les conteneurs dans plusieurs plateformes d’orchestration. CoScale offre une surveillance complète pour les environnements Kubernetes. Il fournit des visualisations et analytique pour toutes les couches de la pile de hello : hello du système d’exploitation, Kubernetes, Docker et les applications en cours d’exécution à l’intérieur de vos conteneurs. CoScale offre plusieurs analyse tableaux de bord intégrés et il a des opérateurs de tooallow de détection d’anomalie intégrés et les problèmes aux développeurs toofind infrastructure et d’application rapidement.

![Interface utilisateur CoScale](./media/container-service-kubernetes-coscale/coscale.png)

Comme indiqué dans cet article, vous pouvez installer des agents sur un toorun de cluster Kubernetes CoScale comme une solution SaaS. Si vous souhaitez tookeep vos données sur site, CoScale est également disponible pour l’installation locale.


## <a name="prerequisites"></a>Composants requis

Vous devez tout d’abord trop[créer un compte CoScale](https://www.coscale.com/free-trial).

Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).

Il suppose également que vous avez hello `az` CLI d’Azure et `kubectl` outils sont installés.

Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :

```azurecli
az --version
```

Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](/cli/azure/install-azure-cli).

Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :

```bash
kubectl version
```

Si `kubectl` n’est pas installé, vous pouvez exécuter :

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>L’installation de l’agent de hello CoScale avec un DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) sont utilisés par Kubernetes toorun une instance unique d’un conteneur sur chaque hôte de cluster de hello.
Ils conviennent parfaitement pour l’exécution des agents de surveillance de l’agent de CoScale hello.

Une fois que vous vous connectez tooCoScale, accédez à toohello [page de l’agent](https://app.coscale.com/) agents de CoScale tooinstall sur votre cluster à l’aide d’un DaemonSet. Hello CoScale UI fournit toocreate des étapes de configuration interactive un agent et le démarrer l’analyse complète de votre cluster Kubernetes.

![Configuration de l’agent CoScale](./media/container-service-kubernetes-coscale/installation.png)

agent de hello toostart sur cluster hello, exécutez la commande hello fourni :

![Démarrer l’agent de hello CoScale](./media/container-service-kubernetes-coscale/agent_script.png)

Et voilà ! Une fois que les agents hello sont en cours d’exécution, vous devez voir les données dans la console hello dans quelques minutes. Visitez hello [page de l’agent](https://app.coscale.com/) toosee un résumé de votre cluster, effectuez les étapes de configuration supplémentaires et consultez les tableaux de bord telles que hello **Kubernetes présentation des clusters**.

![Vue d’ensemble du cluster Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

Hello CoScale agent est automatiquement déployé sur des ordinateurs dans un cluster de hello. Hello agent mises à jour automatiquement lorsqu’une nouvelle version est disponible.


## <a name="next-steps"></a>Étapes suivantes

Consultez hello [CoScale documentation](http://docs.coscale.com/) et [blog](https://www.coscale.com/blog) pour plus d’informations sur la surveillance des solutions de CoScale. 

