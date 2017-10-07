---
title: aaaUse hello extension de machine virtuelle de Azure Docker | Documents Microsoft
description: "Découvrez comment toouse hello Docker VM extension tooquickly et en toute sécurité déployer un environnement Docker dans Azure à l’aide de modèles de gestionnaire de ressources et hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="c324d-103">Créer un environnement de Docker dans Azure à l’aide d’extension de machine virtuelle de Docker hello</span><span class="sxs-lookup"><span data-stu-id="c324d-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="c324d-104">Docker est une plate-forme de création d’images qui vous permet de travail tooquickly avec des conteneurs sur Linux et le gestion des conteneurs populaires.</span><span class="sxs-lookup"><span data-stu-id="c324d-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="c324d-105">Dans Azure, il existe différentes méthodes que vous pouvez déployer selon les besoins de tooyour de Docker.</span><span class="sxs-lookup"><span data-stu-id="c324d-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="c324d-106">Cet article se concentre sur l’utilisation d’extension de machine virtuelle de Docker hello et modèles Azure Resource Manager par hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c324d-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="c324d-107">Vous pouvez également effectuer ces étapes avec hello [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c324d-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="c324d-108">Présentation de l’extension Azure Docket VM</span><span class="sxs-lookup"><span data-stu-id="c324d-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="c324d-109">Hello extension de machine virtuelle de Azure Docker installe et configure les démon Docker de hello, Docker et du client Docker Compose sur votre ordinateur de virtuel (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="c324d-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="c324d-110">Extension de machine virtuelle de Azure Docker hello, vous offre davantage de contrôle et de fonctionnalités que simplement à l’aide d’une Machine Docker ou création de l’hôte de Docker hello vous-même.</span><span class="sxs-lookup"><span data-stu-id="c324d-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="c324d-111">Ces fonctionnalités, telles que [Docker Compose](https://docs.docker.com/compose/overview/), rendre l’extension de machine virtuelle de Azure Docker hello adaptée pour les environnements de développement ou de production plus fiables.</span><span class="sxs-lookup"><span data-stu-id="c324d-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="c324d-112">Pour plus d’informations sur les méthodes de déploiement hello, y compris à l’aide de la Machine Docker et les Services de conteneur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="c324d-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="c324d-113">prototype de tooquickly une application, vous pouvez créer un seul hôte Docker à l’aide de [Docker ordinateur](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="c324d-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="c324d-114">toobuild prêt pour la production d’environnements évolutifs qui fournissent des outils de planification et de gestion supplémentaires, vous pouvez déployer un [Docker Swarm de cluster sur les Services de conteneur Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c324d-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="c324d-115">Déployer un modèle avec hello extension de machine virtuelle de Azure Docker</span><span class="sxs-lookup"><span data-stu-id="c324d-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="c324d-116">Nous allons utiliser un existant toocreate de modèle de démarrage rapide un VM Ubuntu qui utilise hello Azure Docker VM extension tooinstall et configurer l’hôte Docker de hello.</span><span class="sxs-lookup"><span data-stu-id="c324d-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="c324d-117">Vous pouvez afficher le modèle hello ici : [Simple déploiement d’un VM Ubuntu avec Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c324d-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c324d-118">Vous devez hello dernières [Azure CLI 2.0](/cli/azure/install-az-cli2) installé et connecté à l’aide du compte Azure tooan [ouverture de session az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="c324d-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="c324d-119">Tout d’abord, créez un groupe de ressources avec la commande [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c324d-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="c324d-120">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement :</span><span class="sxs-lookup"><span data-stu-id="c324d-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="c324d-121">Ensuite, déployez une machine virtuelle avec [créer de déploiement de groupe az](/cli/azure/group/deployment#create) qui inclut l’extension de machine virtuelle de Azure Docker hello de [ce modèle Azure Resource Manager sur GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c324d-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="c324d-122">Fournissez vos propres valeurs pour *newStorageAccountName*, *adminUsername*, *adminPassword* et *dnsNameForPublicIP* comme suit :</span><span class="sxs-lookup"><span data-stu-id="c324d-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c324d-123">Il prend quelques minutes pour hello déploiement toofinish.</span><span class="sxs-lookup"><span data-stu-id="c324d-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="c324d-124">Une fois le déploiement de hello est terminé, [déplacer l’étape de toonext](#deploy-your-first-nginx-container) tooSSH tooyour machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c324d-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="c324d-125">Invite de toohello tooinstead redonner le contrôle et de déploiement de hello permettent continuent en arrière-plan de hello, ajoutez éventuellement hello `--no-wait` indicateur toohello précédant la commande.</span><span class="sxs-lookup"><span data-stu-id="c324d-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="c324d-126">Ce processus vous permet de tooperform autre travail Bonjour CLI pendant le déploiement hello se poursuit pendant quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c324d-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="c324d-127">Vous pouvez ensuite afficher plus d’informations sur l’état de l’hôte Docker hello avec [afficher de machine virtuelle az](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="c324d-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="c324d-128">Hello exemple suivant vérifie état hello Hello ordinateur virtuel nommé *myDockerVM* (hello nom par défaut à partir du modèle de hello - ne modifiez pas ce nom) dans le groupe de ressources hello nommé *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="c324d-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="c324d-129">Lorsque cette commande retourne *Succeeded*, hello déploiement est terminé et que vous pouvez SSH toohello VM Bonjour suivant l’étape.</span><span class="sxs-lookup"><span data-stu-id="c324d-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="c324d-130">Déployer votre premier conteneur nginx</span><span class="sxs-lookup"><span data-stu-id="c324d-130">Deploy your first nginx container</span></span>
<span data-ttu-id="c324d-131">tooview les détails de votre machine virtuelle, notamment nom DNS hello, utilisent `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="c324d-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="c324d-132">SSH tooyour Docker nouvel hôte à partir de votre ordinateur local comme suit :</span><span class="sxs-lookup"><span data-stu-id="c324d-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c324d-133">Une fois connecté toohello hôte Docker, nous allons exécuter un conteneur nginx :</span><span class="sxs-lookup"><span data-stu-id="c324d-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="c324d-134">sortie de Hello est similaire toohello exemple suivant comme hello nginx image est téléchargée et un conteneur démarré :</span><span class="sxs-lookup"><span data-stu-id="c324d-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="c324d-135">Vérification du statut de hello de conteneurs hello exécutant sur l’hôte Docker comme suit :</span><span class="sxs-lookup"><span data-stu-id="c324d-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="c324d-136">sortie de Hello est similaire toohello l’exemple suivant, indiquant que le conteneur de nginx hello est en cours d’exécution et les ports TCP 80 et 443 et transféré :</span><span class="sxs-lookup"><span data-stu-id="c324d-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="c324d-137">ouverture de votre conteneur dans action, toosee jusqu'à un navigateur web et entrez le nom DNS de hello de l’hôte Docker :</span><span class="sxs-lookup"><span data-stu-id="c324d-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Exécution d’un conteneur ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="c324d-139">Référence de modèle pour l’extension Azure Docker VM</span><span class="sxs-lookup"><span data-stu-id="c324d-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="c324d-140">Hello l’exemple précédent utilise un modèle de démarrage rapide existant.</span><span class="sxs-lookup"><span data-stu-id="c324d-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="c324d-141">Vous pouvez également déployer l’extension de machine virtuelle de Azure Docker hello avec vos propres modèles de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="c324d-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="c324d-142">toodo, ajoutez hello suivant tooyour les modèles de gestionnaire de ressources, la définition de hello `vmName` de votre machine virtuelle en conséquence :</span><span class="sxs-lookup"><span data-stu-id="c324d-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="c324d-143">Pour découvrir la procédure pas à pas d’utilisation de modèles Resource Manager, voir la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c324d-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c324d-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c324d-144">Next steps</span></span>
<span data-ttu-id="c324d-145">Vous souhaiterez peut-être trop[configurer le port TCP de hello Docker démon](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendre [sécurité de Docker](https://docs.docker.com/engine/security/security/), ou déployer des conteneurs à l’aide de [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="c324d-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="c324d-146">Pour plus d’informations sur hello Extension de machine virtuelle Docker Azure lui-même, consultez hello [GitHub projet](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="c324d-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="c324d-147">En savoir plus sur les options de déploiement de Docker supplémentaires hello dans Azure :</span><span class="sxs-lookup"><span data-stu-id="c324d-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="c324d-148">Utiliser l’ordinateur avec hello pilote Azure Docker</span><span class="sxs-lookup"><span data-stu-id="c324d-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="c324d-149">[Prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="c324d-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="c324d-150">Déploiement d’un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c324d-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

