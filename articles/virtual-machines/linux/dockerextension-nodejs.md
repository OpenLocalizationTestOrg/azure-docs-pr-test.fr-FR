---
title: "Utiliser l’extension de machine virtuelle Azure Docker avec Azure CLI 1.0 | Microsoft Docs"
description: "Découvrez comment utiliser l’extension Docker VM sur Azure pour déployer un environnement Docker rapidement et en toute sécurité dans Azure en utilisant des modèle Resource Manager."
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
ms.openlocfilehash: a3cbcf63533f4042dcd695e141655c5814bd7068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension-with-the-azure-cli-10"></a><span data-ttu-id="a599b-103">Création d’un environnement Docker dans Azure à l’aide de l’extension de machine virtuelle Docker avec Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="a599b-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="a599b-104">Docker est une solution courante de gestion de conteneurs et une plateforme de création d’images qui permet de travailler rapidement avec des conteneurs sous Linux (et Windows).</span><span class="sxs-lookup"><span data-stu-id="a599b-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="a599b-105">Dans Azure, il existe différentes méthodes pour déployer Docker selon vos besoins.</span><span class="sxs-lookup"><span data-stu-id="a599b-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="a599b-106">Cet article se concentre sur l’utilisation de l’extension Docker VM et des modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a599b-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="a599b-107">Pour plus d’informations sur les différentes méthodes de déploiement, y compris l’utilisation des services Docker Machine et Azure Container, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="a599b-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="a599b-108">Pour créer rapidement un prototype d’application, vous pouvez créer un hôte Docker unique en utilisant [Docker Machine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="a599b-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="a599b-109">Pour les environnements plus vastes et plus stables, vous pouvez utiliser l’extension Azure Docker VM, qui prend également en charge [Docker Compose](https://docs.docker.com/compose/overview/) pour générer des déploiements de conteneur cohérents.</span><span class="sxs-lookup"><span data-stu-id="a599b-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span></span> <span data-ttu-id="a599b-110">Cet article détaille l’utilisation de l’extension Azure Docker VM.</span><span class="sxs-lookup"><span data-stu-id="a599b-110">This article details using the Azure Docker VM extension.</span></span>
* <span data-ttu-id="a599b-111">Pour créer des environnements prêts pour la production et évolutifs qui exploitent d’autres outils de planification et de gestion, vous pouvez déployer [un cluster Docker Swarm sur les services Azure Container](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="a599b-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="a599b-112">Versions de l’interface de ligne de commande permettant d’effectuer la tâche</span><span class="sxs-lookup"><span data-stu-id="a599b-112">CLI versions to complete the task</span></span>
<span data-ttu-id="a599b-113">Vous pouvez exécuter la tâche en utilisant l’une des versions suivantes de l’interface de ligne de commande (CLI) :</span><span class="sxs-lookup"><span data-stu-id="a599b-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="a599b-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) : notre interface de ligne de commande pour les modèles de déploiement Classique et Resource Manager (cet article)</span><span class="sxs-lookup"><span data-stu-id="a599b-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a599b-115">[Azure CLI 2.0](dockerextension.md) : notre interface de ligne de commande nouvelle génération pour le modèle de déploiement Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a599b-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for the resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="a599b-116">Présentation de l’extension Azure Docket VM</span><span class="sxs-lookup"><span data-stu-id="a599b-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="a599b-117">L’extension de machine virtuelle Docker Azure installe et configure le démon Docker, le client Docker et Docker Compose dans votre machine virtuelle (VM) Linux.</span><span class="sxs-lookup"><span data-stu-id="a599b-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="a599b-118">L’extension Azure Docker VM vous offre plus de contrôle et de fonctionnalités que la simple utilisation de Docker Machine ou la création de votre propre hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="a599b-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="a599b-119">Ces fonctionnalités supplémentaires, telles que [Docker Compose](https://docs.docker.com/compose/overview/), permettent d’adapter l’extension Azure Docker VM à des environnements de développement ou de production plus robustes.</span><span class="sxs-lookup"><span data-stu-id="a599b-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="a599b-120">Les modèles Azure Resource Manager définissent la structure complète de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="a599b-120">Azure Resource Manager templates define the entire structure of your environment.</span></span> <span data-ttu-id="a599b-121">Les modèles vous permettent de créer et de configurer des ressources comme les machines virtuelles hôtes Docker, le stockage, les contrôles d’accès en fonction du rôle (RBAC) et les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a599b-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="a599b-122">Vous pouvez réutiliser ces modèles pour créer des déploiements supplémentaires de manière cohérente.</span><span class="sxs-lookup"><span data-stu-id="a599b-122">You can reuse these templates to create additional deployments in a consistent manner.</span></span> <span data-ttu-id="a599b-123">Pour plus d’informations sur Azure Resource Manager et les modèles, consultez la page [Présentation d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a599b-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="a599b-124">Déployer un modèle avec l’extension de machine virtuelle Azure Docker</span><span class="sxs-lookup"><span data-stu-id="a599b-124">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="a599b-125">Nous allons utiliser un modèle de démarrage rapide existant pour créer une machine virtuelle Ubuntu qui utilise l’extension Azure Docker VM pour installer et configurer l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="a599b-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="a599b-126">Vous pouvez voir le modèle ici : [Simple deployment of an Ubuntu VM with Docker (Déploiement simple d’une machine virtuelle Ubuntu avec Docker)](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="a599b-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="a599b-127">La [dernière version de l’interface de ligne de commande Azure (CLI)](../../cli-install-nodejs.md) doit être installée et connectée à l’aide du mode Resource Manager comme suit :</span><span class="sxs-lookup"><span data-stu-id="a599b-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="a599b-128">Déployez le modèle à l’aide de l’interface de ligne de commande Azure, en spécifiant le modèle URI.</span><span class="sxs-lookup"><span data-stu-id="a599b-128">Deploy the template using the Azure CLI, specifying the template URI.</span></span> <span data-ttu-id="a599b-129">L’exemple suivant crée un groupe de ressources nommé *myResourceGroup* à l’emplacement *westus*.</span><span class="sxs-lookup"><span data-stu-id="a599b-129">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span> <span data-ttu-id="a599b-130">Utilisez vos propres nom de groupe de ressources et emplacement comme suit :</span><span class="sxs-lookup"><span data-stu-id="a599b-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="a599b-131">Répondez aux invites pour nommer votre compte de stockage, indiquez le nom d’utilisateur et le mot de passe, puis spécifiez un nom DNS.</span><span class="sxs-lookup"><span data-stu-id="a599b-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="a599b-132">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a599b-132">The output is similar to the following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for the following parameters
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

<span data-ttu-id="a599b-133">L’interface CLI Azure vous renvoie à l’invite après quelques secondes, mais l’hôte Docker est toujours en cours de création et de configuration par l’extension Azure Docker VM.</span><span class="sxs-lookup"><span data-stu-id="a599b-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span></span> <span data-ttu-id="a599b-134">Le déploiement prend quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a599b-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="a599b-135">Vous pouvez afficher des détails sur l’état de l’hôte Docker à l’aide de la commande `azure vm show`.</span><span class="sxs-lookup"><span data-stu-id="a599b-135">You can view details about the Docker host status using the `azure vm show` command.</span></span>

<span data-ttu-id="a599b-136">L’exemple suivant vérifie l’état de la machine virtuelle nommée *myDockerVM* (nom par défaut extrait du gabarit - ne pas modifier ce nom) dans le groupe de ressources nommé *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="a599b-136">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*.</span></span> <span data-ttu-id="a599b-137">Entrez le nom du groupe de ressources que vous avez créé à l’étape précédente :</span><span class="sxs-lookup"><span data-stu-id="a599b-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="a599b-138">Le résultat de la commande `azure vm show` ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="a599b-138">The output of the `azure vm show` command is similar to the following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myDockerVM"
+ Looking up the NIC "myVMNicD"
+ Looking up the public ip "myPublicIPD"
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

<span data-ttu-id="a599b-139">Vers le haut de la sortie, vous voyez le **ProvisioningState** de la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a599b-139">Near the top of the output, you see the **ProvisioningState** of the VM.</span></span> <span data-ttu-id="a599b-140">Lorsque *Succeeded* (Opération réussie) s’affiche, le déploiement est terminé et vous pouvez vous connecter par SSH à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="a599b-140">When this displays *Succeeded*, the deployment has finished and you can SSH to the VM.</span></span>

<span data-ttu-id="a599b-141">Vers la fin du résultat, *FQDN* affiche le nom de domaine complet de l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="a599b-141">Towards the end of the output, *FQDN* displays the fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="a599b-142">Ce nom de domaine complet est ce que vous utilisez pour vous connecter par SSH à votre hôte Docker dans les étapes restantes.</span><span class="sxs-lookup"><span data-stu-id="a599b-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="a599b-143">Déployer votre premier conteneur nginx</span><span class="sxs-lookup"><span data-stu-id="a599b-143">Deploy your first nginx container</span></span>
<span data-ttu-id="a599b-144">Une fois le déploiement terminé, connectez-vous par SSH à votre nouvel hôte Docker à partir de votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="a599b-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span></span> <span data-ttu-id="a599b-145">Entrez vos propre nom d’utilisateur et nom de domaine complet comme suit :</span><span class="sxs-lookup"><span data-stu-id="a599b-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="a599b-146">Une fois connecté à l’hôte Docker, nous allons exécuter un conteneur nginx :</span><span class="sxs-lookup"><span data-stu-id="a599b-146">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="a599b-147">La sortie est similaire à l’exemple suivant lorsque l’image nginx est téléchargée et qu’un conteneur est démarré :</span><span class="sxs-lookup"><span data-stu-id="a599b-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="a599b-148">Vérifiez l’état des conteneurs s’exécutant sur l’hôte Docker comme suit :</span><span class="sxs-lookup"><span data-stu-id="a599b-148">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="a599b-149">Le résultat est similaire à l’exemple suivant, indiquant que le conteneur nginx est en cours d’exécution et que les ports TCP 80 et 443 sont transférés :</span><span class="sxs-lookup"><span data-stu-id="a599b-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="a599b-150">Pour voir votre conteneur en action, ouvrez un navigateur Web et entrez le nom complet de votre hôte Docker :</span><span class="sxs-lookup"><span data-stu-id="a599b-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span></span>

![Exécution d’un conteneur ngnix](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="a599b-152">Référence de modèle pour l’extension Azure Docker VM</span><span class="sxs-lookup"><span data-stu-id="a599b-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="a599b-153">L’exemple précédent utilise un modèle de démarrage rapide existant.</span><span class="sxs-lookup"><span data-stu-id="a599b-153">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="a599b-154">Vous pouvez également déployer l’extension Azure Docker VM avec vos propres modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a599b-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="a599b-155">Pour cela, ajoutez ce qui suit à vos gabarits Resource Manager, en définissant la valeur *vmName* de votre machine virtuelle en conséquence :</span><span class="sxs-lookup"><span data-stu-id="a599b-155">To do so, add the following to your Resource Manager templates, defining the *vmName* of your VM appropriately:</span></span>

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

<span data-ttu-id="a599b-156">Pour découvrir la procédure pas à pas d’utilisation de modèles Resource Manager, voir la [Vue d’ensemble d’Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a599b-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a599b-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a599b-157">Next steps</span></span>
<span data-ttu-id="a599b-158">Vous pouvez [configurer le port TCP du démon Docker](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), examiner la [sécurité Docker](https://docs.docker.com/engine/security/security/), ou déployer des conteneurs à l’aide de [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="a599b-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="a599b-159">Pour plus d’informations sur l’extension Azure Docker VM elle-même, consultez le [projet GitHub](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="a599b-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="a599b-160">En savoir plus sur les options de déploiement supplémentaires Docker dans Azure :</span><span class="sxs-lookup"><span data-stu-id="a599b-160">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="a599b-161">Utiliser Docker Machine avec le pilote Azure</span><span class="sxs-lookup"><span data-stu-id="a599b-161">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="a599b-162">[Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples sur une machine virtuelle Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="a599b-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="a599b-163">Déploiement d’un cluster Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="a599b-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

