---
title: "Didacticiel Azure Container Service - Déployer une application | Microsoft Docs"
description: "Didacticiel Azure Container Service - Déployer une application"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, conteneurs, micro-services, Kubernetes, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="e39f7-104">Exécuter des applications dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e39f7-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="e39f7-105">Dans ce didacticiel (le quatrième d’une série de sept), un exemple d’application est déployé dans un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e39f7-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="e39f7-106">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e39f7-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e39f7-107">Télécharger les fichiers manifeste Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e39f7-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="e39f7-108">Exécuter une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e39f7-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="e39f7-109">Test de l'application</span><span class="sxs-lookup"><span data-stu-id="e39f7-109">Test the application</span></span>

<span data-ttu-id="e39f7-110">Dans les didacticiels suivants, cette application est mise à l’échelle et Operations Management Suite est configuré pour la surveillance du cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e39f7-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="e39f7-111">Ce didacticiel suppose une compréhension élémentaire des concepts de Kubernetes. Pour en savoir plus, consultez la [documentation Kubernetes](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="e39f7-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e39f7-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e39f7-112">Before you begin</span></span>

<span data-ttu-id="e39f7-113">Dans les didacticiels précédents, une application a été empaquetée dans une image conteneur, l’image a été chargée dans Azure Container Registry et un cluster Kubernetes a été créé.</span><span class="sxs-lookup"><span data-stu-id="e39f7-113">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="e39f7-114">Si vous n’avez pas accompli ces étapes et que vous souhaitez suivre cette procédure, revenez au [Didacticiel 1 – Créer des images conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="e39f7-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="e39f7-115">Au minimum, ce didacticiel nécessite un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e39f7-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="e39f7-116">Obtenir un fichier manifeste</span><span class="sxs-lookup"><span data-stu-id="e39f7-116">Get manifest file</span></span>

<span data-ttu-id="e39f7-117">Pour ce didacticiel, les [objets Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) sont déployés à l’aide d’un manifeste Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e39f7-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="e39f7-118">Un manifeste Kubernetes est un fichier YAML ou JSON contenant des instructions de configuration et de déploiement pour l’objet Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e39f7-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="e39f7-119">Le fichier manifeste d’application de ce didacticiel est disponible dans le référentiel d’application Azure Vote, qui a été cloné dans un didacticiel précédent.</span><span class="sxs-lookup"><span data-stu-id="e39f7-119">The application manifest file for this tutorial is available in the Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="e39f7-120">Si vous ne l’avez pas déjà fait, clonez le référentiel à l’aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="e39f7-120">If you have not already done so, clone the repo with the following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="e39f7-121">Le fichier manifeste se trouve dans le répertoire suivant du référentiel cloné.</span><span class="sxs-lookup"><span data-stu-id="e39f7-121">The manifest file is found in the following directory of the cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="e39f7-122">Mettre à jour le fichier manifeste</span><span class="sxs-lookup"><span data-stu-id="e39f7-122">Update manifest file</span></span>

<span data-ttu-id="e39f7-123">Si vous utilisez Azure Container Registry pour stocker les images conteneur, le fichier manifeste doit être mis à jour avec le nom du serveur de connexion ACR.</span><span class="sxs-lookup"><span data-stu-id="e39f7-123">If using Azure Container Registry to store the container images, the manifest needs to be updated with the ACR loginServer name.</span></span>

<span data-ttu-id="e39f7-124">Obtenez le nom du serveur de connexion ACR à l’aide de la commande [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="e39f7-124">Get the ACR login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="e39f7-125">L’exemple de fichier manifeste a été précréé avec le nom de référentiel *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="e39f7-125">The sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="e39f7-126">Ouvrez le fichier avec un éditeur de texte, puis remplacez la valeur *microsoft* par le nom du serveur de connexion de votre instance ACR.</span><span class="sxs-lookup"><span data-stu-id="e39f7-126">Open the file with any text editor, and replace the *microsoft* value with the login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="e39f7-127">Déployer l’application</span><span class="sxs-lookup"><span data-stu-id="e39f7-127">Deploy application</span></span>

<span data-ttu-id="e39f7-128">Utilisez la commande [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="e39f7-128">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span> <span data-ttu-id="e39f7-129">Cette commande analyse le fichier manifeste et crée les objets Kubernetes définis.</span><span class="sxs-lookup"><span data-stu-id="e39f7-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="e39f7-130">Output:</span><span class="sxs-lookup"><span data-stu-id="e39f7-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="e39f7-131">Tester l’application</span><span class="sxs-lookup"><span data-stu-id="e39f7-131">Test application</span></span>

<span data-ttu-id="e39f7-132">Un [service Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) est créé et expose l’application à Internet.</span><span class="sxs-lookup"><span data-stu-id="e39f7-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="e39f7-133">Ce processus peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="e39f7-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="e39f7-134">Pour surveiller la progression, utilisez la commande [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) avec l’argument `--watch`.</span><span class="sxs-lookup"><span data-stu-id="e39f7-134">To monitor progress, use the [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="e39f7-135">Au début, **EXTERNAL-IP** apparaît comme étant *en attente* pour le service *azure-vote-front*.</span><span class="sxs-lookup"><span data-stu-id="e39f7-135">Initially, the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="e39f7-136">Une fois que l’adresse IP externe est passée du statut *En attente* à *Adresse IP*, utilisez `CTRL-C` pour arrêter le processus de surveillance kubectl.</span><span class="sxs-lookup"><span data-stu-id="e39f7-136">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="e39f7-137">Pour afficher l’application, accédez à l’adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="e39f7-137">To see the application, browse to the external IP address.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="e39f7-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e39f7-139">Next steps</span></span>

<span data-ttu-id="e39f7-140">Dans ce didacticiel, l’application Azure Vote a été déployée sur un cluster Kubernetes Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="e39f7-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="e39f7-141">Les tâches accomplies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e39f7-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="e39f7-142">Téléchargement des fichiers manifeste Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e39f7-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="e39f7-143">Exécution de l’application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e39f7-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="e39f7-144">Test de l’application</span><span class="sxs-lookup"><span data-stu-id="e39f7-144">Tested the application</span></span>

<span data-ttu-id="e39f7-145">Passez au didacticiel suivant pour en savoir plus sur la mise à l’échelle d’une application Kubernetes et de l’infrastructure Kubernetes sous-jacente.</span><span class="sxs-lookup"><span data-stu-id="e39f7-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e39f7-146">Mettre à l’échelle l’application et l’infrastructure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="e39f7-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)