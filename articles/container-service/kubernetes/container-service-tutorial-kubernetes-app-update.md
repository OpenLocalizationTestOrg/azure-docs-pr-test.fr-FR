---
title: "Didacticiel Azure Container Service - Mettre à jour une application"
description: "Didacticiel Azure Container Service - Mettre à jour une application"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5ecaa3a79270e29ac002e91065f7df4f7e8914e7
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: MTE
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2018
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="6fc8e-103">Mettre à jour une application dans Kubernetes</span><span class="sxs-lookup"><span data-stu-id="6fc8e-103">Update an application in Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="6fc8e-104">Après avoir déployé une application dans Kubernetes, vous pouvez la mettre à jour en spécifiant une nouvelle image conteneur ou une nouvelle version de l’image.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="6fc8e-105">Cette mise à jour se fait alors étape par étape, afin que seulement une partie du déploiement soit mise à jour simultanément.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="6fc8e-106">Cette mise à jour progressive permet à l’application de poursuivre son exécution pendant la mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-106">This staged update enables the application to keep running during the update.</span></span> <span data-ttu-id="6fc8e-107">Elle fournit également un mécanisme de restauration en cas d’échec du déploiement.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-107">It also provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="6fc8e-108">Dans ce didacticiel (le sixième d’une série de sept), l’exemple de l’application Azure Vote est mis à jour.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="6fc8e-109">Les tâches que vous effectuez sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fc8e-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6fc8e-110">Mise à jour du code de l’application frontale</span><span class="sxs-lookup"><span data-stu-id="6fc8e-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="6fc8e-111">Création d’une image conteneur mise à jour</span><span class="sxs-lookup"><span data-stu-id="6fc8e-111">Creating an updated container image</span></span>
> * <span data-ttu-id="6fc8e-112">Envoi (push) de l’image conteneur à Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6fc8e-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="6fc8e-113">Déploiement de l’image conteneur mise à jour</span><span class="sxs-lookup"><span data-stu-id="6fc8e-113">Deploying the updated container image</span></span>

<span data-ttu-id="6fc8e-114">Dans les didacticiels suivants, Operations Management Suite est configuré pour la surveillance du cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6fc8e-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="6fc8e-115">Before you begin</span></span>

<span data-ttu-id="6fc8e-116">Dans les didacticiels précédents, une application a été empaquetée dans une image conteneur, l’image a été chargée dans Azure Container Registry et un cluster Kubernetes a été créé.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="6fc8e-117">L’application a ensuite été exécutée sur le cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="6fc8e-118">Un référentiel d’application a également été cloné, ce qui inclut le code source de l’application et un fichier Docker Compose précréé utilisé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-118">An application repository was also cloned which includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span></span> <span data-ttu-id="6fc8e-119">Vérifiez que vous avez cloné le référentiel et que vous avez modifié des répertoires dans le répertoire cloné.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-119">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span></span> <span data-ttu-id="6fc8e-120">Vous trouverez à l’intérieur un répertoire nommé `azure-vote` et un fichier nommé `docker-compose.yml`.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-120">Inside is a directory named `azure-vote` and a file named `docker-compose.yml`.</span></span>

<span data-ttu-id="6fc8e-121">Si vous n’avez pas accompli ces étapes et que vous souhaitez suivre cette procédure, revenez au [Didacticiel 1 – Créer des images conteneur](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="6fc8e-121">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="6fc8e-122">Mettre à jour l’application</span><span class="sxs-lookup"><span data-stu-id="6fc8e-122">Update application</span></span>

<span data-ttu-id="6fc8e-123">Pour ce didacticiel, une modification est apportée à l’application et l’application mise à jour est déployée sur le cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-123">For this tutorial, a change is made to the application, and the updated application deployed to the Kubernetes cluster.</span></span> 

<span data-ttu-id="6fc8e-124">Le code source de l’application se trouve à l’intérieur du répertoire `azure-vote`.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-124">The application source code can be found inside of the `azure-vote` directory.</span></span> <span data-ttu-id="6fc8e-125">Ouvrez le fichier `config_file.cfg` avec un éditeur de code ou de texte.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-125">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="6fc8e-126">Dans cet exemple, on utilise `vi` .</span><span class="sxs-lookup"><span data-stu-id="6fc8e-126">In this example `vi` is used.</span></span>

```bash
vi azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="6fc8e-127">Modifiez les valeurs de `VOTE1VALUE` et `VOTE2VALUE`, puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-127">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="6fc8e-128">Enregistrez et fermez le fichier.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-128">Save and close the file.</span></span>

## <a name="update-container-image"></a><span data-ttu-id="6fc8e-129">Créer une image conteneur</span><span class="sxs-lookup"><span data-stu-id="6fc8e-129">Update container image</span></span>

<span data-ttu-id="6fc8e-130">Utilisez [docker-compose](https://docs.docker.com/compose/) pour recréer l’image de l’application frontale et exécuter l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-130">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span> <span data-ttu-id="6fc8e-131">L’argument `--build` est utilisé pour indiquer à Docker Compose de recréer l’image d’application.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-131">The `--build` argument is used to instruct Docker Compose to re-create the application image.</span></span>

```bash
docker-compose up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="6fc8e-132">Tester l’application localement</span><span class="sxs-lookup"><span data-stu-id="6fc8e-132">Test application locally</span></span>

<span data-ttu-id="6fc8e-133">Accédez à http://localhost:8080 pour afficher l’application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-133">Browse to http://localhost:8080 to see the updated application.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="6fc8e-135">Marquer et envoyer des images</span><span class="sxs-lookup"><span data-stu-id="6fc8e-135">Tag and push images</span></span>

<span data-ttu-id="6fc8e-136">Marquez l’image `azure-vote-front` avec le loginServer du registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-136">Tag the `azure-vote-front` image with the loginServer of the container registry.</span></span> 

<span data-ttu-id="6fc8e-137">Obtenez le nom du serveur de connexion à l’aide de la commande [az acr list](/cli/azure/acr#list).</span><span class="sxs-lookup"><span data-stu-id="6fc8e-137">Get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="6fc8e-138">Utilisez [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) pour ajouter une balise à l’image.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-138">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="6fc8e-139">Remplacez `<acrLoginServer>` par le nom de votre serveur de connexion Azure Container Registry ou par votre nom d’hôte de registre public.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-139">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span> <span data-ttu-id="6fc8e-140">Notez également que la version de l’image est mise à jour à `redis-v2`.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-140">Also notice that the image version is updated to `redis-v2`.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="6fc8e-141">Utilisez [docker push](https://docs.docker.com/engine/reference/commandline/push/) pour charger l’image dans le Registre.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-141">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="6fc8e-142">Remplacez `<acrLoginServer>` par votre nom de serveur de connexion Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-142">Replace `<acrLoginServer>` with your Azure Container Registry login server name.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="6fc8e-143">Déployer l’application mise à jour</span><span class="sxs-lookup"><span data-stu-id="6fc8e-143">Deploy update application</span></span>

<span data-ttu-id="6fc8e-144">Pour garantir une disponibilité maximale, vous devez exécuter plusieurs instances du pod d’application.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-144">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="6fc8e-145">Vérifiez cette configuration avec la commande [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="6fc8e-145">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="6fc8e-146">Output:</span><span class="sxs-lookup"><span data-stu-id="6fc8e-146">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="6fc8e-147">Si vous n’avez qu’un POD exécutant l’image azure-vote-front, mettez à l’échelle le déploiement `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-147">If you do not have multiple pods running the azure-vote-front image, scale the `azure-vote-front` deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="6fc8e-148">Pour mettre à jour l’application, utilisez la commande [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set).</span><span class="sxs-lookup"><span data-stu-id="6fc8e-148">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="6fc8e-149">Mettez à jour `<acrLoginServer>` avec le nom du serveur de connexion ou le nom d’hôte de votre registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-149">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="6fc8e-150">Pour surveiller le déploiement, utilisez la commande [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get).</span><span class="sxs-lookup"><span data-stu-id="6fc8e-150">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="6fc8e-151">À mesure que l’application mise à jour est déployée, vos pods sont terminés et recréés avec la nouvelle image conteneur.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-151">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="6fc8e-152">Output:</span><span class="sxs-lookup"><span data-stu-id="6fc8e-152">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="6fc8e-153">Tester l’application mise à jour</span><span class="sxs-lookup"><span data-stu-id="6fc8e-153">Test updated application</span></span>

<span data-ttu-id="6fc8e-154">Obtenez l’adresse IP externe du service `azure-vote-front`.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-154">Get the external IP address of the `azure-vote-front` service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="6fc8e-155">Accédez à l’adresse IP pour voir l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-155">Browse to the IP address to see the updated application.</span></span>

![Image du cluster Kubernetes sur Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="6fc8e-157">étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="6fc8e-157">Next steps</span></span>

<span data-ttu-id="6fc8e-158">Dans ce didacticiel, nous avons mis à jour une application et nous avons déployé cette mise à jour sur un cluster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-158">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="6fc8e-159">Les tâches suivantes ont été accomplies :</span><span class="sxs-lookup"><span data-stu-id="6fc8e-159">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6fc8e-160">Mise à jour du code de l’application frontale</span><span class="sxs-lookup"><span data-stu-id="6fc8e-160">Updated the front-end application code</span></span>
> * <span data-ttu-id="6fc8e-161">Création d’une image conteneur mise à jour</span><span class="sxs-lookup"><span data-stu-id="6fc8e-161">Created an updated container image</span></span>
> * <span data-ttu-id="6fc8e-162">Envoi (push) de l’image conteneur à Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6fc8e-162">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="6fc8e-163">Déploiement de l’application mise à jour</span><span class="sxs-lookup"><span data-stu-id="6fc8e-163">Deployed the updated application</span></span>

<span data-ttu-id="6fc8e-164">Passez au didacticiel suivant pour en savoir plus sur la surveillance de Kubernetes avec Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="6fc8e-164">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6fc8e-165">Surveiller Kubernetes avec OMS (Operations Management Suite)</span><span class="sxs-lookup"><span data-stu-id="6fc8e-165">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)