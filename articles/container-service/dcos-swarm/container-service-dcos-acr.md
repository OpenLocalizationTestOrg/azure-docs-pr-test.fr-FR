---
title: "aaaUsing ACR avec un cluster de contrôleur de domaine/système d’exploitation Azure | Documents Microsoft"
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
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="8d714-104">Utiliser ACR avec un toodeploy de cluster de contrôleur de domaine/système d’exploitation de votre application</span><span class="sxs-lookup"><span data-stu-id="8d714-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="8d714-105">Dans cet article, nous explorons comment toouse Registre de conteneur Azure avec un cluster de contrôleur de domaine/système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="8d714-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="8d714-106">À l’aide de ACR vous permet de tooprivately store et gérer les images de conteneur.</span><span class="sxs-lookup"><span data-stu-id="8d714-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="8d714-107">Ce didacticiel couvre hello tâches suivantes :</span><span class="sxs-lookup"><span data-stu-id="8d714-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d714-108">Déployer Azure Container Registry (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="8d714-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="8d714-109">Configurer l’authentification ACR sur un cluster de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="8d714-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="8d714-110">Télécharger une image de toohello Registre de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="8d714-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="8d714-111">Exécuter une image de conteneur à partir de hello Registre de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="8d714-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="8d714-112">Vous avez besoin d’un contrôleur de domaine/OS ACS hello toocomplete de cluster les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8d714-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="8d714-113">Le cas échéant, cet [exemple de script](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) peut en créer un pour vous.</span><span class="sxs-lookup"><span data-stu-id="8d714-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="8d714-114">Ce didacticiel requiert hello CLI d’Azure version 2.0.4 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8d714-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8d714-115">Exécutez `az --version` version de hello toofind.</span><span class="sxs-lookup"><span data-stu-id="8d714-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8d714-116">Si vous avez besoin de tooupgrade, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8d714-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="8d714-117">Déployer Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="8d714-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="8d714-118">Si nécessaire, créez un Registre de conteneur Azure avec hello [az acr créer](/cli/azure/acr#create) commande.</span><span class="sxs-lookup"><span data-stu-id="8d714-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="8d714-119">Hello exemple suivant crée un Registre avec une générer de façon aléatoire nom.</span><span class="sxs-lookup"><span data-stu-id="8d714-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="8d714-120">Registre de Hello est également configuré avec un compte d’administrateur à l’aide de hello `--admin-enabled` argument.</span><span class="sxs-lookup"><span data-stu-id="8d714-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="8d714-121">Une fois que le Registre de hello a été créé, hello CLI d’Azure génère des données similaires toohello suit.</span><span class="sxs-lookup"><span data-stu-id="8d714-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="8d714-122">Prenez note de hello `name` et `loginServer`, ils sont utilisés dans les étapes ultérieures.</span><span class="sxs-lookup"><span data-stu-id="8d714-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

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

<span data-ttu-id="8d714-123">Obtenir des informations d’identification du Registre hello conteneur à l’aide de hello [afficher d’informations d’identification az acr](/cli/azure/acr/credential) commande.</span><span class="sxs-lookup"><span data-stu-id="8d714-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="8d714-124">Hello de substitution `--name` avec hello une indication dans la dernière étape de hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="8d714-125">Notez un mot de passe, nécessaire pour une étape ultérieure.</span><span class="sxs-lookup"><span data-stu-id="8d714-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="8d714-126">Pour plus d’informations sur le Registre de conteneur Azure, consultez [registres de conteneur Docker Introduction tooprivate](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="8d714-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="8d714-127">Gérer l’authentification ACR</span><span class="sxs-lookup"><span data-stu-id="8d714-127">Manage ACR authentication</span></span>

<span data-ttu-id="8d714-128">façon conventionnelle de Hello image toopush et par extraction à partir d’un Registre privé est toofirst s’authentifier auprès du Registre de hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="8d714-129">toodo ainsi, vous devez utiliser hello `docker login` commande sur n’importe quel client qui a besoin des registres privés de tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="8d714-130">Un cluster de contrôleur de domaine/système d’exploitation peut contenir plusieurs nœuds, tous doivent toobe authentifié avec hello ACR, il est utile tooautomate ce processus sur chaque nœud.</span><span class="sxs-lookup"><span data-stu-id="8d714-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="8d714-131">Créer un stockage partagé</span><span class="sxs-lookup"><span data-stu-id="8d714-131">Create shared storage</span></span>

<span data-ttu-id="8d714-132">Ce processus utilise un partage de fichiers Azure qui a été monté sur chaque nœud de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="8d714-133">Si vous n’avez pas déjà configuré de stockage partagé, consultez [Configurer un partage de fichier dans un cluster de contrôleur de domaine/système d’exploitation](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="8d714-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="8d714-134">Configurer une authentification ACR</span><span class="sxs-lookup"><span data-stu-id="8d714-134">Configure ACR authentication</span></span>

<span data-ttu-id="8d714-135">Tout d’abord, obtenez hello hello DC/OS maître et le stocker dans une variable de nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="8d714-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="8d714-136">Créez une connexion SSH avec hello masque (ou de hello première) de votre cluster basé sur le système d’exploitation contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="8d714-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="8d714-137">Modifiez le nom d’utilisateur de hello si une valeur par défaut a été utilisée lors de la création du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="8d714-138">Exécutez hello suivant commande toologin toohello Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="8d714-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="8d714-139">Remplacez hello `--username` avec nom hello du Registre de conteneur hello et hello `--password` avec l’un des mots de passe hello fourni.</span><span class="sxs-lookup"><span data-stu-id="8d714-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="8d714-140">Remplacez le dernier argument de hello *mycontainerregistry.azurecr.io* dans l’exemple hello avec le nom de loginServer hello du Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="8d714-141">Cette commande stocke les valeurs de l’authentification de hello localement sous hello `~/.docker` chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="8d714-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="8d714-142">Créer un fichier compressé qui contient des valeurs de l’authentification de Registre de conteneur hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="8d714-143">Copiez ce stockage partagé de cluster toohello des fichiers.</span><span class="sxs-lookup"><span data-stu-id="8d714-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="8d714-144">Cette étape rend hello disponible sur tous les nœuds du cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="8d714-145">Télécharger l’image tooACR</span><span class="sxs-lookup"><span data-stu-id="8d714-145">Upload image tooACR</span></span>

<span data-ttu-id="8d714-146">Maintenant à partir d’un ordinateur de développement, ou tout autre système avec Docker installé, créez une image et téléchargez-le toohello Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="8d714-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="8d714-147">Créer un conteneur à partir de l’image d’Ubuntu hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="8d714-148">Prêt à capturer les conteneur hello dans une nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="8d714-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="8d714-149">nom de l’image Hello doit tooinclude hello `loginServer` nom de registrywith de conteneur hello un format de `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="8d714-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="8d714-150">Connexion en hello Registre de conteneur Azure.</span><span class="sxs-lookup"><span data-stu-id="8d714-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="8d714-151">Remplacez hello par nom de loginServer hello, hello--nom d’utilisateur avec le nom hello du Registre de conteneur hello et hello--mot de passe avec l’un des mots de passe hello fourni.</span><span class="sxs-lookup"><span data-stu-id="8d714-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="8d714-152">Enfin, téléchargez Registre d’ACR toohello hello images.</span><span class="sxs-lookup"><span data-stu-id="8d714-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="8d714-153">Cet exemple permet de télécharger une image nommée dcos-demo.</span><span class="sxs-lookup"><span data-stu-id="8d714-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="8d714-154">Exécuter une image à partir de l’ACR</span><span class="sxs-lookup"><span data-stu-id="8d714-154">Run an image from ACR</span></span>

<span data-ttu-id="8d714-155">toouse une image à partir du Registre ACR hello, créez un fichier de noms *acrDemo.json* et hello de copie après le texte dans celle-ci.</span><span class="sxs-lookup"><span data-stu-id="8d714-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="8d714-156">Remplacez nom de l’image hello avec le nom de loginServer de Registre de conteneur hello et le nom de l’image, par exemple `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="8d714-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="8d714-157">Prenez note de hello `uris` propriété.</span><span class="sxs-lookup"><span data-stu-id="8d714-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="8d714-158">Cette propriété contient l’emplacement de hello du fichier de l’authentification Registre hello conteneur, dans ce cas est le partage de fichiers Azure hello est monté sur chaque nœud de cluster de contrôleur de domaine/système d’exploitation hello.</span><span class="sxs-lookup"><span data-stu-id="8d714-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

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

<span data-ttu-id="8d714-159">Déployer l’application hello avec hello DC/OC CLI.</span><span class="sxs-lookup"><span data-stu-id="8d714-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="8d714-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8d714-160">Next steps</span></span>

<span data-ttu-id="8d714-161">Dans ce didacticiel vous avez configurer toouse de contrôleur de domaine/système d’exploitation registre de conteneur Azure notamment hello suivant de tâches :</span><span class="sxs-lookup"><span data-stu-id="8d714-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d714-162">Déployer Azure Container Registry (le cas échéant)</span><span class="sxs-lookup"><span data-stu-id="8d714-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="8d714-163">Configurer l’authentification ACR sur un cluster de contrôleur de domaine/système d’exploitation</span><span class="sxs-lookup"><span data-stu-id="8d714-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="8d714-164">Télécharger une image de toohello Registre de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="8d714-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="8d714-165">Exécuter une image de conteneur à partir de hello Registre de conteneur Azure</span><span class="sxs-lookup"><span data-stu-id="8d714-165">Run a container image from hello Azure Container Registry</span></span>
