---
title: "aaaSet de votre environnement de développement sur toowork Mac OS X avec Azure Service Fabric | Documents Microsoft"
description: "Installer le runtime de hello, Kit de développement logiciel et les outils et créer un cluster de développement local. Après avoir terminé cette installation, vous serez prêt toobuild des applications sur Mac OS X."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2017
ms.author: saysa
ms.openlocfilehash: 0b8a6c1fc1871fa76f3e21cefbc7f66f79072797
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-your-development-environment-on-mac-os-x"></a><span data-ttu-id="50405-104">Configurer votre environnement de développement sur Mac OS X</span><span class="sxs-lookup"><span data-stu-id="50405-104">Set up your development environment on Mac OS X</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="50405-105">Windows</span><span class="sxs-lookup"><span data-stu-id="50405-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="50405-106">Linux</span><span class="sxs-lookup"><span data-stu-id="50405-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="50405-107">OSX</span><span class="sxs-lookup"><span data-stu-id="50405-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="50405-108">Vous pouvez générer toorun des applications de Service Fabric sur les clusters Linux à l’aide de Mac OS X. Cet article décrit comment tooset de votre Mac pour le développement.</span><span class="sxs-lookup"><span data-stu-id="50405-108">You can build Service Fabric applications toorun on Linux clusters using Mac OS X. This article covers how tooset up your Mac for development.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50405-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="50405-109">Prerequisites</span></span>
<span data-ttu-id="50405-110">L’infrastructure de service ne s’exécute pas en mode natif sur OS X. toorun un cluster Service Fabric local, nous fournir l’ordinateur virtuel préconfiguré Ubuntu à l’aide de Vagrant et VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="50405-110">Service Fabric does not run natively on OS X. toorun a local Service Fabric cluster, we provide a pre-configured Ubuntu virtual machine using Vagrant and VirtualBox.</span></span> <span data-ttu-id="50405-111">Avant de commencer, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="50405-111">Before you get started, you need:</span></span>

* [<span data-ttu-id="50405-112">Vagrant (v1.8.4 ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="50405-112">Vagrant (v1.8.4 or later)</span></span>](http://www.vagrantup.com/downloads.html)
* [<span data-ttu-id="50405-113">VirtualBox</span><span class="sxs-lookup"><span data-stu-id="50405-113">VirtualBox</span></span>](http://www.virtualbox.org/wiki/Downloads)

>[!NOTE]
> <span data-ttu-id="50405-114">Vous devez toouse mutuellement pris en charge les versions de Vagrant et VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="50405-114">You need toouse mutually supported versions of Vagrant and VirtualBox.</span></span> <span data-ttu-id="50405-115">Vagrant peut avoir un comportement erratique sur une version non prise en charge de VirtualBox.</span><span class="sxs-lookup"><span data-stu-id="50405-115">Vagrant might behave erratically on an unsupported VirtualBox version.</span></span>
>

## <a name="create-hello-local-vm"></a><span data-ttu-id="50405-116">Créer hello VM locale</span><span class="sxs-lookup"><span data-stu-id="50405-116">Create hello local VM</span></span>
<span data-ttu-id="50405-117">toocreate hello local machine virtuelle contenant un cluster Service Fabric 5, effectuez les hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="50405-117">toocreate hello local VM containing a 5-node Service Fabric cluster, perform hello following steps:</span></span>

1. <span data-ttu-id="50405-118">Hello du clone `Vagrantfile` référentiel</span><span class="sxs-lookup"><span data-stu-id="50405-118">Clone hello `Vagrantfile` repo</span></span>

    ```bash
    git clone https://github.com/azure/service-fabric-linux-vagrant-onebox.git
    ```
    <span data-ttu-id="50405-119">Cette procédure mettre downloads hello fichier `Vagrantfile` contenant hello VM configuration ainsi que de hello d’emplacement hello machine virtuelle est téléchargée depuis.</span><span class="sxs-lookup"><span data-stu-id="50405-119">This steps bring downs hello file `Vagrantfile` containing hello VM configuration along with hello location hello VM is downloaded from.</span></span>

2. <span data-ttu-id="50405-120">Accédez toohello le clone local de dépôt de hello</span><span class="sxs-lookup"><span data-stu-id="50405-120">Navigate toohello local clone of hello repo</span></span>

    ```bash
    cd service-fabric-linux-vagrant-onebox
    ```
3. <span data-ttu-id="50405-121">(Facultatif) Modifier les paramètres de machine virtuelle par défaut hello</span><span class="sxs-lookup"><span data-stu-id="50405-121">(Optional) Modify hello default VM settings</span></span>

    <span data-ttu-id="50405-122">Par défaut, hello local machine virtuelle est configurée comme suit :</span><span class="sxs-lookup"><span data-stu-id="50405-122">By default, hello local VM is configured as follows:</span></span>

   * <span data-ttu-id="50405-123">3 Go de mémoire allouée</span><span class="sxs-lookup"><span data-stu-id="50405-123">3 GB of memory allocated</span></span>
   * <span data-ttu-id="50405-124">Réseau privé hôte configuré sur l’IP 192.168.50.50 l’activation de relais du trafic de l’hôte de Mac hello</span><span class="sxs-lookup"><span data-stu-id="50405-124">Private host network configured at IP 192.168.50.50 enabling passthrough of traffic from hello Mac host</span></span>

     <span data-ttu-id="50405-125">Vous pouvez modifier une de ces paramètres ou ajouter d’autres toohello configuration VM Bonjour `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="50405-125">You can change either of these settings or add other configuration toohello VM in hello `Vagrantfile`.</span></span> <span data-ttu-id="50405-126">Consultez hello [documentation de Vagrant](http://www.vagrantup.com/docs) pour la liste complète des options de configuration hello.</span><span class="sxs-lookup"><span data-stu-id="50405-126">See hello [Vagrant documentation](http://www.vagrantup.com/docs) for hello full list of configuration options.</span></span>
4. <span data-ttu-id="50405-127">Créer hello machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="50405-127">Create hello VM</span></span>

    ```bash
    vagrant up
    ```

   <span data-ttu-id="50405-128">Cette étape télécharge l’image de machine virtuelle hello préconfiguré, démarrage du cluster local, puis configurer une infrastructure de Service local qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="50405-128">This step downloads hello preconfigured VM image, boot it locally, and then set up a local Service Fabric cluster in it.</span></span> <span data-ttu-id="50405-129">Vous devez prévoir il tootake quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="50405-129">You should expect it tootake a few minutes.</span></span> <span data-ttu-id="50405-130">Si le programme d’installation se termine correctement, vous consultez un message dans la sortie de hello indiquant le que démarrage de ce cluster hello.</span><span class="sxs-lookup"><span data-stu-id="50405-130">If setup completes successfully, you see a message in hello output indicating that hello cluster is starting up.</span></span>

    ![La configuration du cluster démarre après l’approvisionnement de la machine virtuelle][cluster-setup-script]

    >[!TIP]
    > <span data-ttu-id="50405-132">Si le téléchargement de machine virtuelle hello prend beaucoup de temps, vous pouvez le télécharger à l’aide de wget ou curl ou via un navigateur en parcourant le lien toohello spécifié par **config.vm.box_url** dans le fichier de hello `Vagrantfile`.</span><span class="sxs-lookup"><span data-stu-id="50405-132">If hello VM download is taking a long time, you can download it using wget or curl or through a browser by navigating toohello link specified by **config.vm.box_url** in hello file `Vagrantfile`.</span></span> <span data-ttu-id="50405-133">Après l’avoir téléchargé localement, modifier `Vagrantfile` toopoint toohello chemin d’accès local où vous avez téléchargé l’image de hello.</span><span class="sxs-lookup"><span data-stu-id="50405-133">After downloading it locally, edit `Vagrantfile` toopoint toohello local path where you downloaded hello image.</span></span> <span data-ttu-id="50405-134">Pour exemple si vous avez téléchargé hello image too/home/users/test/azureservicefabric.tp8.box, puis définissez **config.vm.box_url** toothat chemin.</span><span class="sxs-lookup"><span data-stu-id="50405-134">For example if you downloaded hello image too/home/users/test/azureservicefabric.tp8.box, then set **config.vm.box_url** toothat path.</span></span>
    >

5. <span data-ttu-id="50405-135">Tester ce hello cluster a été correctement configuré en accédant tooService Fabric Explorer dans http://192.168.50.50:19080/Explorateur (en supposant que vous avez conservé l’adresse IP de réseau privé hello par défaut).</span><span class="sxs-lookup"><span data-stu-id="50405-135">Test that hello cluster has been set up correctly by navigating tooService Fabric Explorer at http://192.168.50.50:19080/Explorer (assuming you kept hello default private network IP).</span></span>

    ![Service Fabric Explorer affichés à partir de l’hôte hello Mac][sfx-mac]


## <a name="create-application-on-mac-using-yeoman"></a><span data-ttu-id="50405-137">Créer l’application sur Mac à l’aide de Yeoman</span><span class="sxs-lookup"><span data-stu-id="50405-137">Create application on Mac using Yeoman</span></span>
<span data-ttu-id="50405-138">Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric depuis un terminal à l’aide du générateur de modèles Yeoman.</span><span class="sxs-lookup"><span data-stu-id="50405-138">Service Fabric provides scaffolding tools which will help you create a Service Fabric application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="50405-139">Veuillez suivre les étapes de hello ci-dessous tooensure que vous possédez Générateur de modèle yeoman Service Fabric hello vous travaillez sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="50405-139">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator working on your machine.</span></span>

1. <span data-ttu-id="50405-140">Vous devez toohave Node.js et NPM installé sur le mac vous.</span><span class="sxs-lookup"><span data-stu-id="50405-140">You need toohave Node.js and NPM installed on you mac.</span></span> <span data-ttu-id="50405-141">Si ce n’est pas le cas, vous pouvez installer Node.js et NPM à l’aide de Homebrew utilisant hello.</span><span class="sxs-lookup"><span data-stu-id="50405-141">If not you can install Node.js and NPM using Homebrew using hello following.</span></span> <span data-ttu-id="50405-142">versions de hello toocheck de Node.js et NPM installé sur votre Mac, vous pouvez utiliser hello ``-v`` option.</span><span class="sxs-lookup"><span data-stu-id="50405-142">toocheck hello versions of Node.js and NPM installed on your Mac, you can use hello ``-v`` option.</span></span>

  ```bash
  brew install node
  node -v
  npm -v
  ```
2. <span data-ttu-id="50405-143">Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="50405-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="50405-144">Installer hello Yeoman générateur souhaité toouse, hello comme suit dans la mise en route de hello [documentation](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="50405-144">Install hello Yeoman generator you want toouse, following hello steps in hello getting started [documentation](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="50405-145">Applications de l’infrastructure de Service toocreate Yeoman, à l’aide de la procédure hello-</span><span class="sxs-lookup"><span data-stu-id="50405-145">toocreate Service Fabric Applications using Yeoman, follow hello steps -</span></span>

  ```bash
  npm install -g generator-azuresfjava       # for Service Fabric Java Applications
  npm install -g generator-azuresfguest      # for Service Fabric Guest executables
  npm install -g generator-azuresfcontainer  # for Service Fabric Container Applications
  ```
4. <span data-ttu-id="50405-146">toobuild une application Java de l’infrastructure de Service sur le Mac, vous devriez - JDK 1.8 et Gradle installé sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="50405-146">toobuild a Service Fabric Java application on Mac, you would need - JDK 1.8 and Gradle installed on hello machine.</span></span>


## <a name="install-hello-service-fabric-plugin-for-eclipse-neon"></a><span data-ttu-id="50405-147">Installer le plug-in de hello Service Fabric pour Eclipse Neon</span><span class="sxs-lookup"><span data-stu-id="50405-147">Install hello Service Fabric plugin for Eclipse Neon</span></span>

<span data-ttu-id="50405-148">L’infrastructure de service fournit un plug-in pour hello **Neon Eclipse pour Java IDE** qui peuvent simplifier le processus de hello de création, la création et déploiement des services de Java.</span><span class="sxs-lookup"><span data-stu-id="50405-148">Service Fabric provides a plugin for hello **Eclipse Neon for Java IDE** that can simplify hello process of creating, building, and deploying Java services.</span></span> <span data-ttu-id="50405-149">Vous pouvez suivre les étapes d’installation hello mentionnés dans cette général [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) sur l’installation ou la mise à jour du plug-in Eclipse de l’infrastructure de Service.</span><span class="sxs-lookup"><span data-stu-id="50405-149">You can follow hello installation steps mentioned in this general [documentation](service-fabric-get-started-eclipse.md#install-or-update-the-service-fabric-plug-in-in-eclipse-neon) about installing or updating Service Fabric Eclipse plugin.</span></span>

>[!TIP]
> <span data-ttu-id="50405-150">Par défaut nous prenons en charge hello par défaut IP comme indiqué dans hello ``Vagrantfile`` Bonjour ``Local.json`` de l’application hello généré.</span><span class="sxs-lookup"><span data-stu-id="50405-150">By default we support hello default IP as mentioned in hello ``Vagrantfile`` in hello ``Local.json`` of hello generated application.</span></span> <span data-ttu-id="50405-151">Si vous modifiez qui et déployez Vagrant avec une autre adresse IP, mettez à jour hello adresse IP correspondante dans ``Local.json`` de votre application.</span><span class="sxs-lookup"><span data-stu-id="50405-151">In case you change that and deploy Vagrant with a different IP, please update hello corresponding IP in ``Local.json`` of your application as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="50405-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50405-152">Next steps</span></span>
<!-- Links -->
* [<span data-ttu-id="50405-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide de Yeoman)</span><span class="sxs-lookup"><span data-stu-id="50405-153">Create and deploy your first Service Fabric Java application on Linux using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="50405-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse (Créer et déployer votre première application Java Service Fabric sur Linux à l’aide du plug-in Service Fabric pour Eclipse)</span><span class="sxs-lookup"><span data-stu-id="50405-154">Create and deploy your first Service Fabric Java application on Linux using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="50405-155">Créer un cluster Service Fabric Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="50405-155">Create a Service Fabric cluster in hello Azure portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="50405-156">Créer un cluster Service Fabric à l’aide de hello Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="50405-156">Create a Service Fabric cluster using hello Azure Resource Manager</span></span>](service-fabric-cluster-creation-via-arm.md)
* [<span data-ttu-id="50405-157">Comprendre le modèle d’application hello Service Fabric</span><span class="sxs-lookup"><span data-stu-id="50405-157">Understand hello Service Fabric application model</span></span>](service-fabric-application-model.md)

<!-- Images -->
[cluster-setup-script]: ./media/service-fabric-get-started-mac/cluster-setup-mac.png
[sfx-mac]: ./media/service-fabric-get-started-mac/sfx-mac.png
[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-mac/sf-eclipse-plugin-install.png
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
