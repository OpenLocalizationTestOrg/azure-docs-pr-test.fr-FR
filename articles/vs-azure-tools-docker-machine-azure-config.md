---
title: "Créer des hôtes Docker dans Azure avec Docker Machine | Microsoft Docs"
description: "Décrit l'utilisation de Docker Machine pour créer des hôtes Docker dans Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: 766d327a87ed13e04166d71c3d9ae0a1e7a66d19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="af7b0-103">Créer des hôtes Docker dans Azure avec Docker Machine</span><span class="sxs-lookup"><span data-stu-id="af7b0-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="af7b0-104">L’exécution de conteneurs [Docker](https://www.docker.com/) nécessite une machine virtuelle hôte exécutant le démon Docker.</span><span class="sxs-lookup"><span data-stu-id="af7b0-104">Running [Docker](https://www.docker.com/) containers requires a host VM running the docker daemon.</span></span>
<span data-ttu-id="af7b0-105">Cette rubrique décrit comment utiliser la commande [docker-machine](https://docs.docker.com/machine/) pour créer des machines virtuelles Linux, configurées avec le démon Docker et s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="af7b0-105">This topic describes how to use the [docker-machine](https://docs.docker.com/machine/) command to create new Linux VMs, configured with the Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="af7b0-106">**Remarque :**</span><span class="sxs-lookup"><span data-stu-id="af7b0-106">**Note:**</span></span> 

* <span data-ttu-id="af7b0-107">*Cet article suppose que la version de docker-machine est 0.9.0-rc2 ou une version supérieure*</span><span class="sxs-lookup"><span data-stu-id="af7b0-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="af7b0-108">*Les conteneurs Windows seront prochainement pris en charge avec docker-machine*</span><span class="sxs-lookup"><span data-stu-id="af7b0-108">*Windows Containers will be supported through docker-machine in the near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="af7b0-109">Créer des machines virtuelles avec Docker Machine</span><span class="sxs-lookup"><span data-stu-id="af7b0-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="af7b0-110">Créez des machines virtuelles d’hôte Docker sans Azure avec la commande `docker-machine create` en utilisant le pilote `azure`.</span><span class="sxs-lookup"><span data-stu-id="af7b0-110">Create docker host VMs in Azure with the `docker-machine create` command using the `azure` driver.</span></span> 

<span data-ttu-id="af7b0-111">Le pilote Azure nécessite votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="af7b0-111">The Azure driver requires your subscription ID.</span></span> <span data-ttu-id="af7b0-112">Vous pouvez utiliser l’[interface de ligne de commande Azure](cli-install-nodejs.md) ou le [Portail Azure](https://portal.azure.com) pour récupérer votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="af7b0-112">You can use the [Azure CLI](cli-install-nodejs.md) or the [Azure Portal](https://portal.azure.com) to retrieve your Azure Subscription.</span></span> 

<span data-ttu-id="af7b0-113">**Utilisation du portail Azure**</span><span class="sxs-lookup"><span data-stu-id="af7b0-113">**Using the Azure Portal**</span></span>

* <span data-ttu-id="af7b0-114">Sélectionnez **Abonnements** dans la page de navigation de gauche, puis copiez l’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="af7b0-114">Select **Subscriptions** from the left navigation page and copy the subscription id.</span></span>

<span data-ttu-id="af7b0-115">**Utilisation de l’interface de ligne de commande Azure (CLI)**</span><span class="sxs-lookup"><span data-stu-id="af7b0-115">**Using the Azure CLI**</span></span>

* <span data-ttu-id="af7b0-116">Saisissez ```azure account list``` et copiez l’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="af7b0-116">Type ```azure account list``` and copy the subscription id.</span></span>

<span data-ttu-id="af7b0-117">Saisissez `docker-machine create --driver azure` pour afficher les options et leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="af7b0-117">Type `docker-machine create --driver azure` to see the options and their default values.</span></span>
<span data-ttu-id="af7b0-118">Vous pouvez également consulter la [Documentation Docker Azure pilote](https://docs.docker.com/machine/drivers/azure/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="af7b0-118">You can also see the [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="af7b0-119">L’exemple suivant repose sur les [valeurs par défaut](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mais il définit de façon facultative les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="af7b0-119">The following example relies upon the [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="af7b0-120">azure-dns pour le nom associé à l’adresse IP publique et aux certificats générés.</span><span class="sxs-lookup"><span data-stu-id="af7b0-120">azure-dns for the name associated with the public IP and certificates generated.</span></span> <span data-ttu-id="af7b0-121">Il s’agit du nom DNS de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="af7b0-121">This is the DNS name of your virtual machine.</span></span> <span data-ttu-id="af7b0-122">La machine virtuelle peut alors être éteinte en toute sécurité, libérer l’adresse IP dynamique et donner la possibilité de se reconnecter après le redémarrage de la machine virtuelle avec une nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="af7b0-122">The VM can then safely stop, release the dynamic IP, and provide the ability to reconnect after the vm starts again with a new IP.</span></span> <span data-ttu-id="af7b0-123">Le préfixe du nom doit être unique pour cette région UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="af7b0-123">The name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="af7b0-124">Ouverture du port 80 sur la machine virtuelle pour l’accès sortant à Internet</span><span class="sxs-lookup"><span data-stu-id="af7b0-124">open port 80 on the VM for outbound internet access</span></span>
* <span data-ttu-id="af7b0-125">Taille de la machine virtuelle pour utiliser le stockage Premium plus rapide</span><span class="sxs-lookup"><span data-stu-id="af7b0-125">size of the VM to utilize faster premium storage</span></span>
* <span data-ttu-id="af7b0-126">Stockage Premium utilisé pour le disque de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="af7b0-126">premium storage used for the vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="af7b0-127">Choisissez un hôte Docker avec docker-machine</span><span class="sxs-lookup"><span data-stu-id="af7b0-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="af7b0-128">Une fois que vous avez une entrée dans docker-machine pour votre hôte, vous pouvez définir l’hôte par défaut lorsque vous exécutez des commandes Docker.</span><span class="sxs-lookup"><span data-stu-id="af7b0-128">Once you have an entry in docker-machine for your host, you can set the default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="af7b0-129">Utiliser PowerShell</span><span class="sxs-lookup"><span data-stu-id="af7b0-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="af7b0-130">Avec Bash</span><span class="sxs-lookup"><span data-stu-id="af7b0-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="af7b0-131">Vous pouvez maintenant exécuter des commandes Docker sur l’hôte spécifié</span><span class="sxs-lookup"><span data-stu-id="af7b0-131">You can now run docker commands against the specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="af7b0-132">Exécuter un conteneur</span><span class="sxs-lookup"><span data-stu-id="af7b0-132">Run a container</span></span>
<span data-ttu-id="af7b0-133">Avec un hôte configuré, vous pouvez maintenant exécuter un serveur web simple pour vérifier si votre hôte a bien été configuré.</span><span class="sxs-lookup"><span data-stu-id="af7b0-133">With a host configured, you can now run a simple web server to test whether your host was configured correctly.</span></span>
<span data-ttu-id="af7b0-134">Comme nous utilisons ici une image nginx standard, spécifiez que le serveur doit écouter sur le port 80, et que si la machine virtuelle hôte redémarre, le conteneur redémarre également (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="af7b0-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if the host VM restarts, the container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="af7b0-135">La sortie doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="af7b0-135">The output should look something like the following:</span></span>

```
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-the-container"></a><span data-ttu-id="af7b0-136">Tester le conteneur</span><span class="sxs-lookup"><span data-stu-id="af7b0-136">Test the container</span></span>
<span data-ttu-id="af7b0-137">Examinez les conteneurs en cours d'exécution en utilisant `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="af7b0-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="af7b0-138">Pour connaître le conteneur en cours d’exécution, saisissez `docker-machine ip <VM name>` pour rechercher l’adresse IP à saisir dans le navigateur :</span><span class="sxs-lookup"><span data-stu-id="af7b0-138">And, to see the running container, type `docker-machine ip <VM name>` to find the IP address to enter in the browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Exécution d’un conteneur ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="af7b0-140">Résumé</span><span class="sxs-lookup"><span data-stu-id="af7b0-140">Summary</span></span>
<span data-ttu-id="af7b0-141">Avec docker-machine, vous pouvez facilement approvisionner des hôtes Docker dans Azure pour chacune de vos validations d’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="af7b0-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="af7b0-142">Pour l’hébergement de production de conteneurs, consultez le [Service de conteneur Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="af7b0-142">For production hosting of containers, see the [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="af7b0-143">Pour développer des applications .NET Core avec Visual Studio, consultez [Outils Docker pour Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="af7b0-143">To develop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

