---
title: "conteneurs d’aaaDeploy avec dirigeants dans Azure Kubernetes | Documents Microsoft"
description: Utiliser des conteneurs de toodeploy hello dirigeants empaquetage outil sur un cluster Kubernetes dans le Service de conteneur Azure
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Utiliser des conteneurs de toodeploy dirigeants sur un cluster Kubernetes 

[Dirigeants](https://github.com/kubernetes/helm/) est un outil de mise en package open source qui vous aide à installer et gérer hello du cycle de vie des applications de Kubernetes. Gestionnaires de packages tooLinux similaires tels que get-Apt et Yum, dirigeants est utilisé toomanage Kubernetes graphiques, qui sont des packages de ressources Kubernetes préconfigurées. Cet article vous explique comment toowork avec dirigeants sur un cluster Kubernetes déployé dans le Service de conteneur Azure.

Helm comprend deux composants : 
* Hello **dirigeants CLI** est un client qui s’exécute sur votre ordinateur local ou dans le cloud de hello  

* **Hauteur** est un serveur qui s’exécute sur un cluster de Kubernetes hello et gère hello du cycle de vie de vos applications Kubernetes 
 
## <a name="prerequisites"></a>Composants requis

* [Déployer un cluster Kubernetes](container-service-kubernetes-walkthrough.md) dans Azure Container Service

* [Installer et configurer `kubectl`](../container-service-connect.md) sur un ordinateur local

* [Installer Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) sur un ordinateur local

## <a name="helm-basics"></a>Principes de base Helm 

tooview informations hello Kubernetes cluster que vous installez la hauteur et le déploiement de vos applications, tapez Bonjour de commande suivante :

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Une fois que vous avez installé les dirigeants, installez hauteur sur votre cluster Kubernetes en tapant hello de commande suivante :

```bash
helm init --upgrade
```
Lorsqu’il s’achève avec succès, vous voyez la sortie hello suivante :

![Installation de Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview de commandes de tous les hello dirigeants graphiques disponibles dans le référentiel de hello, hello du type suivant :

```bash 
helm search 
```

Vous voyez la sortie hello suivante :

![Recherche dans Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello graphiques tooget hello versions les plus récentes, tapez :

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Déployer un graphique de contrôleur d’entrée Nginx 
 
toodeploy un graphique de contrôleur Nginx en entrée, tapez une commande unique :

```bash
helm install stable/nginx-ingress 
```
![Déployer un contrôleur d’entrée](./media/container-service-kubernetes-helm/nginx-ingress.png)

Si vous tapez `kubectl get svc` tooview tous les services qui sont exécutent sur le cluster de hello, vous voyez qu’une adresse IP est attribuée de contrôleur d’entrée toohello. (Pendant l’affectation de hello est en cours, `<pending>`. Elle prend quelques minutes toocomplete.) 

Une fois que l’adresse IP de hello est affectée, accédez à valeur toohello hello externe IP adresse toosee hello Nginx principal en cours d’exécution. 
 
![Adresse IP d’entrée](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee une liste de graphiques est installé sur votre cluster, de type :

```bash
helm list 
```

Vous pouvez abréger commande hello trop`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Déployer un graphique et un client MariaDB

Déployer maintenant un graphique MariaDB et une base de données MariaDB client tooconnect toohello.

graphique de MariaDB hello toodeploy, hello type commande suivante :

```bash
helm install --name v1 stable/mariadb
```

où `--name` est une balise utilisée pour les publications.

> [!TIP]
> En cas d’échec du déploiement de hello, utilisez `helm repo update` et recommencez l’opération.
>
 
 
tooview tous les graphiques hello déploiement sur votre cluster, de type :

```bash 
helm list
```
 
tooview tous les déploiements en cours d’exécution sur votre cluster, tapez :

```bash
kubectl get deployments 
``` 
 
 
Enfin, toorun un client pod tooaccess hello, tapez :

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
tooconnect toohello client, hello type commande suivante, en remplaçant `v1-mariadb` par nom de hello de votre déploiement :

```bash
sudo mysql –h v1-mariadb
```
 
 
Vous pouvez maintenant utiliser des bases de données toocreate de commandes SQL standard, les tables, etc.. Par exemple, `Create DATABASE testdb1;` crée une base de données vide. 
 
 
 
## <a name="next-steps"></a>Étapes suivantes

* Pour plus d’informations sur la gestion Kubernetes graphiques, consultez hello [dirigeants documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

