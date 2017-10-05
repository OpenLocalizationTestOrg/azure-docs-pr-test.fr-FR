---
title: "Gérer le cluster Kubernetes Azure avec l’interface utilisateur Web | Microsoft Docs"
description: "Utilisation de l’interface web Kubernetes dans Azure Container Service"
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e31f90d61fc61f17582372fe9f491a1e21f628b0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="using-the-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="989ff-103">Utilisation de l’interface utilisateur Web Kubernetes avec Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="989ff-103">Using the Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="989ff-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="989ff-104">Prerequisites</span></span>
<span data-ttu-id="989ff-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="989ff-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="989ff-106">Elle suppose également que vous avez installé les outils `kubectl` et Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="989ff-106">It also assumes that you have the Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="989ff-107">Vous pouvez tester si l’outil `az` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="989ff-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="989ff-108">Si l’outil `az` n’est pas installé, suivez les instructions figurant [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="989ff-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="989ff-109">Vous pouvez tester si l’outil `kubectl` est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="989ff-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="989ff-110">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="989ff-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="989ff-111">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="989ff-111">Overview</span></span>

### <a name="connect-to-the-web-ui"></a><span data-ttu-id="989ff-112">Connexion à l’interface web</span><span class="sxs-lookup"><span data-stu-id="989ff-112">Connect to the web UI</span></span>
<span data-ttu-id="989ff-113">Vous pouvez lancer l’interface web Kubernetes en exécutant :</span><span class="sxs-lookup"><span data-stu-id="989ff-113">You can launch the Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="989ff-114">Cette commande ouvre un navigateur web configuré pour communiquer avec un proxy sécurisé, en connectant votre machine locale à l’interface utilisateur web Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="989ff-114">This should open a web browser configured to talk to a secure proxy connecting your local machine to the Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="989ff-115">Création et exposition d’un service</span><span class="sxs-lookup"><span data-stu-id="989ff-115">Create and expose a service</span></span>
1. <span data-ttu-id="989ff-116">Dans l’interface web Kubernetes, cliquez sur le bouton **Créer** dans la fenêtre supérieure droite.</span><span class="sxs-lookup"><span data-stu-id="989ff-116">In the Kubernetes web UI, click **Create** button in the upper right window.</span></span>

    ![Interface de création Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="989ff-118">Une boîte de dialogue dans laquelle vous pouvez commencer à créer votre application s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="989ff-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="989ff-119">Donnez-lui le nom `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="989ff-119">Give it the name `hello-nginx`.</span></span> <span data-ttu-id="989ff-120">Utilisez le [ `nginx` conteneur de Docker](https://hub.docker.com/_/nginx/) et déployez trois réplicas de ce service web.</span><span class="sxs-lookup"><span data-stu-id="989ff-120">Use the [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Boîte de dialogue de création de pods Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="989ff-122">Sous **Service**, sélectionnez **Externe** et saisissez le port 80.</span><span class="sxs-lookup"><span data-stu-id="989ff-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="989ff-123">Ce paramètre permet d’équilibrer la charge du trafic pour les trois réplicas.</span><span class="sxs-lookup"><span data-stu-id="989ff-123">This setting load-balances traffic to the three replicas.</span></span>

    ![Boîte de dialogue de création de service Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="989ff-125">Cliquez sur **Déployer** pour déployer ces conteneurs et ces services.</span><span class="sxs-lookup"><span data-stu-id="989ff-125">Click **Deploy** to deploy these containers and services.</span></span>

    ![Déploiement de Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="989ff-127">Affichage de vos conteneurs</span><span class="sxs-lookup"><span data-stu-id="989ff-127">View your containers</span></span>
<span data-ttu-id="989ff-128">Une fois que vous cliquez sur **Déployer**, l’interface utilisateur affiche une vue de votre service pendant son déploiement :</span><span class="sxs-lookup"><span data-stu-id="989ff-128">After you click **Deploy**, the UI shows a view of your service as it deploys:</span></span>

![État de Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="989ff-130">Vous pouvez voir l’état de chaque objet Kubernetes dans le cercle sur le côté gauche de l’interface utilisateur, sous **Pods**.</span><span class="sxs-lookup"><span data-stu-id="989ff-130">You can see the status of each Kubernetes object in the circle on the left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="989ff-131">Si le cercle est partiellement complet, l’objet est toujours en cours de déploiement.</span><span class="sxs-lookup"><span data-stu-id="989ff-131">If it is a partially full circle, then the object is still deploying.</span></span> <span data-ttu-id="989ff-132">Lorsqu’un objet est entièrement déployé, une coche verte s’affiche :</span><span class="sxs-lookup"><span data-stu-id="989ff-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes déployé](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="989ff-134">Une fois que tout est en cours d’exécution, cliquez sur l’un de vos pods pour afficher les détails sur le service web exécuté.</span><span class="sxs-lookup"><span data-stu-id="989ff-134">Once everything is running, click one of your pods to see details about the running web service.</span></span>

![Pods kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="989ff-136">Dans la vue **Pods**, vous pouvez voir des informations sur les conteneurs dans le pod, ainsi que les ressources de processeur et de mémoire utilisées par ces conteneurs :</span><span class="sxs-lookup"><span data-stu-id="989ff-136">In the **Pods** view, you can see information about the containers in the pod as well as the CPU and memory resources used by those containers:</span></span>

![Ressources Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="989ff-138">Si vous ne voyez pas les ressources, vous devrez peut-être attendre quelques minutes que les données de surveillance se propagent.</span><span class="sxs-lookup"><span data-stu-id="989ff-138">If you don't see the resources, you may need to wait a few minutes for the monitoring data to propagate.</span></span>

<span data-ttu-id="989ff-139">Cliquez sur **Afficher les journaux** pour afficher les journaux de votre conteneur.</span><span class="sxs-lookup"><span data-stu-id="989ff-139">To see the logs for your container, click **View logs**.</span></span>

![Journaux Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="989ff-141">Affichage de votre service</span><span class="sxs-lookup"><span data-stu-id="989ff-141">Viewing your service</span></span>
<span data-ttu-id="989ff-142">Outre l’exécution de vos conteneurs, l’interface Kubernetes a créé un élément `Service` externe qui approvisionne un équilibrage de charge pour diriger le trafic vers les conteneurs de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="989ff-142">In addition to running your containers, the Kubernetes UI has created an external `Service` which provisions a load balancer to bring traffic to the containers in your cluster.</span></span>

<span data-ttu-id="989ff-143">Dans le volet de navigation de gauche, cliquez sur **Services** pour afficher tous les services (pour le moment, vous ne devriez en voir qu’un).</span><span class="sxs-lookup"><span data-stu-id="989ff-143">In the left navigation pane, click **Services** to view all services (there should be only one).</span></span>

![Services Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="989ff-145">Dans cette vue, vous devriez voir un point de terminaison externe (adresse IP) qui a été affecté à votre service.</span><span class="sxs-lookup"><span data-stu-id="989ff-145">In that view, you should see an external endpoint (IP address) that has been allocated to your service.</span></span>
<span data-ttu-id="989ff-146">Si vous cliquez sur cette adresse IP, vous devez voir votre conteneur Nginx en cours d’exécution derrière l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="989ff-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Vue nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="989ff-148">Redimensionnement de votre service</span><span class="sxs-lookup"><span data-stu-id="989ff-148">Resizing your service</span></span>
<span data-ttu-id="989ff-149">Outre l’affichage de vos objets dans l’interface, vous pouvez modifier et mettre à jour les objets API Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="989ff-149">In addition to viewing your objects in the UI, you can edit and update the Kubernetes API objects.</span></span>

<span data-ttu-id="989ff-150">Cliquez d’abord sur **Déploiements** dans le volet de navigation gauche pour afficher le déploiement pour votre service.</span><span class="sxs-lookup"><span data-stu-id="989ff-150">First, click **Deployments** in the left navigation pane to see the deployment for your service.</span></span>

<span data-ttu-id="989ff-151">Une fois que vous êtes dans cette vue, cliquez sur ReplicaSet, puis sur **Modifier** dans la barre de navigation supérieure :</span><span class="sxs-lookup"><span data-stu-id="989ff-151">Once you are in that view, click on the replica set, and then click **Edit** in the upper navigation bar:</span></span>

![Modification de Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="989ff-153">Modifiez le champ `spec.replicas` pour avoir la valeur `2`, et cliquez sur **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="989ff-153">Edit the `spec.replicas` field to be `2`, and click **Update**.</span></span>

<span data-ttu-id="989ff-154">Il n’y aura donc plus que deux réplicas, car l’un de vos pods sera supprimé.</span><span class="sxs-lookup"><span data-stu-id="989ff-154">This causes the number of replicas to drop to two by deleting one of your pods.</span></span>

 

