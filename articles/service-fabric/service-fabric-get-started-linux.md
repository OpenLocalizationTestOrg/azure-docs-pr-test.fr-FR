---
title: "aaaSet de votre environnement de développement sur Linux | Documents Microsoft"
description: "Installer le runtime de hello et Kit de développement logiciel et créez un cluster de développement local sur Linux. Après avoir terminé cette installation, vous serez prêt toobuild applications."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a><span data-ttu-id="76726-104">Préparer votre environnement de développement sur Linux</span><span class="sxs-lookup"><span data-stu-id="76726-104">Prepare your development environment on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="76726-105">Windows</span><span class="sxs-lookup"><span data-stu-id="76726-105">Windows</span></span>](service-fabric-get-started.md)
> * [<span data-ttu-id="76726-106">Linux</span><span class="sxs-lookup"><span data-stu-id="76726-106">Linux</span></span>](service-fabric-get-started-linux.md)
> * [<span data-ttu-id="76726-107">OSX</span><span class="sxs-lookup"><span data-stu-id="76726-107">OSX</span></span>](service-fabric-get-started-mac.md)
>
>  

<span data-ttu-id="76726-108">toodeploy et exécutez [les applications Azure Service Fabric](service-fabric-application-model.md) sur votre ordinateur de développement Linux, installer hello runtime et le Kit de développement logiciel courants.</span><span class="sxs-lookup"><span data-stu-id="76726-108">toodeploy and run [Azure Service Fabric applications](service-fabric-application-model.md) on your Linux development machine, install hello runtime and common SDK.</span></span> <span data-ttu-id="76726-109">Vous pouvez également installer les Kits de développement logiciel (SDK) facultatifs pour Java et .NET Core.</span><span class="sxs-lookup"><span data-stu-id="76726-109">You can also install optional SDKs for Java and .NET Core.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="76726-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="76726-110">Prerequisites</span></span>

<span data-ttu-id="76726-111">Hello versions de système d’exploitation suivantes est prises en charge pour le développement :</span><span class="sxs-lookup"><span data-stu-id="76726-111">hello following operating system versions are supported for development:</span></span>

* <span data-ttu-id="76726-112">Ubuntu 16.04 (`Xenial Xerus`)</span><span class="sxs-lookup"><span data-stu-id="76726-112">Ubuntu 16.04 (`Xenial Xerus`)</span></span>

## <a name="update-your-apt-sources"></a><span data-ttu-id="76726-113">Mise à jour des sources APT</span><span class="sxs-lookup"><span data-stu-id="76726-113">Update your APT sources</span></span>
<span data-ttu-id="76726-114">tooinstall hello SDK et hello runtime associé package via l’outil de ligne de commande get-apt hello, vous devez tout d’abord mettre à jour vos sources de l’outil de mise en package avancées (APT).</span><span class="sxs-lookup"><span data-stu-id="76726-114">tooinstall hello SDK and hello associated runtime package via hello apt-get command-line tool, you must first update your Advanced Packaging Tool (APT) sources.</span></span>

1. <span data-ttu-id="76726-115">Ouvrez un terminal.</span><span class="sxs-lookup"><span data-stu-id="76726-115">Open a terminal.</span></span>
2. <span data-ttu-id="76726-116">Ajouter la liste de sources de hello Service Fabric référentiel tooyour.</span><span class="sxs-lookup"><span data-stu-id="76726-116">Add hello Service Fabric repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. <span data-ttu-id="76726-117">Ajouter hello `dotnet` liste des sources de référentiel tooyour.</span><span class="sxs-lookup"><span data-stu-id="76726-117">Add hello `dotnet` repo tooyour sources list.</span></span>

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. <span data-ttu-id="76726-118">Ajouter hello nouvelle garde de confidentialité Gnu (GnuPG ou GPG) clé tooyour APT trousseau de clés.</span><span class="sxs-lookup"><span data-stu-id="76726-118">Add hello new Gnu Privacy Guard (GnuPG, or GPG) key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. <span data-ttu-id="76726-119">Ajoutez hello officiel Docker GPG tooyour clé APT porte-clé.</span><span class="sxs-lookup"><span data-stu-id="76726-119">Add hello official Docker GPG key tooyour APT keyring.</span></span>

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. <span data-ttu-id="76726-120">Configurer le référentiel de Docker hello.</span><span class="sxs-lookup"><span data-stu-id="76726-120">Set up hello Docker repository.</span></span>

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. <span data-ttu-id="76726-121">Actualiser votre package listes selon hello nouvellement ajouté référentiels.</span><span class="sxs-lookup"><span data-stu-id="76726-121">Refresh your package lists based on hello newly added repositories.</span></span>

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a><span data-ttu-id="76726-122">Installer et configurer hello Kit de développement logiciel pour le programme d’installation de cluster local</span><span class="sxs-lookup"><span data-stu-id="76726-122">Install and set up hello SDK for local cluster setup</span></span>

<span data-ttu-id="76726-123">Une fois que vous avez mis à jour vos sources, vous pouvez installer hello SDK.</span><span class="sxs-lookup"><span data-stu-id="76726-123">After you have updated your sources, you can install hello SDK.</span></span> <span data-ttu-id="76726-124">Installer le package de Service Fabric SDK hello, vérifier l’installation de hello et acceptez le contrat de licence toohello.</span><span class="sxs-lookup"><span data-stu-id="76726-124">Install hello Service Fabric SDK package, confirm hello installation, and agree toohello license agreement.</span></span>

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   <span data-ttu-id="76726-125">Hello commandes suivantes automatisent acceptant licence hello pour les packages de Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="76726-125">hello following commands automate accepting hello license for Service Fabric packages:</span></span>
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a><span data-ttu-id="76726-126">Configurer un cluster local</span><span class="sxs-lookup"><span data-stu-id="76726-126">Set up a local cluster</span></span>
  <span data-ttu-id="76726-127">Si l’installation de hello est réussie, vous devez être en mesure de toostart un cluster local.</span><span class="sxs-lookup"><span data-stu-id="76726-127">If hello installation is successful, you should be able toostart a local cluster.</span></span>

  1. <span data-ttu-id="76726-128">Exécutez le script d’installation de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="76726-128">Run hello cluster setup script.</span></span>

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. <span data-ttu-id="76726-129">Ouvrez un navigateur web et accédez trop[Service Fabric Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="76726-129">Open a web browser and go too[Service Fabric Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="76726-130">Si le cluster de hello a démarré, vous devez voir le tableau de bord de Service Fabric Explorer hello.</span><span class="sxs-lookup"><span data-stu-id="76726-130">If hello cluster has started, you should see hello Service Fabric Explorer dashboard.</span></span>

      ![Service Fabric Explorer sur Linux][sfx-linux]

  <span data-ttu-id="76726-132">À ce stade, vous pouvez déployer des packages d’application Service Fabric préconfigurés ou de nouveaux packages basés sur des conteneurs invités ou des exécutables invités.</span><span class="sxs-lookup"><span data-stu-id="76726-132">At this point, you can deploy pre-built Service Fabric application packages or new ones based on guest containers or guest executables.</span></span> <span data-ttu-id="76726-133">toobuild de nouveaux services à l’aide de Java de hello ou les kits de développement logiciel de .NET Core, les étapes hello facultatives d’installation qui sont fournies dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="76726-133">toobuild new services by using hello Java or .NET Core SDKs, follow hello optional setup steps that are provided in subsequent sections.</span></span>


  > [!NOTE]
  > <span data-ttu-id="76726-134">Les clusters autonomes ne sont pas pris en charge sous Linux.</span><span class="sxs-lookup"><span data-stu-id="76726-134">Standalone clusters aren't supported in Linux.</span></span> <span data-ttu-id="76726-135">prend en charge l’aperçu Hello uniquement une case et Azure Linux des clusters comportant plusieurs ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="76726-135">hello preview supports only one-box and Azure Linux multi-machine clusters.</span></span>
  >

## <a name="set-up-hello-service-fabric-cli"></a><span data-ttu-id="76726-136">Configurer hello CLI de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="76726-136">Set up hello Service Fabric CLI</span></span>

<span data-ttu-id="76726-137">Hello [Service Fabric CLI](service-fabric-cli.md) dispose des commandes pour interagir avec les entités de Service Fabric, y compris des clusters et des applications.</span><span class="sxs-lookup"><span data-stu-id="76726-137">hello [Service Fabric CLI](service-fabric-cli.md) has commands for interacting with Service Fabric entities, including clusters and applications.</span></span> <span data-ttu-id="76726-138">Il est basé sur python, soyez sûr toohave python et pip installé avant de poursuivre hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="76726-138">It is based on python, so be sure toohave python and pip installed before you proceed with hello following command:</span></span>

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a><span data-ttu-id="76726-139">Installer et configurer des générateurs de hello pour les conteneurs et les fichiers exécutables de l’invité</span><span class="sxs-lookup"><span data-stu-id="76726-139">Install and set up hello generators for containers and guest-executables</span></span>
<span data-ttu-id="76726-140">Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric depuis le terminal à l’aide du générateur de modèle Yeoman.</span><span class="sxs-lookup"><span data-stu-id="76726-140">Service Fabric provides scaffolding tools which will help you create a Service Fabric applications from terminal using Yeoman template generator.</span></span> <span data-ttu-id="76726-141">Veuillez suivre les étapes de hello ci-dessous tooensure que vous possédez Générateur de modèle yeoman hello Service Fabric pour travailler sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="76726-141">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for working on your machine.</span></span>

1. <span data-ttu-id="76726-142">Installer nodejs et NPM sur votre machine</span><span class="sxs-lookup"><span data-stu-id="76726-142">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="76726-143">Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="76726-143">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="76726-144">Installer le Générateur de conteneur de Service Fabric yo hello et Générateur d’execuatble invité à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="76726-144">Install hello Service Fabric Yeo container generator and guest execuatble generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

<span data-ttu-id="76726-145">Après avoir installé hello au-dessus des générateurs, vous devez être en mesure de toocreate des applications avec les services d’invité exécutable ou un conteneur en exécutant `yo azuresfguest` ou `yo azuresfcontainer` respectivement.</span><span class="sxs-lookup"><span data-stu-id="76726-145">After you have installed hello above generators, you should be able toocreate apps with guest executable or container services by running `yo azuresfguest` or `yo azuresfcontainer` respectively.</span></span>

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a><span data-ttu-id="76726-146">Installer les artefacts Java hello nécessaires (facultatifs, si vous souhaitez que toouse hello Java de modèles de programmation)</span><span class="sxs-lookup"><span data-stu-id="76726-146">Install hello necessary Java artifacts (optional, if you want toouse hello Java programming models)</span></span>

<span data-ttu-id="76726-147">les services de Service Fabric toobuild à l’aide de Java, vous assurer 1.8 JDK installé avec Gradle qui est utilisé pour exécuter des tâches de génération.</span><span class="sxs-lookup"><span data-stu-id="76726-147">toobuild Service Fabric services using Java, ensure you have JDK 1.8 installed along with Gradle which is used for running build tasks.</span></span> <span data-ttu-id="76726-148">Hello suivant extrait installe Open JDK 1.8, ainsi que de Gradle.</span><span class="sxs-lookup"><span data-stu-id="76726-148">hello following snippet installs Open JDK 1.8 along with Gradle.</span></span> <span data-ttu-id="76726-149">bibliothèques de Service Fabric Java Hello sont extraites à partir de Maven.</span><span class="sxs-lookup"><span data-stu-id="76726-149">hello Service Fabric Java libraries are pulled from Maven.</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a><span data-ttu-id="76726-150">Installer hello Neon Eclipse plug-in (facultatif)</span><span class="sxs-lookup"><span data-stu-id="76726-150">Install hello Eclipse Neon plug-in (optional)</span></span>

<span data-ttu-id="76726-151">Vous pouvez installer hello Eclipse plug-in pour l’infrastructure de Service à partir de hello **IDE Eclipse pour développeurs Java**.</span><span class="sxs-lookup"><span data-stu-id="76726-151">You can install hello Eclipse plug-in for Service Fabric from within hello **Eclipse IDE for Java Developers**.</span></span> <span data-ttu-id="76726-152">Vous pouvez utiliser les applications exécutables d’Eclipse toocreate Service Fabric invité et les applications de conteneur dans les applications de l’infrastructure Java tooService Ajout.</span><span class="sxs-lookup"><span data-stu-id="76726-152">You can use Eclipse toocreate Service Fabric guest executable applications and container applications in addition tooService Fabric Java applications.</span></span>

1. <span data-ttu-id="76726-153">Dans Eclipse, assurez-vous qu’avoir dernière Eclipse Neon hello version la plus récente Buildship (1.0.17 ou version ultérieure) installé.</span><span class="sxs-lookup"><span data-stu-id="76726-153">In Eclipse, ensure that you have latest Eclipse Neon and hello latest Buildship version (1.0.17 or later) installed.</span></span> <span data-ttu-id="76726-154">Vous pouvez vérifier les versions des composants installés hello en sélectionnant **aide** > **détails de l’Installation**.</span><span class="sxs-lookup"><span data-stu-id="76726-154">You can check hello versions of installed components by selecting **Help** > **Installation Details**.</span></span> <span data-ttu-id="76726-155">Vous pouvez mettre à jour Buildship à l’aide d’instructions hello à [Eclipse Buildship : Eclipse Plug-ins pour Gradle][buildship-update].</span><span class="sxs-lookup"><span data-stu-id="76726-155">You can update Buildship by using hello instructions at [Eclipse Buildship: Eclipse Plug-ins for Gradle][buildship-update].</span></span>

2. <span data-ttu-id="76726-156">tooinstall hello sélectionnez de plug-in, Service Fabric **aide** > **installer le nouveau logiciel**.</span><span class="sxs-lookup"><span data-stu-id="76726-156">tooinstall hello Service Fabric plug-in, select **Help** > **Install New Software**.</span></span>

3. <span data-ttu-id="76726-157">Bonjour **travailler avec** , tapez **http://dl.microsoft.com/eclipse**.</span><span class="sxs-lookup"><span data-stu-id="76726-157">In hello **Work with** box, type **http://dl.microsoft.com/eclipse**.</span></span>

4. <span data-ttu-id="76726-158">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="76726-158">Click **Add**.</span></span>

    ![page de logiciels disponibles Hello][sf-eclipse-plugin]

5. <span data-ttu-id="76726-160">Sélectionnez hello **ServiceFabric** plug-in, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="76726-160">Select hello **ServiceFabric** plug-in, and then click **Next**.</span></span>

6. <span data-ttu-id="76726-161">Complétez les étapes d’installation hello et puis acceptez le contrat de licence utilisateur final hello.</span><span class="sxs-lookup"><span data-stu-id="76726-161">Complete hello installation steps, and then accept hello end-user license agreement.</span></span>

<span data-ttu-id="76726-162">Si vous avez déjà hello Eclipse de l’infrastructure du Service plug-in installé, assurez-vous que vous avez la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="76726-162">If you already have hello Service Fabric Eclipse plug-in installed, make sure that you have hello latest version.</span></span> <span data-ttu-id="76726-163">Vous pouvez vérifier en sélectionnant **aide** > **détails de l’Installation** et puis en recherchant l’infrastructure de Service dans la liste hello des plug-ins installés. Si une version plus récente est disponible, sélectionnez **Mettre à jour**.</span><span class="sxs-lookup"><span data-stu-id="76726-163">You can check by selecting **Help** > **Installation Details** and then searching for Service Fabric in hello list of installed plug-ins. If a newer version is available, select **Update**.</span></span>

<span data-ttu-id="76726-164">Pour plus d’informations, consultez la section [Plug-in Service Fabric pour le développement d’applications Java sous Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="76726-164">For more information, see [Service Fabric plug-in for Eclipse Java application development](service-fabric-get-started-eclipse.md).</span></span>


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a><span data-ttu-id="76726-165">Installer hello .NET Core Kit de développement logiciel (facultatif, si vous souhaitez que les modèles de programmation .NET Core hello toouse)</span><span class="sxs-lookup"><span data-stu-id="76726-165">Install hello .NET Core SDK (optional, if you want toouse hello .NET Core programming models)</span></span>
<span data-ttu-id="76726-166">Hello .NET Core SDK fournit des bibliothèques de hello et modèles qui sont des services de Service Fabric toobuild requis avec le .NET Core.</span><span class="sxs-lookup"><span data-stu-id="76726-166">hello .NET Core SDK provides hello libraries and templates that are required toobuild Service Fabric services with .NET Core.</span></span> <span data-ttu-id="76726-167">Installer de kit de développement .NET Core hello par les éléments suivants de hello en cours d’exécution :</span><span class="sxs-lookup"><span data-stu-id="76726-167">Install hello .NET Core SDK package by running hello following -</span></span>

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a><span data-ttu-id="76726-168">Hello de mise à jour SDK et d’exécution</span><span class="sxs-lookup"><span data-stu-id="76726-168">Update hello SDK and runtime</span></span>

<span data-ttu-id="76726-169">version la plus récente toohello tooupdate de hello SDK et d’exécution, exécutez hello suivant les commandes (désélectionnez les kits de développement logiciel hello que vous ne souhaitez pas) :</span><span class="sxs-lookup"><span data-stu-id="76726-169">tooupdate toohello latest version of hello SDK and runtime, run hello following commands (deselect hello SDKs that you don't want):</span></span>

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
<span data-ttu-id="76726-170">tooupdate hello Kit de développement logiciel Java fichiers binaires à partir de Maven, vous devez tooupdate détails sur la version hello du binaire correspondant de hello Bonjour ``build.gradle`` version plus récente du fichier toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="76726-170">tooupdate hello Java SDK binaries from Maven, you need tooupdate hello version details of hello corresponding binary in hello ``build.gradle`` file toopoint toohello latest version.</span></span> <span data-ttu-id="76726-171">tooknow là où vous avez besoin tooupdate version de hello, vous pouvez faire référence tooany ``build.gradle`` fichier dans les exemples de prise en main de Service Fabric [ici](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="76726-171">tooknow exactly where you need tooupdate hello version, you can refer tooany ``build.gradle`` file in Service Fabric getting-started samples [here](https://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>

> [!NOTE]
> <span data-ttu-id="76726-172">Mise à jour les packages hello risque de votre toostop de cluster de développement local en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="76726-172">Updating hello packages might cause your local development cluster toostop running.</span></span> <span data-ttu-id="76726-173">Redémarrez votre cluster local après une mise à niveau en suivant les instructions de hello sur cette page.</span><span class="sxs-lookup"><span data-stu-id="76726-173">Restart your local cluster after an upgrade by following hello instructions on this page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="76726-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="76726-174">Next steps</span></span>

* [<span data-ttu-id="76726-175">Créer et déployer votre première application Java Service Fabric sous Linux à l’aide de Yeoman</span><span class="sxs-lookup"><span data-stu-id="76726-175">Create and deploy your first Service Fabric Java application on Linux by using Yeoman</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
* [<span data-ttu-id="76726-176">Créer et déployer votre première application Java Service Fabric sous Linux à l’aide du plug-in Service Fabric pour Eclipse</span><span class="sxs-lookup"><span data-stu-id="76726-176">Create and deploy your first Service Fabric Java application on Linux by using Service Fabric Plugin for Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="76726-177">Create your first Java application on Linux (Créer votre première application Java sur Linux)</span><span class="sxs-lookup"><span data-stu-id="76726-177">Create your first CSharp application on Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
* [<span data-ttu-id="76726-178">Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)</span><span class="sxs-lookup"><span data-stu-id="76726-178">Prepare your development environment on OSX</span></span>](service-fabric-get-started-mac.md)
* [<span data-ttu-id="76726-179">Utiliser hello Service Fabric CLI toomanage vos applications</span><span class="sxs-lookup"><span data-stu-id="76726-179">Use hello Service Fabric CLI toomanage your applications</span></span>](service-fabric-application-lifecycle-sfctl.md)
* [<span data-ttu-id="76726-180">Différences entre Service Fabric Windows/Linux</span><span class="sxs-lookup"><span data-stu-id="76726-180">Service Fabric Windows/Linux differences</span></span>](service-fabric-linux-windows-differences.md)
* [<span data-ttu-id="76726-181">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="76726-181">Get started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
