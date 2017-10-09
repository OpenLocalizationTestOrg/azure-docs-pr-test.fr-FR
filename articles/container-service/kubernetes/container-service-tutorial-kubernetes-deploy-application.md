---
title: "didacticiel de Service de conteneur aaaAzure - déployer une Application | Documents Microsoft"
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
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="0247f-104">Exécuter des applications dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0247f-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="0247f-105">Dans ce didacticiel (le quatrième d’une série de sept), un exemple d’application est déployé dans un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="0247f-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="0247f-106">Les étapes terminées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0247f-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0247f-107">Télécharger les fichiers manifeste Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0247f-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="0247f-108">Exécuter une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0247f-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="0247f-109">Tester l’application hello</span><span class="sxs-lookup"><span data-stu-id="0247f-109">Test hello application</span></span>

<span data-ttu-id="0247f-110">Dans les didacticiels suivants, cette application est monté en charge, mises à jour, et Operations Management Suite configuré le cluster de Kubernetes toomonitor hello.</span><span class="sxs-lookup"><span data-stu-id="0247f-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured toomonitor hello Kubernetes cluster.</span></span>

<span data-ttu-id="0247f-111">Ce didacticiel suppose une compréhension élémentaire des concepts de Kubernetes, pour plus d’informations sur Kubernetes voir hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="0247f-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0247f-112">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0247f-112">Before you begin</span></span>

<span data-ttu-id="0247f-113">Dans les didacticiels précédents, une application a été empaquetée dans une image de conteneur, cette image a été téléchargé tooAzure Registre de conteneur et un cluster Kubernetes a été créé.</span><span class="sxs-lookup"><span data-stu-id="0247f-113">In previous tutorials, an application was packaged into a container image, this image was uploaded tooAzure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="0247f-114">Si vous n’avez pas fait ces étapes et que vous aimeriez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="0247f-114">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="0247f-115">Au minimum, ce didacticiel nécessite un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="0247f-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="0247f-116">Obtenir un fichier manifeste</span><span class="sxs-lookup"><span data-stu-id="0247f-116">Get manifest file</span></span>

<span data-ttu-id="0247f-117">Pour ce didacticiel, les [objets Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) sont déployés à l’aide d’un manifeste Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="0247f-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="0247f-118">Un manifeste Kubernetes est un fichier YAML ou JSON contenant des instructions de configuration et de déploiement pour l’objet Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="0247f-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="0247f-119">fichier manifeste d’application Hello pour ce didacticiel est disponible dans le référentiel d’application hello Vote de Azure, qui a été cloné dans un didacticiel précédent.</span><span class="sxs-lookup"><span data-stu-id="0247f-119">hello application manifest file for this tutorial is available in hello Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="0247f-120">Si vous ne le n'avez pas déjà fait, cloner le référentiel de hello avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0247f-120">If you have not already done so, clone hello repo with hello following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="0247f-121">fichier de manifeste Hello se trouve dans hello suivant le répertoire de dépôt de hello cloné.</span><span class="sxs-lookup"><span data-stu-id="0247f-121">hello manifest file is found in hello following directory of hello cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="0247f-122">Mettre à jour le fichier manifeste</span><span class="sxs-lookup"><span data-stu-id="0247f-122">Update manifest file</span></span>

<span data-ttu-id="0247f-123">Si vous utilisez des images de conteneur de Registre de conteneur Azure toostore hello, hello toobe besoins manifeste mis à jour avec le nom de loginServer l’ACR hello.</span><span class="sxs-lookup"><span data-stu-id="0247f-123">If using Azure Container Registry toostore hello container images, hello manifest needs toobe updated with hello ACR loginServer name.</span></span>

<span data-ttu-id="0247f-124">Obtenir le nom de serveur hello ACR connexion avec hello [liste d’acr az](/cli/azure/acr#list) commande.</span><span class="sxs-lookup"><span data-stu-id="0247f-124">Get hello ACR login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="0247f-125">Hello exemple manifeste a été créé au préalable avec un nom de référentiel de *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="0247f-125">hello sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="0247f-126">Ouvrir le fichier de hello avec n’importe quel éditeur de texte et remplacez hello *microsoft* valeur avec le nom du serveur de connexion de votre instance ACR hello.</span><span class="sxs-lookup"><span data-stu-id="0247f-126">Open hello file with any text editor, and replace hello *microsoft* value with hello login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="0247f-127">Déployer l’application</span><span class="sxs-lookup"><span data-stu-id="0247f-127">Deploy application</span></span>

<span data-ttu-id="0247f-128">Hello d’utilisation [kubectl créer](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) application hello de toorun de commande.</span><span class="sxs-lookup"><span data-stu-id="0247f-128">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span> <span data-ttu-id="0247f-129">Cette commande analyse hello fichier manifeste et créer des objets de Kubernetes de hello défini.</span><span class="sxs-lookup"><span data-stu-id="0247f-129">This command parses hello manifest file and create hello defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="0247f-130">Output:</span><span class="sxs-lookup"><span data-stu-id="0247f-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="0247f-131">Tester l’application</span><span class="sxs-lookup"><span data-stu-id="0247f-131">Test application</span></span>

<span data-ttu-id="0247f-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) est créé qui expose hello application toohello internet.</span><span class="sxs-lookup"><span data-stu-id="0247f-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes hello application toohello internet.</span></span> <span data-ttu-id="0247f-133">Ce processus peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="0247f-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="0247f-134">cours toomonitor, utilisez hello [kubectl obtenir service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) avec hello `--watch` argument.</span><span class="sxs-lookup"><span data-stu-id="0247f-134">toomonitor progress, use hello [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="0247f-135">Au départ, hello **IP externe** pour hello *avant de vote d’azure* service apparaît sous la forme *en attente*.</span><span class="sxs-lookup"><span data-stu-id="0247f-135">Initially, hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="0247f-136">Une fois que l’adresse de hello IP externe a été modifiée à partir de *en attente* tooan *adresse IP*, utilisez `CTRL-C` processus d’observation kubectl toostop hello.</span><span class="sxs-lookup"><span data-stu-id="0247f-136">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="0247f-137">application hello toosee, parcourir toohello une adresse IP externe.</span><span class="sxs-lookup"><span data-stu-id="0247f-137">toosee hello application, browse toohello external IP address.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="0247f-139">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0247f-139">Next steps</span></span>

<span data-ttu-id="0247f-140">Dans ce didacticiel, hello application de vote Azure a été déployé tooan Azure conteneur Service Kubernetes cluster.</span><span class="sxs-lookup"><span data-stu-id="0247f-140">In this tutorial, hello Azure vote application was deployed tooan Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="0247f-141">Les tâches accomplies sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="0247f-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="0247f-142">Téléchargement des fichiers manifeste Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0247f-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="0247f-143">Exécutez l’application hello dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0247f-143">Run hello application in Kubernetes</span></span>
> * <span data-ttu-id="0247f-144">Application hello testée</span><span class="sxs-lookup"><span data-stu-id="0247f-144">Tested hello application</span></span>

<span data-ttu-id="0247f-145">Toohello toolearn de didacticiel suivant sur la mise à l’échelle une application de Kubernetes et le hello sous-jacent Kubernetes infrastructure d’avance.</span><span class="sxs-lookup"><span data-stu-id="0247f-145">Advance toohello next tutorial toolearn about scaling both a Kubernetes application and hello underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="0247f-146">Mettre à l’échelle l’application et l’infrastructure Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0247f-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)