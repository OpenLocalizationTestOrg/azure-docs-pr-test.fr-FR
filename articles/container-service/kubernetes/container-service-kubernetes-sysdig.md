---
title: cluster de Azure Kubernetes aaaMonitor - Sysdig | Documents Microsoft
description: "Surveillance du cluster Kubernetes dans Azure Container Service à l’aide de Sysdig"
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Surveiller un cluster Kubernetes Azure Container Service avec Sysdig

## <a name="prerequisites"></a>Conditions préalables
Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).

Il suppose également que vous disposez des outils cli et kubectl hello azure installés.

Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :

```console
$ az --version
```

Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).

Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :

```console
$ kubectl version
```

Si `kubectl` n’est pas installé, vous pouvez exécuter :

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a>Sysdig
Sysdig est une société de surveillance en tant que service pouvant analyser les conteneurs de votre cluster Kubernetes exécuté dans Azure. L’utilisation de Sysdig nécessite un compte Sysdig actif.
Vous pouvez créer un compte Azure sur leur [site](https://app.sysdigcloud.com).

Une fois que vous êtes connecté dans le site Web du cloud toohello Sysdig, cliquez sur votre nom d’utilisateur et sur la page de hello, vous devez voir votre « clé d’accès ». 

![Clé d’API Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>L’installation hello Sysdig agents tooKubernetes
toomonitor vos conteneurs, et s’exécute de Sysdig un processus sur chaque ordinateur à l’aide d’un Kubernetes `DaemonSet`.
Les DaemonSets sont des objets API Kubernetes qui exécutent une instance unique d’un conteneur par machine.
Ils conviennent parfaitement pour l’installation des outils comme hello agent d’analyse de Sysdig.

tooinstall hello Sysdig daemonset, vous devez tout d’abord télécharger [modèle de hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) à partir de sysdig. Enregistrez ce fichier sous `sysdig-daemonset.yaml`.

Sur Linux et OS X, vous pouvez exécuter :

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

Dans PowerShell :

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Ensuite modifier ce fichier tooinsert votre clé d’accès, que vous avez obtenue à partir de votre compte Sysdig.

Enfin, créez hello DaemonSet :

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>Afficher votre analyse
Une fois installé et en cours d’exécution, les agents hello doivent pump tooSysdig précédent de données.  Revenir en arrière toothe [sysdig le tableau de bord](https://app.sysdigcloud.com) et vous devez obtenir des informations sur vos conteneurs.

Vous pouvez également installer des tableaux de bords spécifiques de Kubernetes en utilisant [l’Assistant Nouveau tableau de bord](https://app.sysdigcloud.com/#/dashboards/new).
