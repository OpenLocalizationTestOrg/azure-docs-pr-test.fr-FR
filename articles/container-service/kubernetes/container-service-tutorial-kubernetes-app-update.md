---
title: "didacticiel de Service de conteneur aaaAzure - application de la mise à jour | Documents Microsoft"
description: "Didacticiel Azure Container Service - Mettre à jour une application"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="a63c6-104">Mettre à jour une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="a63c6-104">Update an application in Kubernetes</span></span>

<span data-ttu-id="a63c6-105">Après avoir déployé une application dans Kubernetes, vous pouvez la mettre à jour en spécifiant une nouvelle image conteneur ou une nouvelle version de l’image.</span><span class="sxs-lookup"><span data-stu-id="a63c6-105">After you deploy an application in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="a63c6-106">Lorsque vous mettez à jour une application, déploiement de mise à jour hello soit préparé afin que seule une partie du déploiement de hello est mis à jour simultanément.</span><span class="sxs-lookup"><span data-stu-id="a63c6-106">When you update an application, hello update rollout is staged so that only a portion of hello deployment is concurrently updated.</span></span> <span data-ttu-id="a63c6-107">Cette mise à jour intermédiaire hello application tookeep est en cours d’exécution pendant la mise à jour hello et qui offre un mécanisme de restauration cas d’échec du déploiement.</span><span class="sxs-lookup"><span data-stu-id="a63c6-107">This staged update enables hello application tookeep running during hello update, and provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="a63c6-108">Dans ce didacticiel, partie 6 de sept, Azure Vote exemple hello d’application est mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a63c6-108">In this tutorial, part six of seven, hello sample Azure Vote app is updated.</span></span> <span data-ttu-id="a63c6-109">Les tâches que vous effectuez sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="a63c6-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a63c6-110">Mise à jour le code d’application frontale hello</span><span class="sxs-lookup"><span data-stu-id="a63c6-110">Updating hello front-end application code</span></span>
> * <span data-ttu-id="a63c6-111">Création d’une image conteneur mise à jour</span><span class="sxs-lookup"><span data-stu-id="a63c6-111">Creating an updated container image</span></span>
> * <span data-ttu-id="a63c6-112">En exécutant un push hello conteneur image tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="a63c6-112">Pushing hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="a63c6-113">Déploiement d’image de conteneur mis à jour hello</span><span class="sxs-lookup"><span data-stu-id="a63c6-113">Deploying hello updated container image</span></span>

<span data-ttu-id="a63c6-114">Dans les didacticiels suivants Operations Management Suite est le cluster de Kubernetes hello toomonitor configuré.</span><span class="sxs-lookup"><span data-stu-id="a63c6-114">In subsequent tutorials, Operations Management Suite is configured toomonitor hello Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a63c6-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="a63c6-115">Before you begin</span></span>

<span data-ttu-id="a63c6-116">Dans les didacticiels précédents, une application a été empaquetée dans une image de conteneur, image de hello téléchargés tooAzure Registre de conteneur et un cluster Kubernetes créé.</span><span class="sxs-lookup"><span data-stu-id="a63c6-116">In previous tutorials, an application was packaged into a container image, hello image uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="a63c6-117">application Hello puis exécutée sur le cluster de Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="a63c6-117">hello application was then run on hello Kubernetes cluster.</span></span> 

<span data-ttu-id="a63c6-118">Si vous n’avez pas effectué ces étapes et que vous souhaitez toofollow le long, retourner trop[didacticiel 1 : créer des images de conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="a63c6-118">If you haven't completed these steps, and want toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="a63c6-119">Mettre à jour l’application</span><span class="sxs-lookup"><span data-stu-id="a63c6-119">Update application</span></span>

<span data-ttu-id="a63c6-120">toocomplete hello étapes décrites dans ce didacticiel, vous devez ont une copie clonée d’hello application de Vote de Azure.</span><span class="sxs-lookup"><span data-stu-id="a63c6-120">toocomplete hello steps in this tutorial, you must have cloned a copy of hello Azure Vote application.</span></span> <span data-ttu-id="a63c6-121">Si nécessaire, créez cette copie clonée avec hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="a63c6-121">If necessary, create this cloned copy with hello following command:</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="a63c6-122">Ouvrez hello `config_file.cfg` fichier avec un éditeur de code ou de texte.</span><span class="sxs-lookup"><span data-stu-id="a63c6-122">Open hello `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="a63c6-123">Vous pouvez trouver ce fichier sous hello suivant le répertoire de dépôt de hello cloné.</span><span class="sxs-lookup"><span data-stu-id="a63c6-123">You can find this file under hello following directory of hello cloned repo.</span></span>

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="a63c6-124">Modifier les valeurs hello de `VOTE1VALUE` et `VOTE2VALUE`, puis enregistrez le fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="a63c6-124">Change hello values for `VOTE1VALUE` and `VOTE2VALUE`, and then save hello file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="a63c6-125">Utilisez [composer de docker](https://docs.docker.com/compose/) toore-créer une image frontal de hello et application hello exécution mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a63c6-125">Use [docker-compose](https://docs.docker.com/compose/) toore-create hello front-end image and run hello updated application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="a63c6-126">Tester l’application localement</span><span class="sxs-lookup"><span data-stu-id="a63c6-126">Test application locally</span></span>

<span data-ttu-id="a63c6-127">Parcourir trop`http://localhost:8080` toosee hello mis à jour l’application.</span><span class="sxs-lookup"><span data-stu-id="a63c6-127">Browse too`http://localhost:8080` toosee hello updated application.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="a63c6-129">Marquer et envoyer des images</span><span class="sxs-lookup"><span data-stu-id="a63c6-129">Tag and push images</span></span>

<span data-ttu-id="a63c6-130">Hello de balise *avant de vote d’azure* image avec loginServer hello du Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="a63c6-130">Tag hello *azure-vote-front* image with hello loginServer of hello container registry.</span></span>

<span data-ttu-id="a63c6-131">Si vous utilisez le Registre de conteneur Azure, obtenir le nom du serveur hello avec hello [liste d’acr az](/cli/azure/acr#list) commande.</span><span class="sxs-lookup"><span data-stu-id="a63c6-131">If you're using Azure Container Registry, get hello login server name with hello [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="a63c6-132">Utilisez [balise de docker](https://docs.docker.com/engine/reference/commandline/tag/) image de hello tootag.</span><span class="sxs-lookup"><span data-stu-id="a63c6-132">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello image.</span></span> <span data-ttu-id="a63c6-133">Remplacez `<acrLoginServer>` par le nom de votre serveur de connexion Azure Container Registry ou par votre nom d’hôte de registre public.</span><span class="sxs-lookup"><span data-stu-id="a63c6-133">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="a63c6-134">Utilisez [push de docker](https://docs.docker.com/engine/reference/commandline/push/) Registre de tooyour tooupload hello image.</span><span class="sxs-lookup"><span data-stu-id="a63c6-134">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello image tooyour registry.</span></span> <span data-ttu-id="a63c6-135">Remplacez `<acrLoginServer>` par le nom de votre serveur de connexion Azure Container Registry ou par votre nom d’hôte de registre public.</span><span class="sxs-lookup"><span data-stu-id="a63c6-135">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="a63c6-136">Déployer l’application mise à jour</span><span class="sxs-lookup"><span data-stu-id="a63c6-136">Deploy update application</span></span>

<span data-ttu-id="a63c6-137">tooensure des temps de fonctionnement maximale, plusieurs instances du bloc d’application hello doivent être en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a63c6-137">tooensure maximum uptime, multiple instances of hello application pod must be running.</span></span> <span data-ttu-id="a63c6-138">Vérifier cette configuration avec hello [kubectl obtenir pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.</span><span class="sxs-lookup"><span data-stu-id="a63c6-138">Verify this configuration with hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="a63c6-139">Output:</span><span class="sxs-lookup"><span data-stu-id="a63c6-139">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="a63c6-140">Si vous n’avez pas plusieurs blocs d’image d’azure-vote-front hello en cours d’exécution, à l’échelle hello *avant de vote d’azure* déploiement.</span><span class="sxs-lookup"><span data-stu-id="a63c6-140">If you don't have multiple pods running hello azure-vote-front image, scale hello *azure-vote-front* deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="a63c6-141">application de hello tooupdate, utilisez hello [kubectl ensemble](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) commande.</span><span class="sxs-lookup"><span data-stu-id="a63c6-141">tooupdate hello application, use hello [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="a63c6-142">Mise à jour `<acrLoginServer>` avec le nom de serveur ou l’hôte de connexion de votre Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="a63c6-142">Update `<acrLoginServer>` with hello login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="a63c6-143">déploiement de hello toomonitor, utilisez hello [kubectl obtenir pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) commande.</span><span class="sxs-lookup"><span data-stu-id="a63c6-143">toomonitor hello deployment, use hello [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="a63c6-144">Comme l’application hello mis à jour est déployée, votre POD terminer une commande et recréées avec la nouvelle image de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="a63c6-144">As hello updated application is deployed, your pods are terminated and re-created with hello new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="a63c6-145">Output:</span><span class="sxs-lookup"><span data-stu-id="a63c6-145">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="a63c6-146">Tester l’application mise à jour</span><span class="sxs-lookup"><span data-stu-id="a63c6-146">Test updated application</span></span>

<span data-ttu-id="a63c6-147">Obtenir l’adresse IP externe de hello Hello *avant de vote d’azure* service.</span><span class="sxs-lookup"><span data-stu-id="a63c6-147">Get hello external IP address of hello *azure-vote-front* service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="a63c6-148">Parcourir toohello IP adresse toosee hello mis à jour l’application.</span><span class="sxs-lookup"><span data-stu-id="a63c6-148">Browse toohello IP address toosee hello updated application.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="a63c6-150">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a63c6-150">Next steps</span></span>

<span data-ttu-id="a63c6-151">Dans ce didacticiel, vous mis à jour d’une application et transférée à ce cluster de Kubernetes tooa mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a63c6-151">In this tutorial, you updated an application and rolled out this update tooa Kubernetes cluster.</span></span> <span data-ttu-id="a63c6-152">Bonjour tâches suivantes ont été effectuée :</span><span class="sxs-lookup"><span data-stu-id="a63c6-152">hello following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a63c6-153">Code d’application frontale hello mis à jour</span><span class="sxs-lookup"><span data-stu-id="a63c6-153">Updated hello front-end application code</span></span>
> * <span data-ttu-id="a63c6-154">Création d’une image conteneur mise à jour</span><span class="sxs-lookup"><span data-stu-id="a63c6-154">Created an updated container image</span></span>
> * <span data-ttu-id="a63c6-155">Objet d’un push hello conteneur image tooAzure Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="a63c6-155">Pushed hello container image tooAzure Container Registry</span></span>
> * <span data-ttu-id="a63c6-156">Application déployée hello mis à jour</span><span class="sxs-lookup"><span data-stu-id="a63c6-156">Deployed hello updated application</span></span>

<span data-ttu-id="a63c6-157">Toohello toolearn de didacticiel suivant sur la façon d’avance toomonitor Kubernetes avec Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="a63c6-157">Advance toohello next tutorial toolearn about how toomonitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a63c6-158">Surveiller Kubernetes avec OMS</span><span class="sxs-lookup"><span data-stu-id="a63c6-158">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)