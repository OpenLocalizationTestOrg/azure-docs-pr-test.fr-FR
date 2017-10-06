---
title: "cluster de Azure Kubernetes aaaMonitor - gestion des opérations | Documents Microsoft"
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
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Surveiller un cluster Azure Container Service avec Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Composants requis
Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).

Il suppose également que vous avez hello `az` cli Azure et `kubectl` outils sont installés.

Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :

```console
$ az --version
```

Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).  
Vous pouvez également utiliser [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), qui a hello `az` cli Azure et `kubectl` outils déjà installés pour vous.  

Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :

```console
$ kubectl version
```

Si `kubectl` n’est pas installé, vous pouvez exécuter :
```console
$ az acs kubernetes install-cli
```

tootest si vous avez des clés kubernetes installés dans votre outil kubectl que vous pouvez exécuter :
```console
$ kubectl get nodes
```

Si hello ci-dessus erreurs de commande out, vous avez besoin de clés de cluster tooinstall kubernetes dans votre outil kubectl. Vous pouvez faire cela avec hello de commande suivante :
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Surveillance de conteneurs avec Operations Management Suite (OMS)

Microsoft Operations Management Suite (OMS) est une solution de gestion informatique basée sur le cloud de Microsoft qui vous permet de gérer et de protéger votre infrastructure locale et de cloud. Conteneur est une solution dans Analytique de journal d’OMS, ce qui vous permet d’afficher l’inventaire hello conteneur, les performances et les journaux dans un emplacement unique. Vous pouvez auditer, résoudre des conteneurs en consultant les journaux hello dans un emplacement centralisé et trouver bruyantes consommation excessive conteneur sur un ordinateur hôte.

![](media/container-service-monitoring-oms/image1.png)

Pour plus d’informations sur les solutions de conteneur, reportez-vous à toothe [Analytique de journal conteneur Solution](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Installation d’OMS sur Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Obtenir l’ID et la clé d’espace de travail
Pourquoi le service de toohello tootalk OMS agent, elle doit toobe configuré avec un id de l’espace de travail et une clé de l’espace de travail. compte tooget hello id et la clé que vous avez besoin de toocreate un OMS <https://mms.microsoft.com>. Veuillez suivre hello étapes toocreate un compte. Une fois que vous avez terminé la création de compte de hello, vous devez tooobtain id et votre clé en cliquant sur **paramètres**, puis **Sources connectées**, puis **des serveurs Linux**, comme illustré ci-dessous.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Installer l’agent OMS de hello à l’aide d’un DaemonSet
DaemonSets sont utilisés par Kubernetes toorun une instance unique d’un conteneur sur chaque hôte de cluster de hello.
Ils sont parfaits pour exécuter des agents de surveillance.

Voici hello [fichier de DaemonSet YAML](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Enregistrer les fichiers tooa nommé `oms-daemonset.yaml` et remplacer des valeurs d’espace réservé hello pour `WSID` et `KEY` avec l’id de l’espace de travail et votre clé dans le fichier de hello.

Une fois que vous avez ajouté votre ID d’espace de travail et de la configuration de DaemonSet toohello clé, vous pouvez installer l’agent OMS de hello sur votre cluster avec hello `kubectl` outil de ligne de commande :

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>L’installation de l’agent OMS de hello à l’aide d’une clé secrète Kubernetes
tooprotect votre ID d’espace de travail OMS et la clé que vous pouvez utiliser Kubernetes Secret comme une partie du fichier de DaemonSet YAML.

 - Copier les script hello, fichier modèle secrète et hello fichier de DaemonSet YAML (à partir de [référentiel](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) et assurez-vous qu’ils sont sur hello même répertoire. 
      - clé de secret générant le script - secret-gen.sh
      - modèle de clé de secret - secret-template.yaml
   - Fichier DaemonSet YAML - omsagent-ds-secrets.yaml
 - Exécutez le script de hello. script de Hello demandera hello ID d’espace de travail OMS et la clé primaire. Veuillez insérer qui et hello script crée un fichier yaml secrète, vous pouvez l’exécuter.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Créer des pod de secrets hello en exécutant hello suivante :``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, exécutez hello suivante : 

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
 
  - Créer votre DaemonsSet de l’agent OMS en exécutant ``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Conclusion
Et voilà ! Après quelques minutes, vous devez être en mesure de toosee transferts de données du tableau de bord OMS tooyour.
