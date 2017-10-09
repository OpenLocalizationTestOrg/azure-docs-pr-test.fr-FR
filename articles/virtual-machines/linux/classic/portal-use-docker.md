---
title: aaaUsing Extension de machine virtuelle Docker pour Linux | Documents Microsoft
description: "Décrit Docker et extensions des Machines virtuelles Azure hello et comment toocreate Machines virtuelles Azure qui sont des hôtes docker à l’aide de hello CLI d’Azure dans le modèle de déploiement classique."
services: virtual-machines-linux
documentationcenter: 
author: squillace
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 19cf64e8-f92c-43ad-a120-8976cd9102ac
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/27/2016
ms.author: rasquill
ms.openlocfilehash: 9d455b63c48b0c1b6f14862e072f899a73b46153
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-docker-vm-extension-with-hello-azure-classic-portal"></a><span data-ttu-id="11e45-103">À l’aide de hello Extension de machine virtuelle Docker avec hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="11e45-103">Using hello Docker VM Extension with hello Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="11e45-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="11e45-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="11e45-105">Cet article décrit à l’aide du modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="11e45-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="11e45-106">Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="11e45-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="11e45-107">[Docker](https://www.docker.com/) d'entre hello est la virtualisation qui utilise les plus populaires [les conteneurs Linux](http://en.wikipedia.org/wiki/LXC) plutôt que des machines virtuelles comme un moyen d’isoler les données et le calcul sur des ressources partagées.</span><span class="sxs-lookup"><span data-stu-id="11e45-107">[Docker](https://www.docker.com/) is one of hello most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="11e45-108">Vous pouvez utiliser extension de machine virtuelle de Docker hello gérée par [Linux Agent Azure] toocreate une machine virtuelle Docker qui héberge un nombre quelconque de conteneurs pour vos applications sur Azure.</span><span class="sxs-lookup"><span data-stu-id="11e45-108">You can use hello Docker VM extension managed by [Azure Linux Agent] toocreate a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="11e45-109">Cette rubrique décrit comment toocreate une machine virtuelle de Docker à partir de hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="11e45-109">This topic describes how toocreate a Docker VM from hello Azure classic portal.</span></span> <span data-ttu-id="11e45-110">toosee toocreate une machine virtuelle de Docker à la ligne de commande hello, voir [comment toouse hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)].</span><span class="sxs-lookup"><span data-stu-id="11e45-110">toosee how toocreate a Docker VM at hello command line, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="11e45-111">toosee une description détaillée des conteneurs et leurs avantages, consultez hello [tableau blanc de niveau élevé Docker](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="11e45-111">toosee a high-level discussion of containers and their advantages, see hello [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-hello-image-gallery"></a><span data-ttu-id="11e45-112">Créer une machine virtuelle à partir de la galerie d’images de hello</span><span class="sxs-lookup"><span data-stu-id="11e45-112">Create a new VM from hello Image Gallery</span></span>
<span data-ttu-id="11e45-113">première étape de Hello nécessite une machine virtuelle de Azure à partir d’une image Linux qui prend en charge hello Extension de machine virtuelle Docker, à l’aide d’une image Ubuntu 14.04 LTS hello Galerie d’images en tant qu’une image de serveur exemple et Ubuntu 14.04 Desktop en tant que client.</span><span class="sxs-lookup"><span data-stu-id="11e45-113">hello first step requires an Azure VM from a Linux image that supports hello Docker VM Extension, using an Ubuntu 14.04 LTS image from hello Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="11e45-114">Dans le portail de hello, cliquez sur **+ nouveau** Bonjour bas à gauche angle toocreate une nouvelle instance de la machine virtuelle et sélectionnez une image d’Ubuntu 14.04 LTS à partir de sélections hello disponibles ou de hello terminer la galerie d’images, comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="11e45-114">In hello portal, click **+ New** in hello bottom left corner toocreate a new VM instance and select an Ubuntu 14.04 LTS image from hello selections available or from hello complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="11e45-115">Actuellement, seules les images Ubuntu 14.04 LTS plus récentes que celle de juillet 2014 prend en charge hello Extension de machine virtuelle Docker.</span><span class="sxs-lookup"><span data-stu-id="11e45-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support hello Docker VM Extension.</span></span>
> 
> 

![Create a new Ubuntu Image](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="11e45-117">Création de certificats Docker</span><span class="sxs-lookup"><span data-stu-id="11e45-117">Create Docker Certificates</span></span>
<span data-ttu-id="11e45-118">Après avoir hello machine virtuelle a été créé, vérifiez que Docker est installé sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="11e45-118">After hello VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="11e45-119">(pour plus d'informations, voir [Instructions d'installation de Docker](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="11e45-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="11e45-120">Créer des fichiers de certificat et la clé pour la communication Docker selon trop hello[en cours d’exécution de Docker avec https] et placez-les dans hello  **`~/.docker`**  répertoire sur votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="11e45-120">Create hello certificate and key files for Docker communication according too[Running Docker with https] and place them in hello **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="11e45-121">actuellement, Hello Extension de machine virtuelle Docker dans le portail de hello requiert les informations d’identification qui sont codées en base64.</span><span class="sxs-lookup"><span data-stu-id="11e45-121">hello Docker VM Extension in hello portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="11e45-122">À la ligne de commande hello, utilisez  **`base64`**  ou favori un autre encodage rubriques codé en base 64 des toocreate d’outil.</span><span class="sxs-lookup"><span data-stu-id="11e45-122">At hello command line, use **`base64`** or another favorite encoding tool toocreate base64-encoded topics.</span></span> <span data-ttu-id="11e45-123">Cette opération avec un ensemble simple de fichiers de certificat et la clé peut se présenter toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="11e45-123">Doing this with a simple set of certificate and key files might look similar toothis:</span></span>

```
 ~/.docker$ ls
 ca-key.pem  ca.pem  cert.pem  key.pem  server-cert.pem  server-key.pem
 ~/.docker$ base64 ca.pem > ca64.pem
 ~/.docker$ base64 server-cert.pem > server-cert64.pem
 ~/.docker$ base64 server-key.pem > server-key64.pem
 ~/.docker$ ls
 ca64.pem    ca.pem    key.pem            server-cert.pem   server-key.pem
 ca-key.pem  cert.pem  server-cert64.pem  server-key64.pem
```

## <a name="add-hello-docker-vm-extension"></a><span data-ttu-id="11e45-124">Ajouter hello Extension de machine virtuelle Docker</span><span class="sxs-lookup"><span data-stu-id="11e45-124">Add hello Docker VM Extension</span></span>
<span data-ttu-id="11e45-125">tooadd hello Extension de machine virtuelle Docker, recherchez l’instance de machine virtuelle hello vous avez créé et faites défiler trop**Extensions** et cliquez sur toobring des Extensions de machine virtuelle, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="11e45-125">tooadd hello Docker VM Extension, locate hello VM instance you created and scroll down too**Extensions** and click it toobring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="11e45-126">Cette fonctionnalité est prise en charge dans le portail en version préliminaire hello uniquement : https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="11e45-126">This functionality is supported in hello preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="11e45-127">Ajout d’une extension</span><span class="sxs-lookup"><span data-stu-id="11e45-127">Add an Extension</span></span>
<span data-ttu-id="11e45-128">Cliquez sur hello **+ ajouter** toodisplay hello possibles Extensions de machine virtuelle vous pouvez ajouter toothis machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="11e45-128">Click hello **+ Add** toodisplay hello possible VM Extensions you can add toothis VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-hello-docker-vm-extension"></a><span data-ttu-id="11e45-129">Sélectionnez hello Extension de machine virtuelle Docker</span><span class="sxs-lookup"><span data-stu-id="11e45-129">Select hello Docker VM Extension</span></span>
<span data-ttu-id="11e45-130">Hello, Extension de machine virtuelle Docker, qui met à jour les description de Docker hello et les liens importants, et cliquez sur **créer** au niveau de la procédure d’installation hello bas toobegin hello.</span><span class="sxs-lookup"><span data-stu-id="11e45-130">Choose hello Docker VM Extension, which brings up hello Docker description and important links, and then click **Create** at hello bottom toobegin hello installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="11e45-131">Ajout de vos certificats et de vos fichiers de clés :</span><span class="sxs-lookup"><span data-stu-id="11e45-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="11e45-132">Dans les champs de formulaire hello, entrez hello codée en base64 les versions de votre certificat d’autorité de certification, votre certificat de serveur et votre clé de serveur, comme indiqué dans le graphique suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="11e45-132">In hello form fields, enter hello base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in hello following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="11e45-133">Notez que (par exemple hello précédant l’image) hello 2376 est renseigné par défaut.</span><span class="sxs-lookup"><span data-stu-id="11e45-133">Note that (as in hello preceding image) hello 2376 is filled in by default.</span></span> <span data-ttu-id="11e45-134">Vous pouvez entrer n’importe quel point de terminaison ici, mais maintenant hello seront tooopen des hello point de terminaison de mise en correspondance.</span><span class="sxs-lookup"><span data-stu-id="11e45-134">You can enter any endpoint here, but hello next step will be tooopen up hello matching endpoint.</span></span> <span data-ttu-id="11e45-135">Si vous modifiez la valeur par défaut de hello, assurez-vous que tooopen des hello correspondant à un point de terminaison à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="11e45-135">If you change hello default, make sure tooopen up hello matching endpoint in hello next step.</span></span>
> 
> 

## <a name="add-hello-docker-communication-endpoint"></a><span data-ttu-id="11e45-136">Ajouter hello point de terminaison de Communication Docker</span><span class="sxs-lookup"><span data-stu-id="11e45-136">Add hello Docker Communication Endpoint</span></span>
<span data-ttu-id="11e45-137">Lorsque vous affichez un groupe de ressources hello que vous avez créé, sélectionnez hello groupe de sécurité réseau associé à votre machine virtuelle, puis cliquez sur **règles de sécurité de trafic entrant** tooview hello règles comme illustré ici.</span><span class="sxs-lookup"><span data-stu-id="11e45-137">When viewing hello resource group you've created, select hello Network Security Group associated with your VM, and click **Inbound Security Rules** tooview hello rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="11e45-138">Cliquez sur **+ ajouter** tooadd une autre règle et dans le cas par défaut de hello, entrez un nom pour le point de terminaison hello (dans cet exemple, **Docker**) et 2376 « plage de Port de Destination ».</span><span class="sxs-lookup"><span data-stu-id="11e45-138">Click **+ Add** tooadd another rule, and in hello default case, enter a name for hello endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="11e45-139">Définir l’affichage de valeur de protocole hello **TCP**, puis cliquez sur **OK** règle de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="11e45-139">Set hello protocol value showing **TCP**, and Click **OK** toocreate hello rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="11e45-140">Tester le client Docker et l’hôte Azure Docker</span><span class="sxs-lookup"><span data-stu-id="11e45-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="11e45-141">Recherchez et copiez hello nom de domaine de votre machine virtuelle et à la ligne de commande hello de votre ordinateur client, tapez `docker --tls -H tcp://` *dockerextension* `.cloudapp.net:2376 info` (où *dockerextension* est remplacé par hello sous-domaine de votre machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="11e45-141">Locate and copy hello name of your VM's domain, and at hello command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by hello subdomain for your VM).</span></span>

<span data-ttu-id="11e45-142">résultat de Hello doit apparaître toothis similaire :</span><span class="sxs-lookup"><span data-stu-id="11e45-142">hello result should appear similar toothis:</span></span>

```
$ docker --tls -H tcp://dockerextension.cloudapp.net:2376 info
Containers: 0
Images: 0
Storage Driver: devicemapper
 Pool Name: docker-8:1-131214-pool
 Pool Blocksize: 65.54 kB
 Data file: /var/lib/docker/devicemapper/devicemapper/data
 Metadata file: /var/lib/docker/devicemapper/devicemapper/metadata
 Data Space Used: 305.7 MB
 Data Space Total: 107.4 GB
 Metadata Space Used: 729.1 kB
 Metadata Space Total: 2.147 GB
 Library Version: 1.02.82-git (2013-10-04)
Execution Driver: native-0.2
Kernel Version: 3.13.0-36-generic
WARNING: No swap limit support
```

<span data-ttu-id="11e45-143">Après avoir terminé hello étapes ci-dessus, vous avez maintenant un hôte Docker entièrement fonctionnel en cours d’exécution sur une machine virtuelle Azure, configuré toobe connecté tooremotely à partir d’autres clients.</span><span class="sxs-lookup"><span data-stu-id="11e45-143">Once you complete hello above steps, you now have a fully functional Docker host running on an Azure VM, configured toobe connected tooremotely from other clients.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="11e45-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11e45-144">Next steps</span></span>
<span data-ttu-id="11e45-145">Vous êtes prêt toogo toohello [Guide de l’utilisateur Docker] et utiliser votre machine virtuelle Docker.</span><span class="sxs-lookup"><span data-stu-id="11e45-145">You are ready toogo toohello [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="11e45-146">Si vous souhaitez tooautomate création d’hôtes Docker sur les machines virtuelles Azure via l’interface de ligne de commande, consultez [comment toouse hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)]</span><span class="sxs-lookup"><span data-stu-id="11e45-146">If you want tooautomate creating Docker hosts on Azure VMs through command line interface, see [How toouse hello Docker VM Extension from hello Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from hello Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add hello Docker VM Extension]:#adddockerextension
[Test Docker Client and Azure Docker Host]:#testclientandserver
[Next steps]:#next-steps

<!--Image references-->
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[StartingPoint]:./media/StartingPoint.png
[6]:./media/markdown-template-for-new-articles/pretty49.png
[7]:./media/markdown-template-for-new-articles/channel-9.png


<!--Link references-->
[comment toouse hello Extension de machine virtuelle Docker à partir de hello Azure Interface de ligne (Azure)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/
[Linux Agent Azure]:../agent-user-guide.md
[Link 3 tooanother azure.microsoft.com documentation topic]:../storage-whatis-account.md

[en cours d’exécution de Docker avec https]:http://docs.docker.com/articles/https/
[Guide de l’utilisateur Docker]:https://docs.docker.com/userguide/
