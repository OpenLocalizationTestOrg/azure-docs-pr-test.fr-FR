---
title: "aaaManage Azure Kubernetes cluster associé à l’interface utilisateur web | Documents Microsoft"
description: "À l’aide de hello Kubernetes web l’interface utilisateur dans le conteneur de Service Azure"
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
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="bc039-103">À l’aide de hello Kubernetes web l’interface utilisateur avec le Service de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="bc039-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc039-104">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bc039-104">Prerequisites</span></span>
<span data-ttu-id="bc039-105">Cette procédure pas à pas suppose que vous avez [créé un cluster Kubernetes à l’aide d’Azure Container Service](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="bc039-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="bc039-106">Il suppose également que vous avez hello Azure CLI 2.0 et `kubectl` outils sont installés.</span><span class="sxs-lookup"><span data-stu-id="bc039-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="bc039-107">Vous pouvez tester si vous avez hello `az` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="bc039-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="bc039-108">Si vous n’avez pas hello `az` outil est installé, il existe des instructions [ici](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="bc039-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="bc039-109">Vous pouvez tester si vous avez hello `kubectl` outil est installé en exécutant :</span><span class="sxs-lookup"><span data-stu-id="bc039-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="bc039-110">Si `kubectl` n’est pas installé, vous pouvez exécuter :</span><span class="sxs-lookup"><span data-stu-id="bc039-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="bc039-111">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="bc039-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="bc039-112">Se connecter à l’interface utilisateur web de toohello</span><span class="sxs-lookup"><span data-stu-id="bc039-112">Connect toohello web UI</span></span>
<span data-ttu-id="bc039-113">Vous pouvez lancer l’interface utilisateur web de Kubernetes hello en exécutant :</span><span class="sxs-lookup"><span data-stu-id="bc039-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="bc039-114">Il doit s’ouvrir un proxy de tooa sécurisée web navigateur configuré tootalk se connectant à votre interface utilisateur web de Kubernetes de toohello ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="bc039-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="bc039-115">Création et exposition d’un service</span><span class="sxs-lookup"><span data-stu-id="bc039-115">Create and expose a service</span></span>
1. <span data-ttu-id="bc039-116">Dans hello Kubernetes interface utilisateur web, cliquez sur **créer** bouton hello supérieur droit de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bc039-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Interface de création Kubernetes](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="bc039-118">Une boîte de dialogue dans laquelle vous pouvez commencer à créer votre application s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="bc039-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="bc039-119">Nommez hello `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="bc039-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="bc039-120">Hello d’utilisation [ `nginx` conteneur à partir de Docker](https://hub.docker.com/_/nginx/) et déployer les trois réplicas de ce service web.</span><span class="sxs-lookup"><span data-stu-id="bc039-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Boîte de dialogue de création de pods Kubernetes](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="bc039-122">Sous **Service**, sélectionnez **Externe** et saisissez le port 80.</span><span class="sxs-lookup"><span data-stu-id="bc039-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="bc039-123">Ce paramètre équilibre la charge de trois réplicas de trafic toohello.</span><span class="sxs-lookup"><span data-stu-id="bc039-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Boîte de dialogue de création de service Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="bc039-125">Cliquez sur **déployer** toodeploy ces conteneurs et les services.</span><span class="sxs-lookup"><span data-stu-id="bc039-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Déploiement de Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="bc039-127">Affichage de vos conteneurs</span><span class="sxs-lookup"><span data-stu-id="bc039-127">View your containers</span></span>
<span data-ttu-id="bc039-128">Après avoir cliqué sur **déployer**, hello l’interface utilisateur affiche une vue de votre service lors de son déploiement :</span><span class="sxs-lookup"><span data-stu-id="bc039-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![État de Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="bc039-130">Vous pouvez voir sous état hello de chaque objet Kubernetes dans un cercle hello sur la partie gauche de l’interface utilisateur, hello **POD**.</span><span class="sxs-lookup"><span data-stu-id="bc039-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="bc039-131">S’il s’agit d’un cercle complet partiellement, puis les objet hello consiste toujours à déployer.</span><span class="sxs-lookup"><span data-stu-id="bc039-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="bc039-132">Lorsqu’un objet est entièrement déployé, une coche verte s’affiche :</span><span class="sxs-lookup"><span data-stu-id="bc039-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes déployé](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="bc039-134">Une fois que tout est en cours d’exécution, cliquez sur un de vos modules toosee plus d’informations sur hello en cours d’exécution service web.</span><span class="sxs-lookup"><span data-stu-id="bc039-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Pods kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="bc039-136">Bonjour **POD** vue, vous pouvez voir des informations sur les conteneurs hello dans pod de hello, ainsi que des ressources processeur et mémoire hello utilisées par les conteneurs :</span><span class="sxs-lookup"><span data-stu-id="bc039-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Ressources Kubernetes](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="bc039-138">Si vous ne voyez pas les ressources hello, vous devrez peut-être toowait quelques minutes pour hello toopropagate des données d’analyse.</span><span class="sxs-lookup"><span data-stu-id="bc039-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="bc039-139">journaux de hello toosee pour votre conteneur, cliquez sur **afficher les journaux**.</span><span class="sxs-lookup"><span data-stu-id="bc039-139">toosee hello logs for your container, click **View logs**.</span></span>

![Journaux Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="bc039-141">Affichage de votre service</span><span class="sxs-lookup"><span data-stu-id="bc039-141">Viewing your service</span></span>
<span data-ttu-id="bc039-142">Dans Ajout toorunning vos conteneurs, hello Kubernetes UI a créé par un externe `Service` qui configure une charge équilibrage toobring trafic toohello les conteneurs dans votre cluster.</span><span class="sxs-lookup"><span data-stu-id="bc039-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="bc039-143">Dans le volet de navigation gauche hello, cliquez sur **Services** tooview tous les services (il doit être uniquement).</span><span class="sxs-lookup"><span data-stu-id="bc039-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Services Kubernetes](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="bc039-145">Dans cet affichage, vous devez voir un point de terminaison externe (adresse IP) qui a été alloué tooyour service.</span><span class="sxs-lookup"><span data-stu-id="bc039-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="bc039-146">Si vous cliquez sur cette adresse IP, vous devez voir votre conteneur Nginx en cours d’exécution derrière l’équilibrage de charge.</span><span class="sxs-lookup"><span data-stu-id="bc039-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Vue nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="bc039-148">Redimensionnement de votre service</span><span class="sxs-lookup"><span data-stu-id="bc039-148">Resizing your service</span></span>
<span data-ttu-id="bc039-149">En outre tooviewing vos objets dans hello l’interface utilisateur, vous pouvez modifier et mettre à jour les objets de l’API de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="bc039-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="bc039-150">Tout d’abord, cliquez sur **déploiements** Bonjour laissé le déploiement de navigation volet toosee hello pour votre service.</span><span class="sxs-lookup"><span data-stu-id="bc039-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="bc039-151">Une fois que vous êtes dans cette vue, cliquez sur le jeu de réplicas hello, puis cliquez sur **modifier** dans la barre de navigation supérieur hello :</span><span class="sxs-lookup"><span data-stu-id="bc039-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Modification de Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="bc039-153">Modifier hello `spec.replicas` champ toobe `2`, puis cliquez sur **mise à jour**.</span><span class="sxs-lookup"><span data-stu-id="bc039-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="bc039-154">Cela entraîne un nombre hello de réplicas toodrop tootwo par la suppression de l’un de vos modules.</span><span class="sxs-lookup"><span data-stu-id="bc039-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

