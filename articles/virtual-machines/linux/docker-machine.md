---
title: "Utiliser Docker Machine pour créer des hôtes Linux dans Azure | Microsoft Docs"
description: "Décrit l’utilisation de Docker Machine pour créer des hôtes Docker dans Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: a69951ed60edab8ae20374ab3869b468979c4907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-docker-machine-to-create-hosts-in-azure"></a><span data-ttu-id="7a55d-103">Comment utiliser Docker Machine pour créer des hôtes dans Azure</span><span class="sxs-lookup"><span data-stu-id="7a55d-103">How to use Docker Machine to create hosts in Azure</span></span>
<span data-ttu-id="7a55d-104">Cet article explique comment utiliser [Docker Machine](https://docs.docker.com/machine/) pour créer des hôtes dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7a55d-104">This article details how to use [Docker Machine](https://docs.docker.com/machine/) to create hosts in Azure.</span></span> <span data-ttu-id="7a55d-105">La commande `docker-machine` crée une machine virtuelle Linux dans Azure, puis installe Docker.</span><span class="sxs-lookup"><span data-stu-id="7a55d-105">The `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="7a55d-106">Vous pouvez ensuite gérer vos hôtes Docker dans Azure en utilisant les mêmes outils et flux de travail locaux.</span><span class="sxs-lookup"><span data-stu-id="7a55d-106">You can then manage your Docker hosts in Azure using the same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="7a55d-107">Créer des machines virtuelles avec Docker Machine</span><span class="sxs-lookup"><span data-stu-id="7a55d-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="7a55d-108">Commencez par obtenir votre ID d’abonnement Azure à l’aide de la commande [az account show](/cli/azure/account#show), comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a55d-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="7a55d-109">Vous créez des machines virtuelles hôtes Docker dans Azure avec `docker-machine create` en spécifiant *azure* comme pilote.</span><span class="sxs-lookup"><span data-stu-id="7a55d-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as the driver.</span></span> <span data-ttu-id="7a55d-110">Consultez la [Documentation Docker Azure pilote](https://docs.docker.com/machine/drivers/azure/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="7a55d-110">For more information, see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="7a55d-111">L’exemple suivant crée une machine virtuelle nommée *myVM*, crée un compte d’utilisateur nommé *azureuser*, puis ouvre le port *80* sur la machine virtuelle hôte.</span><span class="sxs-lookup"><span data-stu-id="7a55d-111">The following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on the host VM.</span></span> <span data-ttu-id="7a55d-112">Suivez les invites pour vous connecter à votre compte Azure et accorder à Docker Machine les autorisations nécessaires pour créer et gérer des ressources.</span><span class="sxs-lookup"><span data-stu-id="7a55d-112">Follow any prompts to log in to your Azure account and grant Docker Machine permissions to create and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="7a55d-113">Le résultat ressemble à l’exemple qui suit :</span><span class="sxs-lookup"><span data-stu-id="7a55d-113">The output looks similar to the following example:</span></span>

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine to be running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH to be available...
Detecting the provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs to the local machine directory...
Copying certs to the remote machine...
Setting Docker configuration on the remote daemon...
Checking connection to Docker...
Docker is up and running!
To see how to connect your Docker Client to the Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="7a55d-114">Configurer votre interpréteur de commandes Docker</span><span class="sxs-lookup"><span data-stu-id="7a55d-114">Configure your Docker shell</span></span>
<span data-ttu-id="7a55d-115">Pour vous connecter à votre hôte Docker dans Azure, définissez les paramètres de connexion appropriés.</span><span class="sxs-lookup"><span data-stu-id="7a55d-115">To connect to your Docker host in Azure, define the appropriate connection settings.</span></span> <span data-ttu-id="7a55d-116">Entrez la commande suivante pour afficher les informations de connexion pour votre hôte Docker, comme indiqué à la fin de la sortie :</span><span class="sxs-lookup"><span data-stu-id="7a55d-116">As noted at the end of the output, view the connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="7a55d-117">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7a55d-117">The output is similar to the following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command to configure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="7a55d-118">Pour définir les paramètres de connexion, vous pouvez exécuter la commande de configuration suggérée (`eval $(docker-machine env myvmdocker)`) ou définir les variables d’environnement manuellement.</span><span class="sxs-lookup"><span data-stu-id="7a55d-118">To define the connection settings you can either run the suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set the environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="7a55d-119">Exécuter un conteneur</span><span class="sxs-lookup"><span data-stu-id="7a55d-119">Run a container</span></span>
<span data-ttu-id="7a55d-120">Pour voir un conteneur en action, vous pouvez exécuter un serveur web NGINX de base.</span><span class="sxs-lookup"><span data-stu-id="7a55d-120">To see a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="7a55d-121">Créez un conteneur avec `docker run` et exposez le port 80 au trafic web comme suit :</span><span class="sxs-lookup"><span data-stu-id="7a55d-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="7a55d-122">Le résultat ressemble à l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="7a55d-122">The output is similar to the following example:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="7a55d-123">Affichez les conteneurs en cours d’exécution en utilisant `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="7a55d-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="7a55d-124">L’exemple de sortie suivant montre le conteneur NGINX en cours d’exécution avec le port 80 exposé :</span><span class="sxs-lookup"><span data-stu-id="7a55d-124">The following example output shows the NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-the-container"></a><span data-ttu-id="7a55d-125">Tester le conteneur</span><span class="sxs-lookup"><span data-stu-id="7a55d-125">Test the container</span></span>
<span data-ttu-id="7a55d-126">Procédez comme suit pour obtenir l’adresse IP publique de l’hôte Docker :</span><span class="sxs-lookup"><span data-stu-id="7a55d-126">Obtain the public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="7a55d-127">Pour voir le conteneur en action, ouvrez un navigateur web et entrez l’adresse IP publique notée dans la sortie de la commande précédente :</span><span class="sxs-lookup"><span data-stu-id="7a55d-127">To see the container in action, open a web browser and enter the public IP address noted in the output of the preceding command:</span></span>

![Exécution d’un conteneur ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="7a55d-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7a55d-129">Next steps</span></span>
<span data-ttu-id="7a55d-130">Vous pouvez également créer des hôtes avec [l’extension de machine virtuelle Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="7a55d-130">You can also create hosts with the [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="7a55d-131">Pour obtenir des exemples sur l’utilisation de Docker Compose, consultez [Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples dans Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="7a55d-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
