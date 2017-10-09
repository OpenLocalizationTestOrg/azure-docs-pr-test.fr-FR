---
title: aaaUse hello extension de machine virtuelle de Azure Docker avec hello Azure CLI 1.0 | Documents Microsoft
description: "Découvrez comment toouse hello tooquickly d’extension de machine virtuelle de Docker et déployer en toute sécurité un environnement de Docker dans Azure à l’aide de modèles de gestionnaire de ressources."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="c3364-103">Créer un environnement de Docker dans Azure à l’aide d’extension de machine virtuelle de Docker hello avec hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c3364-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="c3364-104">Docker est une plate-forme de création d’images qui vous permet de travail tooquickly avec des conteneurs sur Linux (et ainsi de Windows) et le gestion des conteneurs populaires.</span><span class="sxs-lookup"><span data-stu-id="c3364-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="c3364-105">Dans Azure, il existe différentes méthodes que vous pouvez déployer selon les besoins de tooyour de Docker.</span><span class="sxs-lookup"><span data-stu-id="c3364-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="c3364-106">Cet article se concentre sur l’utilisation d’extension de machine virtuelle de Docker hello et modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="c3364-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="c3364-107">Pour plus d’informations sur les méthodes de déploiement hello, y compris à l’aide de la Machine Docker et les Services de conteneur Azure, consultez hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="c3364-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="c3364-108">prototype de tooquickly une application, vous pouvez créer un seul hôte Docker à l’aide de [Docker ordinateur](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="c3364-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="c3364-109">Pour les environnements plus grandes et plus stables, vous pouvez utiliser extension de machine virtuelle de Azure Docker hello, qui prend également en charge [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate les déploiements de conteneur cohérent.</span><span class="sxs-lookup"><span data-stu-id="c3364-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="c3364-110">Cet article explique à l’aide d’extension de machine virtuelle de Azure Docker hello.</span><span class="sxs-lookup"><span data-stu-id="c3364-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="c3364-111">toobuild prêt pour la production d’environnements évolutifs qui fournissent des outils de planification et de gestion supplémentaires, vous pouvez déployer un [Docker Swarm de cluster sur les Services de conteneur Azure](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="c3364-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c3364-112">Tâche de hello CLI versions toocomplete</span><span class="sxs-lookup"><span data-stu-id="c3364-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="c3364-113">Vous pouvez exécuter la tâche hello à l’aide de hello CLI versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="c3364-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="c3364-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – notre CLI pour hello classique et la ressource gestion des modèles de déploiement (cet article)</span><span class="sxs-lookup"><span data-stu-id="c3364-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c3364-115">[Azure CLI 2.0](dockerextension.md) -notre prochaine génération CLI pour le modèle de déploiement de gestion de ressources hello</span><span class="sxs-lookup"><span data-stu-id="c3364-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="c3364-116">Présentation de l’extension Azure Docket VM</span><span class="sxs-lookup"><span data-stu-id="c3364-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="c3364-117">Hello extension de machine virtuelle de Azure Docker installe et configure les démon Docker de hello, Docker et du client Docker Compose sur votre ordinateur de virtuel (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="c3364-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="c3364-118">Extension de machine virtuelle de Azure Docker hello, vous offre davantage de contrôle et de fonctionnalités que simplement à l’aide d’une Machine Docker ou création de l’hôte de Docker hello vous-même.</span><span class="sxs-lookup"><span data-stu-id="c3364-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="c3364-119">Ces fonctionnalités, telles que [Docker Compose](https://docs.docker.com/compose/overview/), rendre l’extension de machine virtuelle de Azure Docker hello adaptée pour les environnements de développement ou de production plus fiables.</span><span class="sxs-lookup"><span data-stu-id="c3364-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="c3364-120">Les modèles de gestionnaire de ressources Azure définissent hello intégralité de la structure de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="c3364-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="c3364-121">Les modèles vous toocreate et configurer les ressources, telles que l’hôte Docker de hello machines virtuelles, de stockage, de contrôles d’accès en fonction du rôle (RBAC) et de diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c3364-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="c3364-122">Vous pouvez réutiliser ces déploiements supplémentaires toocreate de modèles de manière cohérente.</span><span class="sxs-lookup"><span data-stu-id="c3364-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="c3364-123">Pour plus d’informations sur Azure Resource Manager et les modèles, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3364-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="c3364-124">Déployer un modèle avec hello extension de machine virtuelle de Azure Docker</span><span class="sxs-lookup"><span data-stu-id="c3364-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="c3364-125">Nous allons utiliser un existant toocreate de modèle de démarrage rapide un VM Ubuntu qui utilise hello Azure Docker VM extension tooinstall et configurer l’hôte Docker de hello.</span><span class="sxs-lookup"><span data-stu-id="c3364-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="c3364-126">Vous pouvez afficher le modèle hello ici : [Simple déploiement d’un VM Ubuntu avec Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="c3364-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="c3364-127">Vous devez hello [dernière CLI d’Azure](../../cli-install-nodejs.md) installé et connecté à l’aide de mode de gestionnaire de ressources hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3364-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c3364-128">Déployer le modèle hello à l’aide de hello CLI d’Azure, spécifiant hello modèle URI.</span><span class="sxs-lookup"><span data-stu-id="c3364-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="c3364-129">Hello exemple suivant crée un groupe de ressources nommé *myResourceGroup* Bonjour *westus* emplacement.</span><span class="sxs-lookup"><span data-stu-id="c3364-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="c3364-130">Utilisez vos propres nom de groupe de ressources et emplacement comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3364-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="c3364-131">Répondre à votre compte de stockage hello invites tooname, fournir un nom d’utilisateur et un mot de passe et fournissez un nom DNS.</span><span class="sxs-lookup"><span data-stu-id="c3364-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="c3364-132">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c3364-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="c3364-133">Hello CLI d’Azure vous renvoie toohello invite après quelques secondes seulement, mais l’hôte Docker est toujours créée et configurée par hello extension de machine virtuelle de Azure Docker.</span><span class="sxs-lookup"><span data-stu-id="c3364-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="c3364-134">Il prend quelques minutes pour hello déploiement toofinish.</span><span class="sxs-lookup"><span data-stu-id="c3364-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="c3364-135">Vous pouvez afficher plus d’informations sur l’état de l’hôte Docker hello à l’aide de hello `azure vm show` commande.</span><span class="sxs-lookup"><span data-stu-id="c3364-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="c3364-136">Hello exemple suivant vérifie état hello Hello ordinateur virtuel nommé *myDockerVM* (hello nom par défaut à partir du modèle de hello - ne modifiez pas ce nom) dans le groupe de ressources hello nommé *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="c3364-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="c3364-137">Entrez le nom hello hello du groupe de ressources que vous avez créé dans hello précédant l’étape :</span><span class="sxs-lookup"><span data-stu-id="c3364-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="c3364-138">Hello sortie Hello `azure vm show` commande est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="c3364-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="c3364-139">Début hello de sortie de hello, vous voyez hello **ProvisioningState** Hello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c3364-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="c3364-140">Lorsque cela affiche *Succeeded*, hello déploiement est terminé et que vous pouvez SSH toohello machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="c3364-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="c3364-141">Vers la fin de hello de sortie de hello, *nom de domaine complet* affiche le nom de domaine complet de hello de l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="c3364-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="c3364-142">Ce nom de domaine complet est ce que vous utilisez hôte Docker tooSSH tooyour hello restant comme suit.</span><span class="sxs-lookup"><span data-stu-id="c3364-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="c3364-143">Déployer votre premier conteneur nginx</span><span class="sxs-lookup"><span data-stu-id="c3364-143">Deploy your first nginx container</span></span>
<span data-ttu-id="c3364-144">Une fois hello déploiement est terminé, SSH tooyour hôte Docker à partir de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="c3364-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="c3364-145">Entrez vos propre nom d’utilisateur et nom de domaine complet comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3364-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="c3364-146">Une fois connecté toohello hôte Docker, nous allons exécuter un conteneur nginx :</span><span class="sxs-lookup"><span data-stu-id="c3364-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="c3364-147">sortie de Hello est similaire toohello exemple suivant comme hello nginx image est téléchargée et un conteneur démarré :</span><span class="sxs-lookup"><span data-stu-id="c3364-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="c3364-148">Vérification du statut de hello de conteneurs hello exécutant sur l’hôte Docker comme suit :</span><span class="sxs-lookup"><span data-stu-id="c3364-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="c3364-149">sortie de Hello est similaire toohello l’exemple suivant, indiquant que le conteneur de nginx hello est en cours d’exécution et les ports TCP 80 et 443 et transféré :</span><span class="sxs-lookup"><span data-stu-id="c3364-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="c3364-150">ouverture de votre conteneur dans action, toosee jusqu'à un navigateur web et entrez le nom de domaine complet hello de l’hôte Docker :</span><span class="sxs-lookup"><span data-stu-id="c3364-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Exécution d’un conteneur ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="c3364-152">Référence de modèle pour l’extension Azure Docker VM</span><span class="sxs-lookup"><span data-stu-id="c3364-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="c3364-153">Hello l’exemple précédent utilise un modèle de démarrage rapide existant.</span><span class="sxs-lookup"><span data-stu-id="c3364-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="c3364-154">Vous pouvez également déployer l’extension de machine virtuelle de Azure Docker hello avec vos propres modèles de gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="c3364-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="c3364-155">toodo, ajoutez hello suivant tooyour les modèles de gestionnaire de ressources, la définition de hello *vmName* de votre machine virtuelle en conséquence :</span><span class="sxs-lookup"><span data-stu-id="c3364-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="c3364-156">Pour découvrir la procédure pas à pas d’utilisation de modèles Resource Manager, voir la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3364-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3364-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c3364-157">Next steps</span></span>
<span data-ttu-id="c3364-158">Vous souhaiterez peut-être trop[configurer le port TCP de hello Docker démon](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), comprendre [sécurité de Docker](https://docs.docker.com/engine/security/security/), ou déployer des conteneurs à l’aide de [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="c3364-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="c3364-159">Pour plus d’informations sur hello Extension de machine virtuelle Docker Azure lui-même, consultez hello [GitHub projet](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="c3364-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="c3364-160">En savoir plus sur les options de déploiement de Docker supplémentaires hello dans Azure :</span><span class="sxs-lookup"><span data-stu-id="c3364-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="c3364-161">Utiliser l’ordinateur avec hello pilote Azure Docker</span><span class="sxs-lookup"><span data-stu-id="c3364-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="c3364-162">[Prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="c3364-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="c3364-163">Déploiement d’un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="c3364-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

