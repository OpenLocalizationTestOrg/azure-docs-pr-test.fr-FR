---
title: "Utilisation d’un ACR avec un cluster DC/OS Azure | Microsoft Docs"
description: Utiliser un Azure Container Registry avec un cluster DC/OS dans Azure Container Service
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: Docker, conteneurs, micro-services, Mesos, Azure, FileShare, cifs
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 618d32ca919e50d41b85c800225fe72c3b94e537
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-acr-with-a-dcos-cluster-to-deploy-your-application"></a><span data-ttu-id="a8116-104">Utiliser un ACR avec un cluster DC/OS pour déployer votre application</span><span class="sxs-lookup"><span data-stu-id="a8116-104">Use ACR with a DC/OS cluster to deploy your application</span></span>

<span data-ttu-id="a8116-105">Dans cet article, nous explorons comment utiliser Azure Container Registry avec un cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a8116-105">In this article, we explore how to use Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="a8116-106">L’utilisation d’ACR permet de stocker en privé et de gérer des images de conteneur.</span><span class="sxs-lookup"><span data-stu-id="a8116-106">Using ACR allows you to privately store and manage container images.</span></span> <span data-ttu-id="a8116-107">Ce didacticiel décrit les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8116-107">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8116-108">Déployer Azure Container Registry (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="a8116-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="a8116-109">Configurer l’authentification ACR sur un cluster de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="a8116-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="a8116-110">Télécharger une image dans Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a8116-110">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="a8116-111">Exécuter une image de conteneur depuis Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a8116-111">Run a container image from the Azure Container Registry</span></span>

<span data-ttu-id="a8116-112">Vous avez besoin d’un cluster DC/OS ACS pour suivre les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="a8116-112">You need an ACS DC/OS cluster to complete the steps in this tutorial.</span></span> <span data-ttu-id="a8116-113">Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.</span><span class="sxs-lookup"><span data-stu-id="a8116-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="a8116-114">Ce didacticiel requiert Azure CLI version 2.0.4 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a8116-114">This tutorial requires the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a8116-115">Exécutez `az --version` pour trouver la version.</span><span class="sxs-lookup"><span data-stu-id="a8116-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="a8116-116">Si vous devez mettre à niveau, consultez [Installation d’Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8116-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="a8116-117">Déployer Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a8116-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="a8116-118">Si nécessaire, créez un registre de conteneurs Azure à l’aide de la commande [créer az acr](/cli/azure/acr#create).</span><span class="sxs-lookup"><span data-stu-id="a8116-118">If needed, create an Azure Container registry with the [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="a8116-119">L’exemple suivant crée un registre avec un nom généré de façon aléatoire.</span><span class="sxs-lookup"><span data-stu-id="a8116-119">The following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="a8116-120">Le registre est également configuré avec un compte d’administrateur à l’aide de `--admin-enabled` l’argument.</span><span class="sxs-lookup"><span data-stu-id="a8116-120">The registry is also configured with an admin account using the `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="a8116-121">Une fois le registre créé, Azure CLI fournit les informations suivantes.</span><span class="sxs-lookup"><span data-stu-id="a8116-121">Once the registry has been created, the Azure CLI outputs data similar to the following.</span></span> <span data-ttu-id="a8116-122">Notez `name` et `loginServer`, utilisés pour les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="a8116-122">Take note of the `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="a8116-123">Obtenez les informations d’identification du registre de conteneurs à l’aide de la commande [afficher les informations d’identification az acr](/cli/azure/acr/credential).</span><span class="sxs-lookup"><span data-stu-id="a8116-123">Get the container registry credentials using the [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="a8116-124">Remplacez `--name` par celui indiqué dans la dernière étape.</span><span class="sxs-lookup"><span data-stu-id="a8116-124">Substitute the `--name` with the one noted in the last step.</span></span> <span data-ttu-id="a8116-125">Notez un mot de passe, nécessaire pour une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a8116-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="a8116-126">Pour plus d’informations sur Azure Container Registry, consultez [Introduction aux registres de conteneurs Docker privés](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="a8116-126">For more information on Azure Container Registry, see [Introduction to private Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="a8116-127">Gérer l’authentification ACR</span><span class="sxs-lookup"><span data-stu-id="a8116-127">Manage ACR authentication</span></span>

<span data-ttu-id="a8116-128">La méthode traditionnelle pour pousser et tirer une image d’un registre privé consiste tout d’abord à l’authentifier auprès de celui-ci.</span><span class="sxs-lookup"><span data-stu-id="a8116-128">The conventional way to push and pull image from a private registry is to first authenticate with the registry.</span></span> <span data-ttu-id="a8116-129">Pour ce faire, vous devez utiliser la commande `docker login` sur n’importe quel client qui a besoin d’accéder au registre privé.</span><span class="sxs-lookup"><span data-stu-id="a8116-129">To do so, you would use the `docker login` command on any client that needs to access the private registry.</span></span> <span data-ttu-id="a8116-130">Un cluster de contrôleur de domaine/système d’exploitation peut contenir plusieurs nœuds qui doivent tous être authentifiés avec l’ACR. Il est donc utile d’automatiser ce processus sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="a8116-130">Because a DC/OS cluster can contain many nodes, all of which need to be authenticated with the ACR, it is helpful to automate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="a8116-131">Créer un stockage partagé</span><span class="sxs-lookup"><span data-stu-id="a8116-131">Create shared storage</span></span>

<span data-ttu-id="a8116-132">Ce processus utilise un partage de fichiers Azure installé sur chaque nœud du cluster.</span><span class="sxs-lookup"><span data-stu-id="a8116-132">This process uses an Azure file share that has been mounted on each node in the cluster.</span></span> <span data-ttu-id="a8116-133">Si vous n’avez pas déjà configuré de stockage partagé, consultez [Configurer un partage de fichier dans un cluster de contrôleur de domaine/système d’exploitation](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="a8116-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="a8116-134">Configurer une authentification ACR</span><span class="sxs-lookup"><span data-stu-id="a8116-134">Configure ACR authentication</span></span>

<span data-ttu-id="a8116-135">Obtenez d’abord le FQDN du DC/OS maître et stockez-le dans une variable.</span><span class="sxs-lookup"><span data-stu-id="a8116-135">First, get the FQDN of the DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="a8116-136">Créez une connexion SSH au maître (ou au premier maître) de votre cluster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a8116-136">Create an SSH connection with the master (or the first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="a8116-137">Si une valeur non définie par défaut a été utilisée lors de la création du cluster, mettez à jour le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a8116-137">Update the user name if a non-default value was used when creating the cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="a8116-138">Exécutez la commande suivante pour vous connecter à Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a8116-138">Run the following command to login to the Azure Container Registry.</span></span> <span data-ttu-id="a8116-139">Remplacez le `--username` par le nom du registre de conteneurs et le `--password` par l’un des mots de passe fournis.</span><span class="sxs-lookup"><span data-stu-id="a8116-139">Replace the `--username` with the name of the container registry, and the `--password` with one of the provided passwords.</span></span> <span data-ttu-id="a8116-140">Remplacez le dernier argument *mycontainerregistry.azurecr.io* dans l’exemple par le nom loginServer du registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a8116-140">Replace the last argument *mycontainerregistry.azurecr.io* in the example with the loginServer name of the container registry.</span></span> 

<span data-ttu-id="a8116-141">Cette commande stocke les valeurs d’authentification localement sous le chemin d’accès `~/.docker`.</span><span class="sxs-lookup"><span data-stu-id="a8116-141">This command stores the authentication values locally under the `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="a8116-142">Créez un fichier compressé qui contient les valeurs d’authentification du registre de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="a8116-142">Create a compressed file that contains the container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="a8116-143">Copiez ce fichier dans le stockage partagé de cluster.</span><span class="sxs-lookup"><span data-stu-id="a8116-143">Copy this file to the cluster shared storage.</span></span> <span data-ttu-id="a8116-144">Cette étape rend le fichier disponible sur tous les nœuds du cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a8116-144">This step makes the file available on all nodes of the DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-to-acr"></a><span data-ttu-id="a8116-145">Télécharger une image dans l’ACR</span><span class="sxs-lookup"><span data-stu-id="a8116-145">Upload image to ACR</span></span>

<span data-ttu-id="a8116-146">Créez à présent, à partir d’un ordinateur de développement ou de tout autre système avec Docker installé, une image et chargez-le dans Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a8116-146">Now from a development machine, or any other system with Docker installed, create an image and upload it to the Azure Container Registry.</span></span>

<span data-ttu-id="a8116-147">Créez un conteneur à partir de l’image Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a8116-147">Create a container from the Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="a8116-148">Capturez maintenant le conteneur dans une nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="a8116-148">Now capture the container into a new image.</span></span> <span data-ttu-id="a8116-149">Le nom de l’image doit inclure le `loginServer` nom du registre de conteneurs avec un format `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="a8116-149">The image name needs to include the `loginServer` name of the container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="a8116-150">Connectez-vous à Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="a8116-150">Login into the Azure Container Registry.</span></span> <span data-ttu-id="a8116-151">Remplacez le nom par le nom loginServer, le --nom d’utilisateur par le nom du registre de conteneurs et le --mot de passe par l’un des mots de passe fournis.</span><span class="sxs-lookup"><span data-stu-id="a8116-151">Replace the name with the loginServer name, the --username with the name of the container registry, and the --password with one of the provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="a8116-152">Enfin, téléchargez l’image dans le registre ACR.</span><span class="sxs-lookup"><span data-stu-id="a8116-152">Finally, upload the image to the ACR registry.</span></span> <span data-ttu-id="a8116-153">Cet exemple permet de télécharger une image nommée dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="a8116-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="a8116-154">Exécuter une image à partir de l’ACR</span><span class="sxs-lookup"><span data-stu-id="a8116-154">Run an image from ACR</span></span>

<span data-ttu-id="a8116-155">Pour utiliser une image à partir du registre ACR, créez un nom de fichier *acrDemo.json* et copiez-y le texte suivant.</span><span class="sxs-lookup"><span data-stu-id="a8116-155">To use an image from the ACR registry, create a file names *acrDemo.json* and copy the following text into it.</span></span> <span data-ttu-id="a8116-156">Remplacez le nom de l’image par le nom de loginServer du registre de conteneurs et le nom de l’image, par exemple `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="a8116-156">Replace the image name with the container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="a8116-157">Notez la propriété `uris`.</span><span class="sxs-lookup"><span data-stu-id="a8116-157">Take note of the `uris` property.</span></span> <span data-ttu-id="a8116-158">Cette propriété contient l’emplacement du fichier d’authentification du registre de conteneurs, qui dans ce cas est le partage de fichiers Azure installé sur chaque nœud du cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="a8116-158">This property holds the location of the container registry authentication file, which in this case is the Azure file share that is mounted on each node in the DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="a8116-159">Déployez l’application avec le CLI DC/OC.</span><span class="sxs-lookup"><span data-stu-id="a8116-159">Deploy the application with the DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="a8116-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a8116-160">Next steps</span></span>

<span data-ttu-id="a8116-161">Dans ce didacticiel, vous avez configurer le contrôleur de domaine/système d’exploitation pour utiliser Azure Container Registry, y compris les tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="a8116-161">In this tutorial you have configure DC/OS to use Azure Container Registry including the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a8116-162">Déployer Azure Container Registry (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="a8116-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="a8116-163">Configurer l’authentification ACR sur un cluster de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="a8116-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="a8116-164">Télécharger une image dans Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a8116-164">Uploaded an image to the Azure Container Registry</span></span>
> * <span data-ttu-id="a8116-165">Exécuter une image de conteneur depuis Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a8116-165">Run a container image from the Azure Container Registry</span></span>
