---
title: aaaUsing hello Extension de machine virtuelle Docker pour Linux sur Azure
description: "Décrit les Docker et les extensions de Machines virtuelles Azure hello et montre comment tooprogrammatically créer des Machines virtuelles sur Azure qui sont des hôtes de docker à partir de la ligne de commande hello à l’aide de hello CLI d’Azure."
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
ms.openlocfilehash: 1e192ad7c273aa9c997ea7bfa53b7de0b41a43c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-from-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="13021-103">À l’aide de hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)</span><span class="sxs-lookup"><span data-stu-id="13021-103">Using hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="13021-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="13021-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="13021-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="13021-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="13021-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="13021-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="13021-107">Pour plus d’informations sur l’utilisation d’extension de machine virtuelle de Docker hello avec modèle de gestionnaire de ressources hello, consultez [ici](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="13021-107">For information about using hello Docker VM extension with hello Resource Manager model, see [here](../dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="13021-108">Cette rubrique décrit comment toocreate une machine virtuelle avec hello Extension de machine virtuelle Docker à partir de hello service en mode de gestion (asm) dans Azure CLI sur n’importe quelle plateforme.</span><span class="sxs-lookup"><span data-stu-id="13021-108">This topic describes how toocreate a VM with hello Docker VM Extension from hello service management (asm) mode in Azure CLI on any platform.</span></span> <span data-ttu-id="13021-109">[Docker](https://www.docker.com/) d'entre hello est la virtualisation qui utilise les plus populaires [les conteneurs Linux](http://en.wikipedia.org/wiki/LXC) plutôt que des machines virtuelles comme un moyen d’isoler les données et le calcul sur des ressources partagées.</span><span class="sxs-lookup"><span data-stu-id="13021-109">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="13021-110">Vous pouvez utiliser l’extension de machine virtuelle de Docker hello et de hello [Linux Agent Azure](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate une machine virtuelle Docker qui héberge un nombre quelconque de conteneurs pour vos applications sur Azure.</span><span class="sxs-lookup"><span data-stu-id="13021-110">You can use hello Docker VM extension and hello [Azure Linux Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span> <span data-ttu-id="13021-111">toosee une description détaillée des conteneurs et leurs avantages, consultez hello [tableau blanc de niveau élevé Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="13021-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>

## <a name="how-toouse-hello-docker-vm-extension-with-azure"></a><span data-ttu-id="13021-112">Comment toouse hello Extension de machine virtuelle Docker avec Azure</span><span class="sxs-lookup"><span data-stu-id="13021-112">How toouse hello Docker VM Extension with Azure</span></span>
<span data-ttu-id="13021-113">extension de machine virtuelle de Docker toouse hello avec Azure, vous devez installer une version de hello [Interface de ligne de commande Azure](https://github.com/Azure/azure-sdk-tools-xplat) (CLI d’Azure) supérieur 0.8.6 (comme ce Hello écrit la version actuelle est 0.10.0).</span><span class="sxs-lookup"><span data-stu-id="13021-113">toouse hello Docker VM extension with Azure, you must install a version of hello [Azure Command-Line Interface](https://github.com/Azure/azure-sdk-tools-xplat) (Azure CLI) higher than 0.8.6 (as of this writing hello current version is 0.10.0).</span></span> <span data-ttu-id="13021-114">Vous pouvez installer hello CLI d’Azure sur le Mac, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="13021-114">You can install hello Azure CLI on Mac, Linux, and Windows.</span></span>

<span data-ttu-id="13021-115">Terminer le processus de Hello toouse Docker sur Azure est simple :</span><span class="sxs-lookup"><span data-stu-id="13021-115">hello complete process toouse Docker on Azure is simple:</span></span>

* <span data-ttu-id="13021-116">Installer hello CLI d’Azure et ses dépendances sur ordinateur hello à partir desquels vous souhaitez toocontrol Azure (sous Windows, ce sera une distribution Linux en cours d’exécution comme une machine virtuelle)</span><span class="sxs-lookup"><span data-stu-id="13021-116">Install hello Azure CLI and its dependencies on hello computer from which you want toocontrol Azure (on Windows, this will be a Linux distribution running as a virtual machine)</span></span>
* <span data-ttu-id="13021-117">Utiliser hello Azure CLI Docker commandes toocreate un hôte Docker de machine virtuelle dans Azure</span><span class="sxs-lookup"><span data-stu-id="13021-117">Use hello Azure CLI Docker commands toocreate a VM Docker host in Azure</span></span>
* <span data-ttu-id="13021-118">Utilisez hello local Docker commandes toomanage vos conteneurs Docker dans votre machine virtuelle de Docker dans Azure.</span><span class="sxs-lookup"><span data-stu-id="13021-118">Use hello local Docker commands toomanage your Docker containers in your Docker VM in Azure.</span></span>

### <a name="install-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="13021-119">Installer hello Azure Interface de ligne (Azure)</span><span class="sxs-lookup"><span data-stu-id="13021-119">Install hello Azure Command-Line Interface (Azure CLI)</span></span>
<span data-ttu-id="13021-120">tooinstall et configurer hello CLI d’Azure, consultez [comment tooinstall hello Interface de ligne de commande Azure](../../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="13021-120">tooinstall and configure hello Azure CLI, see [How tooinstall hello Azure Command-Line Interface](../../../cli-install-nodejs.md).</span></span> <span data-ttu-id="13021-121">installation de hello tooconfirm, type `azure` à l’invite de commande hello et après un court instant, vous devez voir hello art Azure CLI ASCII, qui répertorie les basic de hello commandes tooyou disponible.</span><span class="sxs-lookup"><span data-stu-id="13021-121">tooconfirm hello installation, type `azure` at hello command prompt and after a short moment you should see hello Azure CLI ASCII art, which lists hello basic commands available tooyou.</span></span> <span data-ttu-id="13021-122">Si l’installation de hello fonctionne correctement, vous devez être en mesure de tootype `azure help vm` et qu’une des commandes de hello répertorié est « docker ».</span><span class="sxs-lookup"><span data-stu-id="13021-122">If hello installation worked correctly, you should be able tootype `azure help vm` and see that one of hello listed commands is "docker".</span></span>

> [!NOTE]
> <span data-ttu-id="13021-123">Docker a des outils pour Windows, [Docker Machine](https://docs.docker.com/installation/windows/), qui vous permet également la création de hello tooautomate d’un client docker que vous pouvez utiliser toowork avec des machines virtuelles Azure en tant qu’hôtes de docker.</span><span class="sxs-lookup"><span data-stu-id="13021-123">Docker has tools for Windows, [Docker Machine](https://docs.docker.com/installation/windows/), which you can also use tooautomate hello creation of a docker client that you can use toowork with Azure VMs as docker hosts.</span></span>
> 
> 

### <a name="connect-hello-azure-cli-tootooyour-azure-account"></a><span data-ttu-id="13021-124">Se connecter hello CLI d’Azure tootooyour compte Azure</span><span class="sxs-lookup"><span data-stu-id="13021-124">Connect hello Azure CLI tootooyour Azure Account</span></span>
<span data-ttu-id="13021-125">Avant de pouvoir utiliser hello CLI d’Azure, vous devez associer vos informations d’identification de compte Azure avec hello CLI d’Azure sur votre plateforme.</span><span class="sxs-lookup"><span data-stu-id="13021-125">Before you can use hello Azure CLI you must associate your Azure account credentials with hello Azure CLI on your platform.</span></span> <span data-ttu-id="13021-126">Hello section [comment tooconnect tooyour abonnement Azure](../../../xplat-cli-connect.md) explique comment tooeither télécharger et importer votre **.publishsettings** de fichiers ou d’associer votre CLI d’Azure avec un id d’organisation.</span><span class="sxs-lookup"><span data-stu-id="13021-126">hello section [How tooconnect tooyour Azure subscription](../../../xplat-cli-connect.md) explains how tooeither download and import your **.publishsettings** file or associate your Azure CLI with an organizational id.</span></span>

> [!NOTE]
> <span data-ttu-id="13021-127">Il existe quelques différences de comportement lorsque l’un ou hello autres méthodes d’authentification, donc que tooread hello document au-dessus des fonctionnalités différentes toounderstand hello.</span><span class="sxs-lookup"><span data-stu-id="13021-127">There are some differences in behavior when using one or hello other methods of authentication, so do be sure tooread hello document above toounderstand hello different functionality.</span></span>
> 
> 

### <a name="install-docker-and-use-hello-docker-vm-extension-for-azure"></a><span data-ttu-id="13021-128">Installer Docker et utiliser hello Extension de machine virtuelle Docker pour Azure</span><span class="sxs-lookup"><span data-stu-id="13021-128">Install Docker and use hello Docker VM Extension for Azure</span></span>
<span data-ttu-id="13021-129">Suivez hello [des instructions d’installation Docker](https://docs.docker.com/installation/#installation) tooinstall Docker localement sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="13021-129">Follow hello [Docker installation instructions](https://docs.docker.com/installation/#installation) tooinstall Docker locally on your computer.</span></span>

<span data-ttu-id="13021-130">toouse Docker avec une Machine virtuelle de Azure, image de Linux hello utilisé pour hello machine virtuelle doit disposer de hello [Agent de machine virtuelle Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installé.</span><span class="sxs-lookup"><span data-stu-id="13021-130">toouse Docker with an Azure Virtual Machine, hello Linux image used for hello VM must have hello [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) installed.</span></span> <span data-ttu-id="13021-131">Actuellement, seuls deux types d'image le permettent :</span><span class="sxs-lookup"><span data-stu-id="13021-131">Currently, there are only two types of images that provide this:</span></span>

* <span data-ttu-id="13021-132">Une image de Ubuntu à partir de la galerie d’images Azure de hello ou</span><span class="sxs-lookup"><span data-stu-id="13021-132">An Ubuntu image from hello Azure Image Gallery or</span></span>
* <span data-ttu-id="13021-133">Une image personnalisée de Linux que vous avez créés avec hello Agent de machine virtuelle Azure Linux installé et configuré.</span><span class="sxs-lookup"><span data-stu-id="13021-133">A custom Linux image that you have created with hello Azure Linux VM Agent installed and configured.</span></span> <span data-ttu-id="13021-134">Consultez [Agent de machine virtuelle Azure Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations sur la façon toobuild une VM Linux personnalisé avec hello Agent de machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="13021-134">See [Azure Linux VM Agent](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about how toobuild a custom Linux VM with hello Azure VM Agent.</span></span>

### <a name="using-hello-azure-image-gallery"></a><span data-ttu-id="13021-135">À l’aide de la galerie d’images Azure hello</span><span class="sxs-lookup"><span data-stu-id="13021-135">Using hello Azure Image Gallery</span></span>
<span data-ttu-id="13021-136">À partir d’un interpréteur de commandes ou une session Terminal Server, utilisez hello commande CLI d’Azure toolocate hello image la plus récente Ubuntu dans toouse de la galerie de machine virtuelle hello en tapant suivante</span><span class="sxs-lookup"><span data-stu-id="13021-136">From a Bash or Terminal session, use hello following Azure CLI command toolocate hello most recent Ubuntu image in hello VM gallery toouse by typing</span></span>

`azure vm image list | grep Ubuntu-14_04`

<span data-ttu-id="13021-137">Sélectionnez un des noms d’images hello, tels que `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, et des commandes suivantes de hello utilisation toocreate un nouvel ordinateur virtuel à l’aide de cette image.</span><span class="sxs-lookup"><span data-stu-id="13021-137">and select one of hello image names, such as `b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB`, and use hello following command toocreate a new VM using that image.</span></span>

```
azure vm docker create -e 22 -l "West US" <vm-cloudservice name> "b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB" <username> <password>
```

<span data-ttu-id="13021-138">où :</span><span class="sxs-lookup"><span data-stu-id="13021-138">where:</span></span>

* <span data-ttu-id="13021-139">*&lt;nom de la machine virtuelle-cloudservice&gt;*  hello désigne hello machine virtuelle qui deviendra ordinateur d’hôte de conteneur d’hello Docker dans Azure</span><span class="sxs-lookup"><span data-stu-id="13021-139">*&lt;vm-cloudservice name&gt;* is hello name of hello VM that will become hello Docker container host computer in Azure</span></span>
* <span data-ttu-id="13021-140">*&lt;nom d’utilisateur&gt;*  est username hello d’utilisateur de racine par défaut hello Hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="13021-140">*&lt;username&gt;* is hello username of hello default root user of hello VM</span></span>
* <span data-ttu-id="13021-141">*&lt;mot de passe&gt;*  est un mot de passe hello Hello *nom d’utilisateur* compte qui répond aux normes hello de complexité pour Azure</span><span class="sxs-lookup"><span data-stu-id="13021-141">*&lt;password&gt;* is hello password of hello *username* account that meets hello standards of complexity for Azure</span></span>

> [!NOTE]
> <span data-ttu-id="13021-142">Actuellement, un mot de passe doit comporter au moins 8 caractères, contenir une lettre minuscule et une lettre majuscule, un nombre et un caractère spécial, tel que celui de hello les caractères suivants : `!@#$%^&+=`.</span><span class="sxs-lookup"><span data-stu-id="13021-142">Currently, a password must be at least 8 characters, contain one lower case and one upper case character, a number, and a special character such as one of hello following characters: `!@#$%^&+=`.</span></span> <span data-ttu-id="13021-143">Non, la période de hello à fin hello Hello précédant la phrase n’est pas un caractère spécial.</span><span class="sxs-lookup"><span data-stu-id="13021-143">No, hello period at hello end of hello preceding sentence is NOT a special character.</span></span>
> 
> 

<span data-ttu-id="13021-144">Si la commande hello a réussi, vous devez voir quelque chose comme hello suivantes, selon les arguments précis hello et options que vous avez utilisé :</span><span class="sxs-lookup"><span data-stu-id="13021-144">If hello command was successful, you should see something like hello following, depending on hello precise arguments and options you used:</span></span>

![](media/cli-use-docker/dockercreateresults.png)

> [!NOTE]
> <span data-ttu-id="13021-145">Création d’un ordinateur virtuel peut prendre quelques minutes, mais une fois que ce dernier a été configuré (valeur d’état hello est `ReadyRole`) hello démarre le démon (service Docker de hello) de Docker et vous pouvez vous connecter hôte de conteneur Docker toohello.</span><span class="sxs-lookup"><span data-stu-id="13021-145">Creating a virtual machine can take a few minutes, but after it has been provisioned (hello state value is `ReadyRole`) hello Docker daemon (hello Docker service) starts and you can connect toohello Docker container host.</span></span>
> 
> 

<span data-ttu-id="13021-146">tootest hello virtuelle Docker que vous avez créé dans Azure, type</span><span class="sxs-lookup"><span data-stu-id="13021-146">tootest hello Docker VM you have created in Azure, type</span></span>

`docker --tls -H tcp://<vm-name-you-used>.cloudapp.net:2376 info`

<span data-ttu-id="13021-147">où  *&lt;vm-nom-vous-utilisé&gt;*  est le nom hello de machine virtuelle hello que vous avez utilisé dans votre appel trop`azure vm docker create`.</span><span class="sxs-lookup"><span data-stu-id="13021-147">where *&lt;vm-name-you-used&gt;* is hello name of hello virtual machine that you used in your call too`azure vm docker create`.</span></span> <span data-ttu-id="13021-148">Vous devez voir quelque chose de similaire suivant toohello, ce qui indique que votre machine virtuelle d’hôte Docker est disponible et en cours d’exécution dans Azure et en attente de vos commandes.</span><span class="sxs-lookup"><span data-stu-id="13021-148">You should see something similar toohello following, which indicates that your Docker Host VM is up and running in Azure and waiting for your commands.</span></span> 

<span data-ttu-id="13021-149">Maintenant vous pouvez essayer de tooconnect à l’aide de vos informations de tooobtain client docker (dans certaines configurations de client Docker, tel que sur un Mac, vous devrez peut-être toouse `sudo`) :</span><span class="sxs-lookup"><span data-stu-id="13021-149">Now you can try tooconnect using your docker client tooobtain information (in some Docker client setups, such as that on Mac, you may have toouse `sudo`):</span></span>

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

<span data-ttu-id="13021-150">Simplement toobe certain qu’il s’agit d’utilisation, vous pouvez examiner hello VM pour hello extension Docker :</span><span class="sxs-lookup"><span data-stu-id="13021-150">Just toobe certain that it's all working, you can examine hello VM for hello Docker extension:</span></span>

    azure vm extension get testsshasm
    info: Executing command vm extension get
    + Getting virtual machines
    data: Publisher Extension name ReferenceName Version State
    data: -------------------- --------------- ------------------------- ------- ------
    data: Microsoft.Azure.E... DockerExtension DockerExtension 1.* Enable
    info: vm extension get command OK

### <a name="docker-host-vm-authentication"></a><span data-ttu-id="13021-151">Authentification de la machine virtuelle hôte Docker</span><span class="sxs-lookup"><span data-stu-id="13021-151">Docker Host VM Authentication</span></span>
<span data-ttu-id="13021-152">En outre toocreating hello machine virtuelle Docker, hello `azure vm docker create` commande crée également automatiquement hello certificats nécessaires tooallow votre Docker client ordinateur tooconnect toohello Azure hôte de conteneur à l’aide de HTTPS, et les certificats hello sont stockés sur les deux Bonjour les ordinateurs clients et hôtes, comme il convient.</span><span class="sxs-lookup"><span data-stu-id="13021-152">In addition toocreating hello Docker VM, hello `azure vm docker create` command also automatically creates hello necessary certificates tooallow your Docker client computer tooconnect toohello Azure container host using HTTPS, and hello certificates are stored on both hello client and host machines, as appropriate.</span></span> <span data-ttu-id="13021-153">Lors des tentatives suivantes, les certificats existants hello sont réutilisées et partagées avec le nouvel hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="13021-153">On subsequent attempts, hello existing certificates are reused and shared with hello new host.</span></span>

<span data-ttu-id="13021-154">Par défaut, les certificats sont placés dans `~/.docker`, et Docker sera toorun configuré sur le port **2376**.</span><span class="sxs-lookup"><span data-stu-id="13021-154">By default, certificates are placed in `~/.docker`, and Docker will be configured toorun on port **2376**.</span></span> <span data-ttu-id="13021-155">Si vous souhaitez que toouse un autre port ou le répertoire, vous pouvez utiliser une des manières suivantes les hello `azure vm docker create` les options de ligne de commande tooconfigure votre Docker conteneur hôte VM toouse un autre port ou les différents certificats pour la connexion des clients :</span><span class="sxs-lookup"><span data-stu-id="13021-155">If you would like toouse a different port or directory, then you may use one of hello following `azure vm docker create` command line options tooconfigure your Docker container host VM toouse a different port or different certificates for connecting clients:</span></span>

```
-dp, --docker-port [port]              Port toouse for docker [2376]
-dc, --docker-cert-dir [dir]           Directory containing docker certs [.docker/]
```

<span data-ttu-id="13021-156">est configuré toolisten pour Hello démon Docker sur l’ordinateur hôte de hello et authentifier les connexions sur hello spécifié de port à l’aide de certificats de hello générés par hello de client `azure vm docker create` commande.</span><span class="sxs-lookup"><span data-stu-id="13021-156">hello Docker daemon on hello host is configured toolisten for and authenticate client connections on hello specified port using hello certificates generated by hello `azure vm docker create` command.</span></span> <span data-ttu-id="13021-157">Hello client doit être ces hôte Docker de certificats toogain accès toohello.</span><span class="sxs-lookup"><span data-stu-id="13021-157">hello client machine must have these certificates toogain access toohello Docker host.</span></span>

> [!NOTE]
> <span data-ttu-id="13021-158">Un hôte en réseau en cours d’exécution sans ces certificats sera vulnérable tooanyone pouvant tooconnect toohello machine.</span><span class="sxs-lookup"><span data-stu-id="13021-158">A networked host running without these certificates will be vulnerable tooanyone that can tooconnect toohello machine.</span></span> <span data-ttu-id="13021-159">Avant de modifier de la configuration par défaut de hello, assurez-vous que vous comprenez hello risques tooyour ordinateurs et applications.</span><span class="sxs-lookup"><span data-stu-id="13021-159">Before you modify hello default configuration, ensure that you understand hello risks tooyour computers and applications.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="13021-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="13021-160">Next steps</span></span>
* <span data-ttu-id="13021-161">Vous êtes prêt toogo toohello [Guide de l’utilisateur Docker] et utiliser votre machine virtuelle Docker.</span><span class="sxs-lookup"><span data-stu-id="13021-161">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="13021-162">toocreate une machine virtuelle de Docker activée dans le nouveau portail de hello, consultez [comment toouse hello Extension de machine virtuelle Docker avec hello Portal].</span><span class="sxs-lookup"><span data-stu-id="13021-162">toocreate a Docker-enabled VM in hello new portal, see [How toouse hello Docker VM Extension with hello Portal].</span></span>
* <span data-ttu-id="13021-163">également, Hello extension de machine virtuelle Docker de Azure prend en charge de composer Docker, qui utilise un tootake de fichier YAML déclarative une application modélisée de développeur dans tous les environnements et générer un déploiement cohérent.</span><span class="sxs-lookup"><span data-stu-id="13021-163">hello Azure Docker VM extension also supports Docker Compose, which uses a declarative YAML file tootake a developer-modeled application across any environment and generate a consistent deployment.</span></span> <span data-ttu-id="13021-164">Consultez [prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure].</span><span class="sxs-lookup"><span data-stu-id="13021-164">See [Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine].</span></span>  

<!--Anchors-->
[Subheading 1]:#subheading-1
[Subheading 2]:#subheading-2
[Subheading 3]:#subheading-3
[Next steps]:#next-steps

[How toouse hello Docker VM Extension with Azure]:#How-to-use-the-Docker-VM-Extension-with-Azure
[Virtual Machine Extensions for Linux and Windows]:#Virtual-Machine-Extensions-For-Linux-and-Windows
[Container and Container Management Resources for Azure]:#Container-and-Container-Management-Resources-for-Azure



<!--Link references-->
[Link 1 tooanother azure.microsoft.com documentation topic]:../../virtual-machines-windows-hero-tutorial.md
[Link 2 tooanother azure.microsoft.com documentation topic]:../../../app-service-web/web-sites-custom-domain-name.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md
[comment toouse hello Extension de machine virtuelle Docker avec hello Portal]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-portal/

[Guide de l’utilisateur Docker]:https://docs.docker.com/userguide/

[prise en main Docker et toodefine de composer et exécuter une application conteneur multiples sur une machine virtuelle Azure]:../docker-compose-quickstart.md
