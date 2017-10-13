---
title: "Surveiller le cluster Kubernetes Azure - Gestion des opérations | Microsoft Docs"
description: "Surveillance d’un cluster Kubernetes dans Azure Container Service à l’aide de Microsoft Operations Management Suite"
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
ms.openlocfilehash: bd5c81435c091d25bc14710589b7c043e9f56a25
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Surveiller un cluster Azure Container Service avec Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Composants requis
Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).

Elle suppose également que vous avez installé l’outil `az` de l’interface Azure CLI et l’outil `kubectl`.

Vous pouvez tester si l’outil `az` est installé en exécutant :

```console
$ az --version
```

Si l’outil `az` n’est pas installé, suivez les instructions figurant [ici](https://github.com/azure/azure-cli#installation).  
Sinon, vous pouvez utiliser [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), avec `az`l’interface de ligne Azure et les `kubectl` outils déjà installés pour vous.  

Vous pouvez tester si l’outil `kubectl` est installé en exécutant :

```console
$ kubectl version
```

Si `kubectl` n’est pas installé, vous pouvez exécuter :
```console
$ az acs kubernetes install-cli
```

Pour tester si les clés kubernetes sont installées dans votre outil kubectl vous pouvez exécuter :
```console
$ kubectl get nodes
```

Si les erreurs de commande ci-dessus sortent, vous devez installer les clés de cluster kubernetes dans votre outil kubectl. Ceci peut se faire avec la commande suivante :
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Surveillance de conteneurs avec Operations Management Suite (OMS)

Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. La solution Conteneurs fait partie intégrante d’OMS Log Analytics, qui vous octroie une visibilité sur le stock, les performances et les fichiers journaux des conteneurs à un emplacement unique. Vous pouvez auditer les conteneurs, résoudre les problèmes en consultant les fichiers journaux de manière centralisée, et identifier les conteneurs bruyants à consommation supérieure sur un hôte.

![](media/container-service-monitoring-oms/image1.png)

Pour plus d’informations sur la solution Conteneurs, reportez-vous à [Solution Conteneurs (version préliminaire) Log Analytics](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Installation d’OMS sur Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Obtenir l’ID et la clé d’espace de travail
Pour que l’agent OMS puisse communiquer avec le service, il doit être configuré avec un ID et une clé d’espace de travail. Pour les obtenir, vous devez créer un compte OMS à l’adresse <https://mms.microsoft.com>. Suivez la procédure de création de compte. Une fois que vous avez créé le compte, vous devez obtenir votre ID et votre clé d’espace de travail en cliquant sur **Paramètres**, **Sources connectées**, puis sur **Serveurs Linux**, comme indiqué ci-dessous.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a>Installer l’agent OMS à l’aide d’un DaemonSet
Les DaemonSets sont utilisés par DaemonSet pour exécuter une instance unique d’un conteneur sur chaque hôte du cluster.
Ils sont parfaits pour exécuter des agents de surveillance.

Voici le [fichier DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Enregistrez-le sous le nom `oms-daemonset.yaml` et remplacez dans ce fichier les valeurs des espaces réservés pour `WSID` et `KEY` par l’ID et la clé de votre espace de travail.

Une fois vos ID et clé d’espace de travail ajoutés à la configuration de DaemonSet, vous pouvez installer l’agent OMS sur votre cluster à l’aide de l’outil de ligne de commande `kubectl` :

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-oms-agent-using-a-kubernetes-secret"></a>Installation de l’agent OMS à l’aide d’une clé secrète Kubernetes
Pour protéger votre ID d’espace de travail OMS et la clé vous pouvez utiliser les clés secrètes Kubernetes dans le cadre du fichier YAML DaemonSet.

 - Copiez le script, le fichier modèle de la clé secrète et le fichier YAML DaemonSet (dans le [référentiel](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) et assurez-vous qu’ils se trouvent dans le même répertoire. 
      - clé de secret générant le script - secret-gen.sh
      - modèle de clé de secret - secret-template.yaml
   - Fichier DaemonSet YAML - omsagent-ds-secrets.yaml
 - Exécutez le script. Le script demande l’ID d’espace de travail OMS et la clé primaire. Veuillez l’insérer. Le script crée un fichier yaml secret pour que vous puissiez l’exécuter.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Créez le pod de clés secrètes en exécutant la commande suivante : ``` kubectl create -f omsagentsecret.yaml ```
 
   - Pour vérifier, exécutez la commande suivante : 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Créer votre DaemonsSet omsagent en exécutant ``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Conclusion
Et voilà ! Après quelques minutes, vous devez être en mesure de voir le flux de données vers votre tableau de bord OMS.
