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
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="07e29-103">Utiliser des conteneurs de toodeploy dirigeants sur un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="07e29-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="07e29-104">[Dirigeants](https://github.com/kubernetes/helm/) est un outil de mise en package open source qui vous aide à installer et gérer hello du cycle de vie des applications de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="07e29-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="07e29-105">Gestionnaires de packages tooLinux similaires tels que get-Apt et Yum, dirigeants est utilisé toomanage Kubernetes graphiques, qui sont des packages de ressources Kubernetes préconfigurées.</span><span class="sxs-lookup"><span data-stu-id="07e29-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="07e29-106">Cet article vous explique comment toowork avec dirigeants sur un cluster Kubernetes déployé dans le Service de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="07e29-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="07e29-107">Helm comprend deux composants :</span><span class="sxs-lookup"><span data-stu-id="07e29-107">Helm has two components:</span></span> 
* <span data-ttu-id="07e29-108">Hello **dirigeants CLI** est un client qui s’exécute sur votre ordinateur local ou dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="07e29-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="07e29-109">**Hauteur** est un serveur qui s’exécute sur un cluster de Kubernetes hello et gère hello du cycle de vie de vos applications Kubernetes</span><span class="sxs-lookup"><span data-stu-id="07e29-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="07e29-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="07e29-110">Prerequisites</span></span>

* <span data-ttu-id="07e29-111">[Déployer un cluster Kubernetes](container-service-kubernetes-walkthrough.md) dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="07e29-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="07e29-112">[Installer et configurer `kubectl`](../container-service-connect.md) sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="07e29-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="07e29-113">[Installer Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="07e29-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="07e29-114">Principes de base Helm</span><span class="sxs-lookup"><span data-stu-id="07e29-114">Helm basics</span></span> 

<span data-ttu-id="07e29-115">tooview informations hello Kubernetes cluster que vous installez la hauteur et le déploiement de vos applications, tapez Bonjour de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e29-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="07e29-117">Une fois que vous avez installé les dirigeants, installez hauteur sur votre cluster Kubernetes en tapant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e29-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="07e29-118">Lorsqu’il s’achève avec succès, vous voyez la sortie hello suivante :</span><span class="sxs-lookup"><span data-stu-id="07e29-118">When it completes successfully, you see output like hello following:</span></span>

![Installation de Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="07e29-120">tooview de commandes de tous les hello dirigeants graphiques disponibles dans le référentiel de hello, hello du type suivant :</span><span class="sxs-lookup"><span data-stu-id="07e29-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="07e29-121">Vous voyez la sortie hello suivante :</span><span class="sxs-lookup"><span data-stu-id="07e29-121">You see output like hello following:</span></span>

![Recherche dans Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="07e29-123">tooupdate hello graphiques tooget hello versions les plus récentes, tapez :</span><span class="sxs-lookup"><span data-stu-id="07e29-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="07e29-124">Déployer un graphique de contrôleur d’entrée Nginx</span><span class="sxs-lookup"><span data-stu-id="07e29-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="07e29-125">toodeploy un graphique de contrôleur Nginx en entrée, tapez une commande unique :</span><span class="sxs-lookup"><span data-stu-id="07e29-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Déployer un contrôleur d’entrée](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="07e29-127">Si vous tapez `kubectl get svc` tooview tous les services qui sont exécutent sur le cluster de hello, vous voyez qu’une adresse IP est attribuée de contrôleur d’entrée toohello.</span><span class="sxs-lookup"><span data-stu-id="07e29-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="07e29-128">(Pendant l’affectation de hello est en cours, `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="07e29-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="07e29-129">Elle prend quelques minutes toocomplete.)</span><span class="sxs-lookup"><span data-stu-id="07e29-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="07e29-130">Une fois que l’adresse IP de hello est affectée, accédez à valeur toohello hello externe IP adresse toosee hello Nginx principal en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="07e29-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Adresse IP d’entrée](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="07e29-132">toosee une liste de graphiques est installé sur votre cluster, de type :</span><span class="sxs-lookup"><span data-stu-id="07e29-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="07e29-133">Vous pouvez abréger commande hello trop`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="07e29-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="07e29-134">Déployer un graphique et un client MariaDB</span><span class="sxs-lookup"><span data-stu-id="07e29-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="07e29-135">Déployer maintenant un graphique MariaDB et une base de données MariaDB client tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="07e29-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="07e29-136">graphique de MariaDB hello toodeploy, hello type commande suivante :</span><span class="sxs-lookup"><span data-stu-id="07e29-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="07e29-137">où `--name` est une balise utilisée pour les publications.</span><span class="sxs-lookup"><span data-stu-id="07e29-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="07e29-138">En cas d’échec du déploiement de hello, utilisez `helm repo update` et recommencez l’opération.</span><span class="sxs-lookup"><span data-stu-id="07e29-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="07e29-139">tooview tous les graphiques hello déploiement sur votre cluster, de type :</span><span class="sxs-lookup"><span data-stu-id="07e29-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="07e29-140">tooview tous les déploiements en cours d’exécution sur votre cluster, tapez :</span><span class="sxs-lookup"><span data-stu-id="07e29-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="07e29-141">Enfin, toorun un client pod tooaccess hello, tapez :</span><span class="sxs-lookup"><span data-stu-id="07e29-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="07e29-142">tooconnect toohello client, hello type commande suivante, en remplaçant `v1-mariadb` par nom de hello de votre déploiement :</span><span class="sxs-lookup"><span data-stu-id="07e29-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="07e29-143">Vous pouvez maintenant utiliser des bases de données toocreate de commandes SQL standard, les tables, etc.. Par exemple, `Create DATABASE testdb1;` crée une base de données vide.</span><span class="sxs-lookup"><span data-stu-id="07e29-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="07e29-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07e29-144">Next steps</span></span>

* <span data-ttu-id="07e29-145">Pour plus d’informations sur la gestion Kubernetes graphiques, consultez hello [dirigeants documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="07e29-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

