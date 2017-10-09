---
title: cluster de Azure Kubernetes aaaMonitor avec Datadog | Documents Microsoft
description: "Surveillance du cluster Kubernetes dans Azure Container Service à l’aide de Datadog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Surveiller un cluster Azure Container Service avec Datadog

## <a name="prerequisites"></a>Composants requis
Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).

Il suppose également que vous avez hello `az` cli Azure et `kubectl` outils sont installés.

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

## <a name="datadog"></a>DataDog
Datadog est un service de surveillance qui regroupe les données de surveillance provenant de vos conteneurs dans votre cluster Azure Container Service. Datadog intègre un tableau de bord Docker Integration qui affiche des mesures spécifiques dans vos conteneurs. Les mesures recueillies à partir de vos conteneurs sont classées par processeur, mémoire, réseau et E/S. Datadog fractionne les mesures en conteneurs et images.

Vous devez tout d’abord trop[créer un compte](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>L’installation de hello Datadog Agent avec un DaemonSet
DaemonSets sont utilisés par Kubernetes toorun une instance unique d’un conteneur sur chaque hôte de cluster de hello.
Ils sont parfaits pour exécuter des agents de surveillance.

Une fois que vous êtes connecté à Datadog, vous pouvez suivre hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) agents de Datadog tooinstall sur votre cluster à l’aide d’un DaemonSet.

## <a name="conclusion"></a>Conclusion
Et voilà ! Une fois que les agents hello sont activés et en cours d’exécution vous devez voir des données dans la console hello dans quelques minutes. Vous pouvez visiter hello intégré [kubernetes le tableau de bord](https://app.datadoghq.com/screen/integration/kubernetes) toosee un résumé de votre cluster.
