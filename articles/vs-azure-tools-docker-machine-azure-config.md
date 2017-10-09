---
title: "aaaCreate Docker héberge dans Azure avec une Machine Docker | Documents Microsoft"
description: "Décrit l’utilisation des hôtes de docker toocreate Machine Docker dans Azure."
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
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a><span data-ttu-id="4a17c-103">Créer des hôtes Docker dans Azure avec Docker Machine</span><span class="sxs-lookup"><span data-stu-id="4a17c-103">Create Docker Hosts in Azure with Docker-Machine</span></span>
<span data-ttu-id="4a17c-104">En cours d’exécution [Docker](https://www.docker.com/) conteneurs requiert un démon de docker hôte machine virtuelle en cours d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="4a17c-104">Running [Docker](https://www.docker.com/) containers requires a host VM running hello docker daemon.</span></span>
<span data-ttu-id="4a17c-105">Cette rubrique décrit comment toouse hello [docker-machine](https://docs.docker.com/machine/) commande toocreate nouvelles machines virtuelles Linux, configuré avec hello démon Docker, s’exécutant dans Azure.</span><span class="sxs-lookup"><span data-stu-id="4a17c-105">This topic describes how toouse hello [docker-machine](https://docs.docker.com/machine/) command toocreate new Linux VMs, configured with hello Docker daemon, running in Azure.</span></span> 

<span data-ttu-id="4a17c-106">**Remarque :**</span><span class="sxs-lookup"><span data-stu-id="4a17c-106">**Note:**</span></span> 

* <span data-ttu-id="4a17c-107">*Cet article suppose que la version de docker-machine est 0.9.0-rc2 ou une version supérieure*</span><span class="sxs-lookup"><span data-stu-id="4a17c-107">*This article depends on docker-machine version 0.9.0-rc2 or greater*</span></span>
* <span data-ttu-id="4a17c-108">*Les conteneurs Windows sera être pris en charge via docker-machine Bonjour futur proche*</span><span class="sxs-lookup"><span data-stu-id="4a17c-108">*Windows Containers will be supported through docker-machine in hello near future*</span></span>

## <a name="create-vms-with-docker-machine"></a><span data-ttu-id="4a17c-109">Créer des machines virtuelles avec Docker Machine</span><span class="sxs-lookup"><span data-stu-id="4a17c-109">Create VMs with Docker Machine</span></span>
<span data-ttu-id="4a17c-110">Créer des machines virtuelles hôtes docker dans Azure avec hello `docker-machine create` commande à l’aide de hello `azure` pilote.</span><span class="sxs-lookup"><span data-stu-id="4a17c-110">Create docker host VMs in Azure with hello `docker-machine create` command using hello `azure` driver.</span></span> 

<span data-ttu-id="4a17c-111">Hello pilote Azure nécessite votre ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4a17c-111">hello Azure driver requires your subscription ID.</span></span> <span data-ttu-id="4a17c-112">Vous pouvez utiliser hello [CLI d’Azure](cli-install-nodejs.md) ou hello [Azure Portal](https://portal.azure.com) tooretrieve votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4a17c-112">You can use hello [Azure CLI](cli-install-nodejs.md) or hello [Azure Portal](https://portal.azure.com) tooretrieve your Azure Subscription.</span></span> 

<span data-ttu-id="4a17c-113">**À l’aide de hello portail Azure**</span><span class="sxs-lookup"><span data-stu-id="4a17c-113">**Using hello Azure Portal**</span></span>

* <span data-ttu-id="4a17c-114">Sélectionnez **abonnements** de hello de navigation gauche page et copie hello id d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="4a17c-114">Select **Subscriptions** from hello left navigation page and copy hello subscription id.</span></span>

<span data-ttu-id="4a17c-115">**À l’aide de hello CLI d’Azure**</span><span class="sxs-lookup"><span data-stu-id="4a17c-115">**Using hello Azure CLI**</span></span>

* <span data-ttu-id="4a17c-116">Type ```azure account list``` et id d’abonnement copie hello.</span><span class="sxs-lookup"><span data-stu-id="4a17c-116">Type ```azure account list``` and copy hello subscription id.</span></span>

<span data-ttu-id="4a17c-117">Type `docker-machine create --driver azure` toosee hello options et leurs valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="4a17c-117">Type `docker-machine create --driver azure` toosee hello options and their default values.</span></span>
<span data-ttu-id="4a17c-118">Vous pouvez également voir hello [documentation du pilote de Azure Docker](https://docs.docker.com/machine/drivers/azure/) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4a17c-118">You can also see hello [Docker Azure Driver documentation](https://docs.docker.com/machine/drivers/azure/) for more info.</span></span> 

<span data-ttu-id="4a17c-119">Hello exemple suivant s’appuie sur hello [les valeurs par défaut](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), mais définit ces valeurs si vous le souhaitez :</span><span class="sxs-lookup"><span data-stu-id="4a17c-119">hello following example relies upon hello [default values](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), but it does optionally set these values:</span></span> 

* <span data-ttu-id="4a17c-120">Azure dns pour le nom hello associé hello adresse IP publique et les certificats générés.</span><span class="sxs-lookup"><span data-stu-id="4a17c-120">azure-dns for hello name associated with hello public IP and certificates generated.</span></span> <span data-ttu-id="4a17c-121">Il s’agit de nom DNS de hello de votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4a17c-121">This is hello DNS name of your virtual machine.</span></span> <span data-ttu-id="4a17c-122">Hello machine virtuelle peut alors en toute sécurité arrêter, libérer hello dynamiques d’adresse IP et de fournir hello capacité tooreconnect après le démarrage de machine virtuelle de hello à nouveau avec une nouvelle adresse IP.</span><span class="sxs-lookup"><span data-stu-id="4a17c-122">hello VM can then safely stop, release hello dynamic IP, and provide hello ability tooreconnect after hello vm starts again with a new IP.</span></span> <span data-ttu-id="4a17c-123">préfixe de nom Hello doit être unique pour cette région UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="4a17c-123">hello name prefix must be unique for that region  UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.</span></span>
* <span data-ttu-id="4a17c-124">ouvrir le port 80 sur hello machine virtuelle pour l’accès internet sortant</span><span class="sxs-lookup"><span data-stu-id="4a17c-124">open port 80 on hello VM for outbound internet access</span></span>
* <span data-ttu-id="4a17c-125">taille de stockage premium plus rapide de VM tooutilize de hello</span><span class="sxs-lookup"><span data-stu-id="4a17c-125">size of hello VM tooutilize faster premium storage</span></span>
* <span data-ttu-id="4a17c-126">stockage Premium utilisé pour le disque de machine virtuelle hello</span><span class="sxs-lookup"><span data-stu-id="4a17c-126">premium storage used for hello vm disk</span></span>

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a><span data-ttu-id="4a17c-127">Choisissez un hôte Docker avec docker-machine</span><span class="sxs-lookup"><span data-stu-id="4a17c-127">Choose a docker host with docker-machine</span></span>
<span data-ttu-id="4a17c-128">Une fois que vous avez une entrée dans une machine docker pour votre ordinateur hôte, vous pouvez définir hôte par défaut de hello lors de l’exécution des commandes docker.</span><span class="sxs-lookup"><span data-stu-id="4a17c-128">Once you have an entry in docker-machine for your host, you can set hello default host when running docker commands.</span></span>

## <a name="using-powershell"></a><span data-ttu-id="4a17c-129">Utiliser PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a17c-129">Using PowerShell</span></span>
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a><span data-ttu-id="4a17c-130">Avec Bash</span><span class="sxs-lookup"><span data-stu-id="4a17c-130">Using Bash</span></span>
```bash
eval $(docker-machine env MyDockerHost)
```

<span data-ttu-id="4a17c-131">Vous pouvez maintenant exécuter des commandes docker sur l’hôte spécifié hello</span><span class="sxs-lookup"><span data-stu-id="4a17c-131">You can now run docker commands against hello specified host</span></span>

```
docker ps
docker info
```

## <a name="run-a-container"></a><span data-ttu-id="4a17c-132">Exécuter un conteneur</span><span class="sxs-lookup"><span data-stu-id="4a17c-132">Run a container</span></span>
<span data-ttu-id="4a17c-133">Avec un hôte configuré, vous pouvez maintenant exécuter un tootest de serveur web simple si votre hôte n’a été configuré correctement.</span><span class="sxs-lookup"><span data-stu-id="4a17c-133">With a host configured, you can now run a simple web server tootest whether your host was configured correctly.</span></span>
<span data-ttu-id="4a17c-134">Ici nous allons utiliser une image standard nginx, spécifiez qu’il doit écouter sur le port 80, et que si le redémarrage de la machine virtuelle d’hôte hello, conteneur de hello redémarrent également (`--restart=always`).</span><span class="sxs-lookup"><span data-stu-id="4a17c-134">Here we use a standard nginx image, specify that it should listen on port 80, and that if hello host VM restarts, hello container will restart as well (`--restart=always`).</span></span> 

```bash
docker run -d -p 80:80 --restart=always nginx
```

<span data-ttu-id="4a17c-135">sortie de Hello doit ressembler à hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="4a17c-135">hello output should look something like hello following:</span></span>

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a><span data-ttu-id="4a17c-136">Conteneur de test hello</span><span class="sxs-lookup"><span data-stu-id="4a17c-136">Test hello container</span></span>
<span data-ttu-id="4a17c-137">Examinez les conteneurs en cours d'exécution en utilisant `docker ps`:</span><span class="sxs-lookup"><span data-stu-id="4a17c-137">Examine running containers using `docker ps`:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

<span data-ttu-id="4a17c-138">Et hello toosee en cours d’exécution du conteneur, type `docker-machine ip <VM name>` toofind hello le tooenter d’adresse IP dans le navigateur de hello :</span><span class="sxs-lookup"><span data-stu-id="4a17c-138">And, toosee hello running container, type `docker-machine ip <VM name>` toofind hello IP address tooenter in hello browser:</span></span>

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Exécution d’un conteneur ngnix](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a><span data-ttu-id="4a17c-140">Résumé</span><span class="sxs-lookup"><span data-stu-id="4a17c-140">Summary</span></span>
<span data-ttu-id="4a17c-141">Avec docker-machine, vous pouvez facilement approvisionner des hôtes Docker dans Azure pour chacune de vos validations d’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="4a17c-141">With docker-machine, you can easily provision docker hosts in Azure for your individual docker host validations.</span></span>
<span data-ttu-id="4a17c-142">Pour la production d’hébergement de conteneurs, consultez hello [Service de conteneur Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="4a17c-142">For production hosting of containers, see hello [Azure Container Service](http://aka.ms/AzureContainerService)</span></span>

<span data-ttu-id="4a17c-143">toodevelop .NET des Applications de base avec Visual Studio, consultez [outils Docker pour Visual Studio](http://aka.ms/DockerToolsForVS)</span><span class="sxs-lookup"><span data-stu-id="4a17c-143">toodevelop .NET Core Applications with Visual Studio, see [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)</span></span>

