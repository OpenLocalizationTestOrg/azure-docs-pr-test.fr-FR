---
title: "aaaUse Machine Docker toocreate Linux héberge dans Azure | Documents Microsoft"
description: "Décrit comment toouse Machine Docker toocreate Docker héberge dans Azure."
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
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a><span data-ttu-id="0ea50-103">Comment toouse Machine Docker toocreate héberge dans Azure</span><span class="sxs-lookup"><span data-stu-id="0ea50-103">How toouse Docker Machine toocreate hosts in Azure</span></span>
<span data-ttu-id="0ea50-104">Cet article détails comment toouse [Docker ordinateur](https://docs.docker.com/machine/) hôtes toocreate dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0ea50-104">This article details how toouse [Docker Machine](https://docs.docker.com/machine/) toocreate hosts in Azure.</span></span> <span data-ttu-id="0ea50-105">Hello `docker-machine` commande crée une machine virtuelle de Linux (VM) dans Azure, puis installe Docker.</span><span class="sxs-lookup"><span data-stu-id="0ea50-105">hello `docker-machine` command creates a Linux virtual machine (VM) in Azure then installs Docker.</span></span> <span data-ttu-id="0ea50-106">Vous pouvez ensuite gérer vos hôtes Docker dans Azure à l’aide hello mêmes outils locaux et les flux de travail.</span><span class="sxs-lookup"><span data-stu-id="0ea50-106">You can then manage your Docker hosts in Azure using hello same local tools and workflows.</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="0ea50-107">Créer des machines virtuelles avec Docker Machine</span><span class="sxs-lookup"><span data-stu-id="0ea50-107">Create VMs with Docker Machine</span></span>
<span data-ttu-id="0ea50-108">Commencez par obtenir votre ID d’abonnement Azure à l’aide de la commande [az account show](/cli/azure/account#show), comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ea50-108">First, obtain your Azure subscription ID with [az account show](/cli/azure/account#show) as follows:</span></span>

```azurecli
sub=$(az account show --query "id" -o tsv)
```

<span data-ttu-id="0ea50-109">Vous créez des machines virtuelles de hôte Docker dans Azure avec `docker-machine create` en spécifiant *azure* en tant que pilote de hello.</span><span class="sxs-lookup"><span data-stu-id="0ea50-109">You create Docker host VMs in Azure with `docker-machine create` by specifying *azure* as hello driver.</span></span> <span data-ttu-id="0ea50-110">Pour plus d’informations, consultez hello [documentation du pilote de Azure Docker](https://docs.docker.com/machine/drivers/azure/)</span><span class="sxs-lookup"><span data-stu-id="0ea50-110">For more information, see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/)</span></span>

<span data-ttu-id="0ea50-111">Hello exemple suivant crée un ordinateur virtuel nommé *myVM*, crée un compte d’utilisateur nommé *azureuser*et ouvre le port *80* sur hello héberger l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="0ea50-111">hello following example creates a VM named *myVM*, creates a user account named *azureuser*, and opens port *80* on hello host VM.</span></span> <span data-ttu-id="0ea50-112">Suivez les toolog invites dans tooyour compte Azure et accorder une Machine Docker autorisations toocreate et gérer les ressources.</span><span class="sxs-lookup"><span data-stu-id="0ea50-112">Follow any prompts toolog in tooyour Azure account and grant Docker Machine permissions toocreate and manage resources.</span></span>

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

<span data-ttu-id="0ea50-113">sortie de Hello semble similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0ea50-113">hello output looks similar toohello following example:</span></span>

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
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a><span data-ttu-id="0ea50-114">Configurer votre interpréteur de commandes Docker</span><span class="sxs-lookup"><span data-stu-id="0ea50-114">Configure your Docker shell</span></span>
<span data-ttu-id="0ea50-115">hôte de Docker tooconnect tooyour dans Azure, définissez les paramètres de connexion approprié hello.</span><span class="sxs-lookup"><span data-stu-id="0ea50-115">tooconnect tooyour Docker host in Azure, define hello appropriate connection settings.</span></span> <span data-ttu-id="0ea50-116">Comme indiqué plus haut fin hello de sortie de hello, affichez les informations de connexion hello pour l’hôte Docker comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ea50-116">As noted at hello end of hello output, view hello connection information for your Docker host as follows:</span></span> 

```bash
docker-machine env myvmdocker
```

<span data-ttu-id="0ea50-117">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0ea50-117">hello output is similar toohello following example:</span></span>

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

<span data-ttu-id="0ea50-118">Vous pouvez soit exécuter hello les paramètres de connexion toodefine hello suggéré commande de configuration (`eval $(docker-machine env myvmdocker)`), ou vous pouvez définir des variables d’environnement hello manuellement.</span><span class="sxs-lookup"><span data-stu-id="0ea50-118">toodefine hello connection settings you can either run hello suggested configuration command (`eval $(docker-machine env myvmdocker)`), or you can set hello environment variables manually.</span></span> 

## <a name="run-a-container"></a><span data-ttu-id="0ea50-119">Exécuter un conteneur</span><span class="sxs-lookup"><span data-stu-id="0ea50-119">Run a container</span></span>
<span data-ttu-id="0ea50-120">toosee un conteneur en action, vous permet d’exécuter un serveur de Web NGINX base.</span><span class="sxs-lookup"><span data-stu-id="0ea50-120">toosee a container in action, lets run a basic NGINX webserver.</span></span> <span data-ttu-id="0ea50-121">Créez un conteneur avec `docker run` et exposez le port 80 au trafic web comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ea50-121">Create a container with `docker run` and expose port 80 for web traffic as follows:</span></span>

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="0ea50-122">Hello la sortie est similaire toohello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="0ea50-122">hello output is similar toohello following example:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

<span data-ttu-id="0ea50-123">Affichez les conteneurs en cours d’exécution en utilisant `docker ps`.</span><span class="sxs-lookup"><span data-stu-id="0ea50-123">View running containers with `docker ps`.</span></span> <span data-ttu-id="0ea50-124">Hello exemple de sortie suivant affiche hello NGINX conteneur est en cours d’exécution avec le port 80 exposée :</span><span class="sxs-lookup"><span data-stu-id="0ea50-124">hello following example output shows hello NGINX container running with port 80 exposed:</span></span>

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a><span data-ttu-id="0ea50-125">Conteneur de test hello</span><span class="sxs-lookup"><span data-stu-id="0ea50-125">Test hello container</span></span>
<span data-ttu-id="0ea50-126">Obtenir les adresse IP publique hello de l’hôte Docker comme suit :</span><span class="sxs-lookup"><span data-stu-id="0ea50-126">Obtain hello public IP address of Docker host as follows:</span></span>


```bash
docker-machine ip myvmdocker
```

<span data-ttu-id="0ea50-127">conteneur de hello toosee dans action, ouvrez un navigateur web et entrez l’adresse IP publique hello noté dans la sortie de hello de hello précédant la commande :</span><span class="sxs-lookup"><span data-stu-id="0ea50-127">toosee hello container in action, open a web browser and enter hello public IP address noted in hello output of hello preceding command:</span></span>

![Exécution d’un conteneur ngnix](./media/docker-machine/nginx.png)

## <a name="next-steps"></a><span data-ttu-id="0ea50-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0ea50-129">Next steps</span></span>
<span data-ttu-id="0ea50-130">Vous pouvez également créer des ordinateurs hôtes avec hello [Extension de machine virtuelle Docker](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="0ea50-130">You can also create hosts with hello [Docker VM Extension](dockerextension.md).</span></span> <span data-ttu-id="0ea50-131">Pour obtenir des exemples sur l’utilisation de Docker Compose, consultez [Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples dans Azure](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="0ea50-131">For examples on using Docker Compose, see [Get started with Docker and Compose in Azure](docker-compose-quickstart.md).</span></span>
