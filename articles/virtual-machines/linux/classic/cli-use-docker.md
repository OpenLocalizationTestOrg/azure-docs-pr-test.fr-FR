---
title: "Utilisation de l’extension Docker VM pour Linux sur Azure"
description: "Décrit Docker et les extensions Microsoft Azure Virtual Machines, et illustre la création par programme de machines virtuelles sur Microsoft Azure qui sont des hôtes Docker à partir de la ligne de commande en utilisant l’interface de ligne de commande Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: eaff75e3-d929-4931-a4a1-8c377a8e7302
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/29/2016
ms.author: rasquill
ms.openlocfilehash: a542332c921862241f1f000e6a8f0a0ae0e8a934
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-from-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="47ffc-103">Utilisation de l’extension Docker VM à partir de l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-103">Using the Docker VM Extension from the Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="47ffc-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="47ffc-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="47ffc-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="47ffc-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="47ffc-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="47ffc-107">Pour plus d’informations sur l’utilisation de l’extension Docker VM avec le modèle Resource Manager, suivez [ce lien](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47ffc-107">For information about using the Docker VM extension with the Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="47ffc-108">Cette rubrique décrit la création d’une machine virtuelle avec l’extension Docker VM, en mode Azure Service Management (ASM) à partir de l’interface de ligne de commande Azure sur toute plateforme.</span><span class="sxs-lookup"><span data-stu-id="47ffc-108">This topic describes how to create a VM with the Docker VM Extension from the service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="47ffc-109">[Docker](https://www.docker.com/) fait partie des méthodes de virtualisation les plus prisées. Cet outil utilise des [conteneurs Linux](http://en.wikipedia.org/wiki/LXC) plutôt que des machines virtuelles pour isoler les données et le traitement sur des ressources partagées.</span><span class="sxs-lookup"><span data-stu-id="47ffc-109">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="47ffc-110">Vous pouvez utiliser l’extension Docker VM et [l’agent Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) afin de créer une machine virtuelle Docker hébergeant un nombre indéfini de conteneurs pour vos applications sur Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-110">You can use the Docker VM extension and the [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="47ffc-111">Pour une discussion sur les conteneurs et leurs avantages, consultez le [Tableau blanc Docker de haut niveau](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="47ffc-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-to-use-the-docker-vm-extension-with-azure"></a><span data-ttu-id="47ffc-112">Utilisation de l'extension Docker VM avec Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-112">How to use the Docker VM Extension with Azure</span></span>
<span data-ttu-id="47ffc-113">Pour utiliser l’extension Docker VM avec Azure, vous devez installer une version de [l’interface de ligne de commande Azure](https://github.com/Azure/azure-sdk-tools-xplat) supérieure à 0.8.6 (lors de la rédaction de ce document, la version la plus récente était 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="47ffc-113">To use the Docker VM extension with Azure, you must install a version of the [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing the current version is 0.10.0).</span></span> <span data-ttu-id="47ffc-114">Vous pouvez installer cette interface sur Mac, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="47ffc-114">You can install the Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="47ffc-115">Le processus d'utilisation de Docker sur Azure est relativement simple :</span><span class="sxs-lookup"><span data-stu-id="47ffc-115">The complete process to use Docker on Azure is simple:</span></span>

* <span data-ttu-id="47ffc-116">Installez l’interface de ligne de commande et ses dépendances sur l’ordinateur à partir duquel vous souhaitez contrôler Microsoft Azure (sur Windows, il s’agira d’une distribution Linux qui s’exécute comme une machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="47ffc-116">Install the Azure CLI and its dependencies on the computer from which you want to control Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="47ffc-117">Utiliser les commandes Docker de l’interface de ligne de commande Azure pour créer un hôte VM Docker dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-117">Use the Azure CLI Docker commands to create a VM Docker host in Azure</span></span>
* <span data-ttu-id="47ffc-118">Utilisez les commandes Docker locales pour gérer vos conteneurs dans votre machine virtuelle Docker sous Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-118">Use the local Docker commands to manage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-the-azure-command-line-interface-azure-cli"></a><span data-ttu-id="47ffc-119">Installer l’interface de ligne de commande Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-119">Install the Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="47ffc-120">Pour installer et configurer l’interface de ligne de commande Azure, consultez [Installation de l’interface de ligne de commande Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="47ffc-120">To install and configure the Azure CLI, see [How to install the Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="47ffc-121">Pour confirmer l’installation, tapez `azure` à l’invite de commandes. Après quelques secondes, l’illustration ASCII azure-cli doit normalement apparaître. Elle répertorie les commandes de base mises à votre disposition.</span><span class="sxs-lookup"><span data-stu-id="47ffc-121">To confirm the installation, type `azure` at the command prompt and after a short moment you should see the Azure CLI ASCII art, which lists the basic commands available to you.</span></span> <span data-ttu-id="47ffc-122">Si l’installation s’est déroulée correctement, vous pouvez taper `azure help vm` et voir que l’une des commandes répertoriées est « docker ».</span><span class="sxs-lookup"><span data-stu-id="47ffc-122">If the installation worked correctly, you should be able to type `azure help vm` and see that one of the listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="47ffc-123">Docker présente des outils pour Windows, [Docker Machine](https://docs.docker.com/installation/windows/), qui vous permet également d’automatiser la création d’un client Docker, à mettre à profit pour utiliser des machines virtuelles Azure en tant qu’hôtes Docker.</span><span class="sxs-lookup"><span data-stu-id="47ffc-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use to automate the creation of a docker client that you can use to work with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-the-azure-cli-to-to-your-azure-account"></a><span data-ttu-id="47ffc-124">Connecter l’interface de ligne de commande Microsoft Azure à votre compte Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-124">Connect the Azure CLI to to your Azure Account</span></span>
<span data-ttu-id="47ffc-125">Avant de pouvoir utiliser l’interface de ligne de commande Microsoft Azure, vous devez associer vos informations d’identification Microsoft Azure à l’interface sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="47ffc-125">Before you can use the Azure CLI you must associate your Azure account credentials with the Azure CLI on your platform.</span></span> <span data-ttu-id="47ffc-126">La section [Connexion à votre abonnement Azure](../../../xplat-cli-connect.md) explique comment télécharger ou importer votre fichier **.publishsettings** ou associer votre interface de ligne de commande Azure à un ID d’organisation.</span><span class="sxs-lookup"><span data-stu-id="47ffc-126">The section [How to connect to your Azure subscription](../../../xplat-cli-connect.md) explains how to either download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="47ffc-127">Le comportement diffère quelque peu selon que vous utilisez l’une ou l’autre méthode d’authentification. Veuillez donc lire attentivement le document ci-dessus pour bien comprendre les différentes fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="47ffc-127">There are some differences in behavior when using one or the other methods of authentication, so do be sure to read the document above to understand the different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-the-docker-vm-extension-for-azure"></a><span data-ttu-id="47ffc-128">Installation de Docker et utilisation de l’extension Docker VM pour Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-128">Install Docker and use the Docker VM Extension for Azure</span></span>
<span data-ttu-id="47ffc-129">Suivez les [instructions d'installation de Docker](https://docs.docker.com/installation/#installation) pour installer Docker sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="47ffc-129">Follow the [Docker installation instructions](https://docs.docker.com/installation/#installation) to install Docker locally on your computer.</span></span>

<span data-ttu-id="47ffc-130">Pour utiliser Docker avec une machine virtuelle Azure, [l’Agent de machine virtuelle Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) doit être installé dans l’image Linux utilisée pour la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="47ffc-130">To use Docker with an Azure Virtual Machine, the Linux image used for the VM must have the [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="47ffc-131">Actuellement, seuls deux types d'image le permettent :</span><span class="sxs-lookup"><span data-stu-id="47ffc-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="47ffc-132">une image Ubuntu de la galerie d'images Azure ou</span><span class="sxs-lookup"><span data-stu-id="47ffc-132">An Ubuntu image from the Azure Image Gallery or</span></span>
* <span data-ttu-id="47ffc-133">une image Linux personnalisée que vous avez créée avec l'Agent de machine virtuelle Linux Azure installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="47ffc-133">A custom Linux image that you have created with the Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="47ffc-134">Consultez [Agent de machine virtuelle Linux Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour en savoir plus sur la création d’une machine virtuelle Linux personnalisée avec l’Agent de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="47ffc-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how to build a custom Linux VM with the Azure VM Agent.</span></span>

### <a name="using-the-azure-image-gallery"></a><span data-ttu-id="47ffc-135">Utilisation de la galerie d’images Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-135">Using the Azure Image Gallery</span></span>
<span data-ttu-id="47ffc-136">Dans une session Bash ou Terminal, utilisez la commande d’interface de ligne de commande Microsoft Azure suivante pour localiser l’image Ubuntu la plus récente dans la galerie de machines virtuelles ; tapez :</span><span class="sxs-lookup"><span data-stu-id="47ffc-136">From a Bash or Terminal session, use the following Azure CLI command to locate the most recent Ubuntu image in the VM gallery to use by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="47ffc-137">Puis sélectionnez un des noms d’images (par ex. `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`) ; utilisez la commande suivante pour créer une machine virtuelle en utilisant cette image.</span><span class="sxs-lookup"><span data-stu-id="47ffc-137">and select one of the image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use the following command to create a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="47ffc-138">où :</span><span class="sxs-lookup"><span data-stu-id="47ffc-138">where:</span></span>

* <span data-ttu-id="47ffc-139">*&lt;vm-cloudservice name&gt;* est le nom de la machine virtuelle qui deviendra l’ordinateur hôte du conteneur Docker dans Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-139">*&lt;vm-cloudservice name&gt;* is the name of the VM that will become the Docker container host computer in Azure</span></span>
* <span data-ttu-id="47ffc-140">*&lt;username&gt;* est le nom de l'utilisateur racine par défaut de la machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="47ffc-140">*&lt;username&gt;* is the username of the default root user of the VM</span></span>
* <span data-ttu-id="47ffc-141">*&lt;password&gt;* est le mot de passe du compte *username* remplissant les conditions de complexité Azure</span><span class="sxs-lookup"><span data-stu-id="47ffc-141">*&lt;password&gt;* is the password of the *username* account that meets the standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="47ffc-142">Un mot de passe doit comporter au moins 8 caractères, dont une lettre minuscule et une lettre majuscule, un chiffre et un caractère spécial parmi les suivants : `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="47ffc-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of the following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="47ffc-143">Le point à la fin de la phrase précédente n'est PAS un caractère spécial.</span><span class="sxs-lookup"><span data-stu-id="47ffc-143">No, the period at the end of the preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="47ffc-144">Si la commande a été exécutée correctement, vous devriez normalement obtenir un résultat comparable à ce qui est illustré ci-dessous, suivant les arguments et options spécifiques que vous avez utilisés :</span><span class="sxs-lookup"><span data-stu-id="47ffc-144">If the command was successful, you should see something like the following, depending on the precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="47ffc-145">La création d’une machine virtuelle peut prendre quelques minutes. Cependant, une fois l’approvisionnement terminé (valeur de l’état `ReadyRole`), le démon Docker (service Docker) démarre et vous pouvez vous connecter à l’hôte du conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="47ffc-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (the state value is `ReadyRole`) the Docker daemon (the Docker service) starts and you can connect to the Docker container host.</span></span>
> 
> 

<span data-ttu-id="47ffc-146">Pour tester la machine virtuelle Docker que vous avez créée dans Azure, tapez</span><span class="sxs-lookup"><span data-stu-id="47ffc-146">To test the Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="47ffc-147">où *&lt;vm-name-you-used&gt;* est le nom de la machine virtuelle utilisée dans votre appel à `azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="47ffc-147">where *&lt;vm-name-you-used&gt;* is the name of the virtual machine that you used in your call to `azure vm docker create`.</span></span> <span data-ttu-id="47ffc-148">Ce que vous devez voir est similaire à ce qui suit ; cela indique que votre machine virtuelle hôte Docker est en service et attend vos commandes.</span><span class="sxs-lookup"><span data-stu-id="47ffc-148">You should see something similar to the following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="47ffc-149">Vous pouvez maintenant essayer de vous connecter à l’aide de votre client docker pour obtenir des informations (dans certaines configurations du client Docker, par exemple sur Mac, vous devrez peut-être utiliser `sudo`) :</span><span class="sxs-lookup"><span data-stu-id="47ffc-149">Now you can try to connect using your docker client to obtain information (in some Docker client setups, such as that on Mac, you may have to use `sudo`):</span></span>

    sudo docker --tls -H tcp://testsshasm.cloudapp.net:2376 info
    Password:
    Containers: 0
    Images: 0
    Storage Driver: devicemapper
    Pool Name: docker-8:1-131781-pool
    Pool Blocksize: 65.54 kB
    Backing Filesystem: extfs
    Data file: /dev/loop0
    Metadata file: /dev/loop1
    Data Space Used: 1.821 GB
    Data Space Total: 107.4 GB
    Data Space Available: 28 GB
    Metadata Space Used: 1.479 MB
    Metadata Space Total: 2.147 GB
    Metadata Space Available: 2.146 GB
    Udev Sync Supported: true
    Deferred Removal Enabled: false
    Data loop file: /var/lib/docker/devicemapper/devicemapper/data
    Metadata loop file: /var/lib/docker/devicemapper/devicemapper/metadata
    Library Version: 1.02.77 (2012-10-15)
    Execution Driver: native-0.2
    Logging Driver: json-file
    Kernel Version: 3.19.0-28-generic
    Operating System: Ubuntu 14.04.3 LTS
    CPUs: 1
    Total Memory: 1.637 GiB
    Name: testsshasm
    WARNING: No swap limit support

<span data-ttu-id="47ffc-150">Pour vous assurer que tout fonctionne, vous pouvez examiner la machine virtuelle pour l’extension Docker :</span><span class="sxs-lookup"><span data-stu-id="47ffc-150">Just to be certain that it's all working, you can examine the VM for the Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="47ffc-151">Authentification de la machine virtuelle hôte Docker</span><span class="sxs-lookup"><span data-stu-id="47ffc-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="47ffc-152">Outre la création de la machine virtuelle Docker, la commande `azure vm docker create` crée automatiquement les certificats nécessaires pour autoriser votre ordinateur client Docker à se connecter à l’hôte de conteneur Azure à l’aide du protocole HTTPS. Les certificats sont stockés sur les ordinateurs clients et hôtes, suivant le cas.</span><span class="sxs-lookup"><span data-stu-id="47ffc-152">In addition to creating the Docker VM, the `azure vm docker create` command also automatically creates the necessary certificates to allow your Docker client computer to connect to the Azure container host using HTTPS, and the certificates are stored on both the client and host machines, as appropriate.</span></span> <span data-ttu-id="47ffc-153">Lors des tentatives suivantes, les certificats existants sont réutilisés et partagés avec le nouvel hôte.</span><span class="sxs-lookup"><span data-stu-id="47ffc-153">On subsequent attempts, the existing certificates are reused and shared with the new host.</span></span>

<span data-ttu-id="47ffc-154">Par défaut, les certificats sont placés dans `~/.docker`, et Docker est configuré pour s’exécuter sur le port **2376**.</span><span class="sxs-lookup"><span data-stu-id="47ffc-154">By default, certificates are placed in `~/.docker`, and Docker will be configured to run on port **2376**.</span></span> <span data-ttu-id="47ffc-155">Si vous souhaitez utiliser un autre port ou répertoire, vous pouvez utiliser l’une des options de ligne de commande `azure vm docker create` suivantes afin de configurer votre machine virtuelle hôte de conteneur Docker, de telle sorte qu’elle utilise un port ou des certificats différents pour la connexion des clients :</span><span class="sxs-lookup"><span data-stu-id="47ffc-155">If you would like to use a different port or directory, then you may use one of the following `azure vm docker create` command line options to configure your Docker container host VM to use a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port to use for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="47ffc-156">Le démon Docker sur l’hôte est configuré pour écouter et authentifier les connexions client sur le port spécifié à l’aide des certificats générés par la commande `azure vm docker create` .</span><span class="sxs-lookup"><span data-stu-id="47ffc-156">The Docker daemon on the host is configured to listen for and authenticate client connections on the specified port using the certificates generated by the `azure vm docker create` command.</span></span> <span data-ttu-id="47ffc-157">L’ordinateur client doit posséder ces certificats pour avoir accès à l’hôte Docker.</span><span class="sxs-lookup"><span data-stu-id="47ffc-157">The client machine must have these certificates to gain access to the Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="47ffc-158">Un hôte en réseau qui s’exécute sans ces certificats est à la merci de toute personne capable de se connecter à l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="47ffc-158">A networked host running without these certificates will be vulnerable to anyone that can to connect to the machine.</span></span> <span data-ttu-id="47ffc-159">Avant de modifier la configuration par défaut, vous devez bien comprendre les risques auxquels sont exposés vos ordinateurs et applications.</span><span class="sxs-lookup"><span data-stu-id="47ffc-159">Before you modify the default configuration, ensure that you understand the risks to your computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="47ffc-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="47ffc-160">Next steps</span></span>
* <span data-ttu-id="47ffc-161">Vous êtes prêt à consulter le [Guide d'utilisation Docker] et à utiliser votre machine virtuelle Docker.</span><span class="sxs-lookup"><span data-stu-id="47ffc-161">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="47ffc-162">Pour créer une machine virtuelle Docker dans le nouveau portail, consultez la page [Utilisation de l'extension Docker VM avec le portail].</span><span class="sxs-lookup"><span data-stu-id="47ffc-162">To create a Docker-enabled VM in the new portal, see [How to use the Docker VM Extension with the Portal].</span></span>
* <span data-ttu-id="47ffc-163">L’extension de machine virtuelle Azure Docker prend également en charge Docker Compose, qui utilise un fichier YAML déclaratif pour utiliser une application modélisée par un développeur dans tout environnement et générer un déploiement cohérent.</span><span class="sxs-lookup"><span data-stu-id="47ffc-163">The Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file to take a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="47ffc-164">Voir [Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples sur une machine virtuelle Azure].</span><span class="sxs-lookup"><span data-stu-id="47ffc-164">See [Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How to use the Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 to another azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 to another azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md
<span data-ttu-id="47ffc-165">[Utilisation de l'extension Docker VM avec le portail]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span><span class="sxs-lookup"><span data-stu-id="47ffc-165">[How to use the Docker VM Extension with the Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/</span></span>

<span data-ttu-id="47ffc-166">[Guide d'utilisation Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="47ffc-166">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>

<span data-ttu-id="47ffc-167">[Prise en main de Docker et Compose pour définir et exécuter une application à conteneurs multiples sur une machine virtuelle Azure]:../docker-compose-quickstart.md</span><span class="sxs-lookup"><span data-stu-id="47ffc-167">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine]:../docker-compose-quickstart.md</span></span>
