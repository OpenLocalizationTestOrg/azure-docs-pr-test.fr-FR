---
title: "Déployer des conteneurs avec Helm dans Azure Kubernetes | Microsoft Docs"
description: "Utiliser l’outil d’empaquetage Helm pour déployer des conteneurs sur un cluster Kubernetes dans Azure Container Service"
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
ms.openlocfilehash: 3cfcc5abbee03ca8fbbec4e4eae711e7c2d9deae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="54ee8-103">Utilisez Helm pour déployer des conteneurs sur un cluster Kubernetes</span><span class="sxs-lookup"><span data-stu-id="54ee8-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="54ee8-104">[Helm](https://github.com/kubernetes/helm/) est un outil d’empaquetage open source qui vous aide à installer et à gérer le cycle de vie d’applications Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="54ee8-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="54ee8-105">À l’instar de gestionnaires de package Linux tels que Apt-get et Yum, Helm sert à gérer les graphiques Kubernetes, qui sont des packages de ressources Kubernetes préconfigurés.</span><span class="sxs-lookup"><span data-stu-id="54ee8-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="54ee8-106">Cet article montre comment utiliser Helm sur un cluster Kubernetes déployé dans Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="54ee8-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="54ee8-107">Helm comprend deux composants :</span><span class="sxs-lookup"><span data-stu-id="54ee8-107">Helm has two components:</span></span> 
* <span data-ttu-id="54ee8-108">**Helm CLI** est un client qui s’exécute sur votre ordinateur en local ou dans le cloud</span><span class="sxs-lookup"><span data-stu-id="54ee8-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="54ee8-109">**Tiller** est un serveur qui s’exécute sur le cluster Kubernetes et gère le cycle de vie de vos applications Kubernetes</span><span class="sxs-lookup"><span data-stu-id="54ee8-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="54ee8-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="54ee8-110">Prerequisites</span></span>

* <span data-ttu-id="54ee8-111">[Déployer un cluster Kubernetes](container-service-kubernetes-walkthrough.md) dans Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="54ee8-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="54ee8-112">[Installer et configurer `kubectl`](../container-service-connect.md) sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="54ee8-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="54ee8-113">[Installer Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) sur un ordinateur local</span><span class="sxs-lookup"><span data-stu-id="54ee8-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="54ee8-114">Principes de base Helm</span><span class="sxs-lookup"><span data-stu-id="54ee8-114">Helm basics</span></span> 

<span data-ttu-id="54ee8-115">Pour afficher des informations concernant le cluster Kubernetes sur lequel vous installez Tiller et déployez vos applications, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54ee8-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="54ee8-117">Après avoir installé Helm, installez Tiller sur votre cluster Kubernetes en tapant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54ee8-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="54ee8-118">Une fois celle-ci exécutée avec succès, vous pouvez voir une sortie telle que la suivante :</span><span class="sxs-lookup"><span data-stu-id="54ee8-118">When it completes successfully, you see output like the following:</span></span>

![Installation de Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="54ee8-120">Pour afficher tous les graphiques Helm disponibles dans le référentiel, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54ee8-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="54ee8-121">Vous pouvez voir une sortie telle que la suivante :</span><span class="sxs-lookup"><span data-stu-id="54ee8-121">You see output like the following:</span></span>

![Recherche dans Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="54ee8-123">Pour mettre à jour les graphiques afin d’obtenir les dernières versions, tapez :</span><span class="sxs-lookup"><span data-stu-id="54ee8-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="54ee8-124">Déployer un graphique de contrôleur d’entrée Nginx</span><span class="sxs-lookup"><span data-stu-id="54ee8-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="54ee8-125">Pour déployer un graphique de contrôleur d’entrée Nginx, tapez une seule commande :</span><span class="sxs-lookup"><span data-stu-id="54ee8-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Déployer un contrôleur d’entrée](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="54ee8-127">Si vous tapez `kubectl get svc` pour afficher tous les services en cours d’exécution sur le cluster, vous voyez qu’une adresse IP est attribuée au contrôleur d’entrée.</span><span class="sxs-lookup"><span data-stu-id="54ee8-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="54ee8-128">(Bien que l’affectation soit en cours, vous voyez `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="54ee8-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="54ee8-129">Quelques minutes sont nécessaires pour achever l’opération.)</span><span class="sxs-lookup"><span data-stu-id="54ee8-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="54ee8-130">Une fois l’adresse IP adresse attribuée, accédez à la valeur de l’adresse IP externe pour voir le serveur principal Nginx en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="54ee8-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![Adresse IP d’entrée](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="54ee8-132">Pour afficher la liste des graphiques installés sur votre cluster, tapez :</span><span class="sxs-lookup"><span data-stu-id="54ee8-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="54ee8-133">Vous pouvez abréger la commande en `helm ls`.</span><span class="sxs-lookup"><span data-stu-id="54ee8-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="54ee8-134">Déployer un graphique et un client MariaDB</span><span class="sxs-lookup"><span data-stu-id="54ee8-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="54ee8-135">Déployez à présent un graphique et un client MariaDB pour vous connecter à la base de données.</span><span class="sxs-lookup"><span data-stu-id="54ee8-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="54ee8-136">Pour déployer le graphique MariaDB, tapez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="54ee8-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="54ee8-137">où `--name` est une balise utilisée pour les publications.</span><span class="sxs-lookup"><span data-stu-id="54ee8-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="54ee8-138">Si le déploiement échoue, exécutez `helm repo update` puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="54ee8-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="54ee8-139">Pour afficher tous les graphiques sur votre cluster, tapez :</span><span class="sxs-lookup"><span data-stu-id="54ee8-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="54ee8-140">Pour afficher tous les déploiements en cours d’exécution sur votre cluster, tapez :</span><span class="sxs-lookup"><span data-stu-id="54ee8-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="54ee8-141">Enfin, pour exécuter un pod pour accéder au client, tapez :</span><span class="sxs-lookup"><span data-stu-id="54ee8-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="54ee8-142">Pour vous connecter au client, tapez la commande suivante en remplaçant `v1-mariadb` par le nom de votre déploiement :</span><span class="sxs-lookup"><span data-stu-id="54ee8-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="54ee8-143">Vous pouvez à présent utiliser des commandes SQL standard pour créer des bases de données, tables, etc. Par exemple, `Create DATABASE testdb1;` crée une base de données vide.</span><span class="sxs-lookup"><span data-stu-id="54ee8-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="54ee8-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="54ee8-144">Next steps</span></span>

* <span data-ttu-id="54ee8-145">Pour plus d’informations sur la gestion des graphiques Kubernetes, consultez la [documentation de Helm](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="54ee8-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

