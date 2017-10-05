---
title: "Utilisation de l’extension Docker VM pour Linux | Microsoft Docs"
description: "Décrit Docker et les extensions Azure Virtual Machines, et explique comment créer des machines virtuelles Azure en tant qu’hôtes Docker à l’aide de l’interface de ligne de commande Azure dans le modèle de déploiement classique."
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
ms.openlocfilehash: 932744208d9d53c87e31dcdf9e34539750be4bdb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-docker-vm-extension-with-the-azure-classic-portal"></a><span data-ttu-id="57498-103">Utilisation de l’extension Docker VM avec le portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="57498-103">Using the Docker VM Extension with the Azure classic portal</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="57498-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="57498-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="57498-105">Cet article traite du modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="57498-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="57498-106">Pour la plupart des nouveaux déploiements, Microsoft recommande d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="57498-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="57498-107">[Docker](https://www.docker.com/) fait partie des méthodes de virtualisation les plus prisées. Cet outil utilise des [conteneurs Linux](http://en.wikipedia.org/wiki/LXC) plutôt que des machines virtuelles pour isoler les données et le traitement sur des ressources partagées.</span><span class="sxs-lookup"><span data-stu-id="57498-107">[Docker](https://www.docker.com/) is one of the most popular virtualization approaches that uses [Linux containers](http://en.wikipedia.org/wiki/LXC) rather than virtual machines as a way of isolating data and computing on shared resources.</span></span> <span data-ttu-id="57498-108">Vous pouvez utiliser l’extension Docker VM sur l’[agent Linux Azure] afin de créer une machine virtuelle Docker hébergeant un nombre indéfini de conteneurs pour vos applications sur Azure.</span><span class="sxs-lookup"><span data-stu-id="57498-108">You can use the Docker VM extension managed by [Azure Linux Agent] to create a Docker VM that hosts any number of containers for your applications on Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="57498-109">Cette rubrique décrit comment créer une machine virtuelle Docker à partir du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="57498-109">This topic describes how to create a Docker VM from the Azure classic portal.</span></span> <span data-ttu-id="57498-110">Pour savoir comment créer une machine virtuelle Docker dans la ligne de commande, consultez la page [Utilisation de l’extension Docker VM à partir de l’interface interplateforme Azure (xplat-cli)].</span><span class="sxs-lookup"><span data-stu-id="57498-110">To see how to create a Docker VM at the command line, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)].</span></span> <span data-ttu-id="57498-111">Pour une discussion sur les conteneurs et leurs avantages, consultez le [Tableau blanc Docker de haut niveau](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span><span class="sxs-lookup"><span data-stu-id="57498-111">To see a high-level discussion of containers and their advantages, see the [Docker High Level Whiteboard](http://channel9.msdn.com/Blogs/Regular-IT-Guy/Docker-High-Level-Whiteboard).</span></span>
> 
> 

## <a name="create-a-new-vm-from-the-image-gallery"></a><span data-ttu-id="57498-112">Création d'une machine virtuelle à partir de la galerie d'images</span><span class="sxs-lookup"><span data-stu-id="57498-112">Create a new VM from the Image Gallery</span></span>
<span data-ttu-id="57498-113">La première étape nécessite une machine virtuelle Azure à partir d'une image Linux qui prend en charge l'extension Docker VM, en utilisant une image Ubuntu 14.04 LTS de la galerie d'images comme exemple d'image de serveur et Ubuntu 14.04 Desktop comme client.</span><span class="sxs-lookup"><span data-stu-id="57498-113">The first step requires an Azure VM from a Linux image that supports the Docker VM Extension, using an Ubuntu 14.04 LTS image from the Image Gallery as an example server image and Ubuntu 14.04 Desktop as a client.</span></span> <span data-ttu-id="57498-114">Dans le portail, cliquez sur **+ Nouveau** dans le coin inférieur gauche pour créer une instance de machine virtuelle, puis sélectionnez une image Ubuntu 14.04 LTS parmi les choix proposés ou la galerie d'images complète (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="57498-114">In the portal, click **+ New** in the bottom left corner to create a new VM instance and select an Ubuntu 14.04 LTS image from the selections available or from the complete Image Gallery, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="57498-115">Actuellement, seules les images Ubuntu 14.04 LTS postérieures à juillet 2014 prennent en charge l’extension Docker VM.</span><span class="sxs-lookup"><span data-stu-id="57498-115">Currently, only Ubuntu 14.04 LTS images more recent than July 2014 support the Docker VM Extension.</span></span>
> 
> 

![Create a new Ubuntu Image](./media/portal-use-docker/ChooseUbuntu.png)

## <a name="create-docker-certificates"></a><span data-ttu-id="57498-117">Création de certificats Docker</span><span class="sxs-lookup"><span data-stu-id="57498-117">Create Docker Certificates</span></span>
<span data-ttu-id="57498-118">Après la création de la machine virtuelle, vérifiez que Docker est installé sur votre ordinateur client</span><span class="sxs-lookup"><span data-stu-id="57498-118">After the VM has been created, ensure that Docker is installed on your client computer.</span></span> <span data-ttu-id="57498-119">(pour plus d'informations, voir [Instructions d'installation de Docker](https://docs.docker.com/installation/#installation).)</span><span class="sxs-lookup"><span data-stu-id="57498-119">(For details, see [Docker installation instructions](https://docs.docker.com/installation/#installation).)</span></span>

<span data-ttu-id="57498-120">Créez le certificat et les fichiers de clés pour les communications Docker en respectant les instructions fournies à la page [Exécution de Docker avec https] ; placez-les ensuite dans le répertoire **`~/.docker`** de votre ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="57498-120">Create the certificate and key files for Docker communication according to [Running Docker with https] and place them in the **`~/.docker`** directory on your client computer.</span></span>

> [!NOTE]
> <span data-ttu-id="57498-121">L’extension Docker VM dans le portail nécessite actuellement des informations d’identification codées en base64.</span><span class="sxs-lookup"><span data-stu-id="57498-121">The Docker VM Extension in the portal currently requires credentials that are base64 encoded.</span></span>
> 
> 

<span data-ttu-id="57498-122">Dans la ligne de commande, utilisez **`base64`** ou un autre outil d’encodage de votre choix pour créer des rubriques codées en base64.</span><span class="sxs-lookup"><span data-stu-id="57498-122">At the command line, use **`base64`** or another favorite encoding tool to create base64-encoded topics.</span></span> <span data-ttu-id="57498-123">Avec un jeu simple de certificats et de fichiers de clés, le code peut être similaire au code suivant :</span><span class="sxs-lookup"><span data-stu-id="57498-123">Doing this with a simple set of certificate and key files might look similar to this:</span></span>

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

## <a name="add-the-docker-vm-extension"></a><span data-ttu-id="57498-124">Ajout de l'extension Docker VM</span><span class="sxs-lookup"><span data-stu-id="57498-124">Add the Docker VM Extension</span></span>
<span data-ttu-id="57498-125">Pour ajouter l'extension Docker VM, localisez l'instance de machine virtuelle que vous avez créée, accédez à **Extensions** , puis cliquez pour afficher Extensions de machine virtuelle (voir ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="57498-125">To add the Docker VM Extension, locate the VM instance you created and scroll down to **Extensions** and click it to bring up VM Extensions, as shown below.</span></span>

> [!NOTE]
> <span data-ttu-id="57498-126">Cette fonctionnalité est prise en charge dans la version préliminaire du portail uniquement : https://portal.azure.com/</span><span class="sxs-lookup"><span data-stu-id="57498-126">This functionality is supported in the preview portal only: https://portal.azure.com/</span></span>
> 
> 

![](media/portal-use-docker/ClickExtensions.png)

### <a name="add-an-extension"></a><span data-ttu-id="57498-127">Ajout d’une extension</span><span class="sxs-lookup"><span data-stu-id="57498-127">Add an Extension</span></span>
<span data-ttu-id="57498-128">Cliquez sur **+ Ajouter** pour afficher les extensions de machine virtuelle que vous pouvez ajouter à cette machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="57498-128">Click the **+ Add** to display the possible VM Extensions you can add to this VM.</span></span>

![](media/portal-use-docker/ClickAdd.png)

### <a name="select-the-docker-vm-extension"></a><span data-ttu-id="57498-129">Sélection de l’extension Docker VM</span><span class="sxs-lookup"><span data-stu-id="57498-129">Select the Docker VM Extension</span></span>
<span data-ttu-id="57498-130">Choisissez l'extension Docker VM : elle affiche la description de Docker et des liens importants. Cliquez ensuite sur **Créer** au bas de l'écran pour commencer l'installation.</span><span class="sxs-lookup"><span data-stu-id="57498-130">Choose the Docker VM Extension, which brings up the Docker description and important links, and then click **Create** at the bottom to begin the installation procedure.</span></span>

![](media/portal-use-docker/ChooseDockerExtension.png)

![](media/portal-use-docker/CreateButtonFocus.png)

### <a name="add-your-certificate-and-key-files"></a><span data-ttu-id="57498-131">Ajout de vos certificats et de vos fichiers de clés :</span><span class="sxs-lookup"><span data-stu-id="57498-131">Add your Certificate and Key Files:</span></span>
<span data-ttu-id="57498-132">Dans les champs du formulaire, entrez les versions codées en base64 de votre certificat CA, le certificat et la clé de votre serveur (voir l’illustration ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="57498-132">In the form fields, enter the base64-encoded versions of your CA Certificate, your Server Certificate, and your Server Key, as shown in the following graphic.</span></span>

![](media/portal-use-docker/AddExtensionFormFilled.png)

> [!NOTE]
> <span data-ttu-id="57498-133">Notez que (comme dans l’illustration précédente), 2376 est indiqué par défaut.</span><span class="sxs-lookup"><span data-stu-id="57498-133">Note that (as in the preceding image) the 2376 is filled in by default.</span></span> <span data-ttu-id="57498-134">Vous pouvez entrer ici n’importe quel point de terminaison, mais l’étape suivante consiste à ouvrir le point de terminaison correspondant.</span><span class="sxs-lookup"><span data-stu-id="57498-134">You can enter any endpoint here, but the next step will be to open up the matching endpoint.</span></span> <span data-ttu-id="57498-135">Si vous modifiez le point de terminaison par défaut, n'oubliez pas d'ouvrir le point de terminaison correct à l'étape suivante.</span><span class="sxs-lookup"><span data-stu-id="57498-135">If you change the default, make sure to open up the matching endpoint in the next step.</span></span>
> 
> 

## <a name="add-the-docker-communication-endpoint"></a><span data-ttu-id="57498-136">Ajout du point de terminaison des communications Docker VM</span><span class="sxs-lookup"><span data-stu-id="57498-136">Add the Docker Communication Endpoint</span></span>
<span data-ttu-id="57498-137">Lorsque vous affichez le groupe de ressources que vous avez créé, sélectionnez le groupe de sécurité réseau associé à votre machine virtuelle, puis cliquez sur **Règles de sécurité entrantes** pour afficher les règles comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="57498-137">When viewing the resource group you've created, select the Network Security Group associated with your VM, and click **Inbound Security Rules** to view the rules as shown here.</span></span>

![](media/portal-use-docker/AddingEndpoint.png)

<span data-ttu-id="57498-138">Cliquez sur **+ Ajouter** pour ajouter une règle ; dans le cas par défaut, entrez un nom pour le point de terminaison (dans cet exemple **Docker**) et 2376 « Étendue du port de destination ».</span><span class="sxs-lookup"><span data-stu-id="57498-138">Click **+ Add** to add another rule, and in the default case, enter a name for the endpoint (in this example, **Docker**), and 2376 'Destination Port Range'.</span></span> <span data-ttu-id="57498-139">Définissez la valeur du protocole sur **TCP** et cliquez sur **OK** pour créer la règle.</span><span class="sxs-lookup"><span data-stu-id="57498-139">Set the protocol value showing **TCP**, and Click **OK** to create the rule.</span></span>

![](media/portal-use-docker/AddEndpointFormFilledOut.png)

## <a name="test-your-docker-client-and-azure-docker-host"></a><span data-ttu-id="57498-140">Tester le client Docker et l’hôte Azure Docker</span><span class="sxs-lookup"><span data-stu-id="57498-140">Test your Docker Client and Azure Docker Host</span></span>
<span data-ttu-id="57498-141">Localisez et copiez le nom de domaine de votre machine virtuelle. Dans la ligne de commande de votre ordinateur client, tapez `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (où *dockerextension* est remplacé par le sous-domaine de votre machine virtuelle).</span><span class="sxs-lookup"><span data-stu-id="57498-141">Locate and copy the name of your VM's domain, and at the command line of your client computer, type `docker --tls -H tcp://`*dockerextension*`.cloudapp.net:2376 info` (where *dockerextension* is replaced by the subdomain for your VM).</span></span>

<span data-ttu-id="57498-142">Le résultat affiché doit avoir l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="57498-142">The result should appear similar to this:</span></span>

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

<span data-ttu-id="57498-143">Lorsque vous avez terminé les étapes ci-dessus, vous disposez maintenant d'un hôte Docker parfaitement fonctionnel exécuté sur une machine virtuelle Azure, configuré pour une connexion à distance à partir d'autres clients.</span><span class="sxs-lookup"><span data-stu-id="57498-143">Once you complete the above steps, you now have a fully functional Docker host running on an Azure VM, configured to be connected to remotely from other clients.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="57498-144">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57498-144">Next steps</span></span>
<span data-ttu-id="57498-145">Vous êtes prêt à consulter le [Guide d'utilisation Docker] et à utiliser votre machine virtuelle Docker.</span><span class="sxs-lookup"><span data-stu-id="57498-145">You are ready to go to the [Docker User Guide] and use your Docker VM.</span></span> <span data-ttu-id="57498-146">Si vous souhaitez automatiser la création d’hôtes Docker sur des machines virtuelles Azure via l’interface de ligne de commande, consultez la page [Utilisation de l’extension Docker VM à partir de l’interface interplateforme Azure (xplat-cli)]</span><span class="sxs-lookup"><span data-stu-id="57498-146">If you want to automate creating Docker hosts on Azure VMs through command line interface, see [How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]</span></span>

<!--Anchors-->
[Create a new VM from the Image Gallery]:#createvm
[Create Docker Certificates]:#dockercerts
[Add the Docker VM Extension]:#adddockerextension
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
<span data-ttu-id="57498-147">[Utilisation de l’extension Docker VM à partir de l’interface interplateforme Azure (xplat-cli)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span><span class="sxs-lookup"><span data-stu-id="57498-147">[How to use the Docker VM Extension from the Azure Command-line Interface (Azure CLI)]:http://azure.microsoft.com/documentation/articles/virtual-machines-docker-with-xplat-cli/</span></span>
<span data-ttu-id="57498-148">[agent Linux Azure]:../agent-user-guide.md</span><span class="sxs-lookup"><span data-stu-id="57498-148">[Azure Linux Agent]:../agent-user-guide.md</span></span>
[Link 3 to another azure.microsoft.com documentation topic]:../storage-whatis-account.md

<span data-ttu-id="57498-149">[Exécution de Docker avec https]:http://docs.docker.com/articles/https/</span><span class="sxs-lookup"><span data-stu-id="57498-149">[Running Docker with https]:http://docs.docker.com/articles/https/</span></span>
<span data-ttu-id="57498-150">[Guide d'utilisation Docker]:https://docs.docker.com/userguide/</span><span class="sxs-lookup"><span data-stu-id="57498-150">[Docker User Guide]:https://docs.docker.com/userguide/</span></span>
