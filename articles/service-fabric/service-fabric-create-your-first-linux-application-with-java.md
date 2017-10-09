---
title: aaaCreate une application de Java Azure Service Fabric acteurs fiable sur Linux | Documents Microsoft
description: "Découvrez comment toocreate et déployer une application d’acteurs fiable Java Service Fabric dans cinq minutes."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="7ba94-103">Création de votre première application Java Service Fabric Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="7ba94-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ba94-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="7ba94-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="7ba94-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="7ba94-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="7ba94-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="7ba94-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="7ba94-107">Ce guide de démarrage rapide vous aide à créer votre première application Azure Service Fabric Java dans un environnement de développement Linux en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7ba94-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="7ba94-108">Lorsque vous avez terminé, vous avez une application de service unique simple Java en cours d’exécution sur le cluster de développement local hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-108">When you are finished, you'll have a simple Java single-service application running on hello local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="7ba94-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7ba94-109">Prerequisites</span></span>
<span data-ttu-id="7ba94-110">Avant de commencer, installez hello Service Fabric SDK hello Service Fabric CLI et le programme d’installation d’un cluster de développement dans votre [environnement de développement Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7ba94-110">Before you get started, install hello Service Fabric SDK, hello Service Fabric CLI, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="7ba94-111">Si vous utilisez Mac OS X, vous pouvez [configurer un environnement de développement Linux sur une machine virtuelle à l’aide de Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="7ba94-111">If you are using Mac OS X, you can [set up a Linux development environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="7ba94-112">Vous pouvez également tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7ba94-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-hello-generators-for-java"></a><span data-ttu-id="7ba94-113">Installer et configurer des générateurs de hello pour Java</span><span class="sxs-lookup"><span data-stu-id="7ba94-113">Install and set up hello generators for Java</span></span>
<span data-ttu-id="7ba94-114">Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Java Service Fabric à partir d’un terminal à l’aide du générateur de modèle Yeoman.</span><span class="sxs-lookup"><span data-stu-id="7ba94-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="7ba94-115">Veuillez suivre les étapes de hello ci-dessous tooensure que vous avez Générateur de modèle yeoman hello Service Fabric pour Java vous travaillez sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7ba94-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for Java working on your machine.</span></span>
1. <span data-ttu-id="7ba94-116">Installer nodejs et NPM sur votre machine</span><span class="sxs-lookup"><span data-stu-id="7ba94-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="7ba94-117">Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="7ba94-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="7ba94-118">Installer le Générateur d’applications hello Service Fabric yo Java à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="7ba94-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a><span data-ttu-id="7ba94-119">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="7ba94-119">Create hello application</span></span>
<span data-ttu-id="7ba94-120">Une application de Service Fabric contient un ou plusieurs services, chacun avec un rôle spécifique dans la fonctionnalité de l’application hello de remise.</span><span class="sxs-lookup"><span data-stu-id="7ba94-120">A Service Fabric application contains one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="7ba94-121">Générateur Hello vous avez installé dans la dernière section de hello, rend facile toocreate votre premier service et tooadd plus ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="7ba94-121">hello generator you installed in hello last section, makes it easy toocreate your first service and tooadd more later.</span></span>  <span data-ttu-id="7ba94-122">Vous pouvez également créer, générer et déployer des applications Java Service Fabric à l’aide d’un plug-in d’Eclipse.</span><span class="sxs-lookup"><span data-stu-id="7ba94-122">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="7ba94-123">Consultez les instructions de [création et déploiement de votre première application Java à l’aide d’Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="7ba94-123">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="7ba94-124">Pour ce guide de démarrage rapide, utilisez Yeoman toocreate une application avec un service unique qui stocke et obtient une valeur de compteur.</span><span class="sxs-lookup"><span data-stu-id="7ba94-124">For this quick start, use Yeoman toocreate an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="7ba94-125">Saisissez ``yo azuresfjava`` dans un terminal.</span><span class="sxs-lookup"><span data-stu-id="7ba94-125">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="7ba94-126">Donnez un nom à votre application.</span><span class="sxs-lookup"><span data-stu-id="7ba94-126">Name your application.</span></span>
3. <span data-ttu-id="7ba94-127">Choisissez le type hello de votre premier service et nommez-le.</span><span class="sxs-lookup"><span data-stu-id="7ba94-127">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="7ba94-128">Pour ce didacticiel, choisissez un service Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="7ba94-128">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="7ba94-129">Pour plus d’informations sur hello autres types de services, consultez [Service Fabric, vue d’ensemble du modèle de programmation](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="7ba94-129">For more information about hello other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="7ba94-130">![Générateur Yeoman Service Fabric pour Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="7ba94-130">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

## <a name="build-hello-application"></a><span data-ttu-id="7ba94-131">Générez l’application hello</span><span class="sxs-lookup"><span data-stu-id="7ba94-131">Build hello application</span></span>
<span data-ttu-id="7ba94-132">modèles de Service Fabric Yeoman Hello incluent un script de génération pour [Gradle](https://gradle.org/), vous pouvez utiliser application hello toobuild hello Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="7ba94-132">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span>
<span data-ttu-id="7ba94-133">Les dépendances Java Service Fabric ont été extraites de Maven.</span><span class="sxs-lookup"><span data-stu-id="7ba94-133">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="7ba94-134">toobuild et utiliser des applications de Service Fabric Java hello, vous devez tooensure que JDK et Gradle sont installés.</span><span class="sxs-lookup"><span data-stu-id="7ba94-134">toobuild and work on hello Service Fabric Java applications, you need tooensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="7ba94-135">Si non encore installé, vous pouvez exécuter hello suivant tooinstall JDK(openjdk-8-jdk) et Gradle -</span><span class="sxs-lookup"><span data-stu-id="7ba94-135">If not yet installed, you can run hello following tooinstall JDK(openjdk-8-jdk) and Gradle -</span></span>

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

<span data-ttu-id="7ba94-136">toobuild et package d’application hello, exécutez hello suivante :</span><span class="sxs-lookup"><span data-stu-id="7ba94-136">toobuild and package hello application, run hello following:</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="7ba94-137">Déployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="7ba94-137">Deploy hello application</span></span>
<span data-ttu-id="7ba94-138">Une fois que l’application hello est générée, vous pouvez le déployer de cluster local de toohello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-138">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="7ba94-139">Connectez le cluster Service Fabric local de toohello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-139">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="7ba94-140">Exécuter le script d’installation hello fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-140">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="7ba94-141">L’application hello généré déploiement est même hello comme toute autre application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ba94-141">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="7ba94-142">Consultez la documentation de hello sur [gérer une application Service Fabric avec hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="7ba94-142">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="7ba94-143">Commandes de toothese de paramètres sont accessibles dans les manifestes hello généré à l’intérieur du package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-143">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="7ba94-144">Une fois que l’application hello a été déployée, ouvrez un navigateur et accédez à [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) à [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="7ba94-144">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="7ba94-145">Développez ensuite hello **Applications** nœud et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-145">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="7ba94-146">Démarrer le client test hello et effectuer un basculement</span><span class="sxs-lookup"><span data-stu-id="7ba94-146">Start hello test client and perform a failover</span></span>
<span data-ttu-id="7ba94-147">Acteurs ne font rien sur leurs propres, ils ont besoin d’un autre toosend de service ou le client les messages.</span><span class="sxs-lookup"><span data-stu-id="7ba94-147">Actors do not do anything on their own, they require another service or client toosend them messages.</span></span> <span data-ttu-id="7ba94-148">modèle d’acteur Hello inclut un script de test simple que vous pouvez utiliser toointeract avec le service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-148">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="7ba94-149">Exécutez le script hello à l’aide de la sortie de hello hello espion utilitaire toosee du service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-149">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>  <span data-ttu-id="7ba94-150">script de test Hello appelle hello `setCountAsync()` hello des appels de méthode sur hello acteur tooincrement un compteur, `getCountAsync()` méthode hello acteur tooget hello nouvelle valeur du compteur, et affiche cette valeur toohello console.</span><span class="sxs-lookup"><span data-stu-id="7ba94-150">hello test script calls hello `setCountAsync()` method on hello actor tooincrement a counter, calls hello `getCountAsync()` method on hello actor tooget hello new counter value, and displays that value toohello console.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="7ba94-151">Dans l’Explorateur de l’infrastructure de Service, recherchez hello nœud hébergement hello réplica principal pour le service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-151">In Service Fabric Explorer, locate hello node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="7ba94-152">Dans la capture d’écran de hello ci-dessous, il est nœud 3.</span><span class="sxs-lookup"><span data-stu-id="7ba94-152">In hello screenshot below, it is node 3.</span></span> <span data-ttu-id="7ba94-153">handles de réplica principal de service Hello lire et écrire des opérations.</span><span class="sxs-lookup"><span data-stu-id="7ba94-153">hello primary service replica handles read and write operations.</span></span>  <span data-ttu-id="7ba94-154">Modifications d’état de service sont ensuite répliquées toohello réplicas secondaires, en cours d’exécution sur les nœuds 0 et 1 dans hello capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7ba94-154">Changes in service state are then replicated out toohello secondary replicas, running on nodes 0 and 1 in hello screen shot below.</span></span>

    ![Réplica principal de recherche hello dans Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="7ba94-156">Dans **nœuds**, cliquez sur le nœud hello vous trouvé à l’étape précédente de hello, puis sélectionnez **désactiver (Redémarrer)** à partir du menu d’Actions hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-156">In **Nodes**, click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="7ba94-157">Cette action redémarre le nœud hello réplica du service principal hello en cours d’exécution et force un tooone de basculement des réplicas secondaires de hello en cours d’exécution sur un autre nœud.</span><span class="sxs-lookup"><span data-stu-id="7ba94-157">This action restarts hello node running hello primary service replica and forces a failover tooone of hello secondary replicas running on another node.</span></span>  <span data-ttu-id="7ba94-158">Ce réplica secondaire est promue tooprimary, un autre réplica secondaire est créé sur un autre nœud et réplica principal de hello commence des opérations de lecture/écriture de tootake.</span><span class="sxs-lookup"><span data-stu-id="7ba94-158">That secondary replica is promoted tooprimary, another secondary replica is created on a different node, and hello primary replica begins tootake read/write operations.</span></span> <span data-ttu-id="7ba94-159">Lors du redémarrage de nœud de hello, regardez la sortie hello de client de test hello et notez que ce compteur hello continue tooincrement malgré hello basculement.</span><span class="sxs-lookup"><span data-stu-id="7ba94-159">As hello node restarts, watch hello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="remove-hello-application"></a><span data-ttu-id="7ba94-160">Supprimer l’application hello</span><span class="sxs-lookup"><span data-stu-id="7ba94-160">Remove hello application</span></span>
<span data-ttu-id="7ba94-161">Utiliser le script de désinstallation hello fournie dans l’instance de l’application hello modèle toodelete hello, annulez l’inscription du package d’application hello et supprimer le package d’application hello à partir du magasin d’images du cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-161">Use hello uninstall script provided in hello template toodelete hello application instance, unregister hello application package, and remove hello application package from hello cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="7ba94-162">Dans l’Explorateur de l’infrastructure de Service, vous voyez qu’application hello et le type d’application n’apparaissent plus dans hello **Applications** nœud.</span><span class="sxs-lookup"><span data-stu-id="7ba94-162">In Service Fabric explorer you see that hello application and application type no longer appear in hello **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="7ba94-163">Bibliothèques Java Service Fabric sur Maven</span><span class="sxs-lookup"><span data-stu-id="7ba94-163">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="7ba94-164">Les bibliothèques Java Service Fabric ont été hébergées dans Maven.</span><span class="sxs-lookup"><span data-stu-id="7ba94-164">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="7ba94-165">Vous pouvez ajouter des dépendances de hello Bonjour ``pom.xml`` ou ``build.gradle`` de vos bibliothèques de Service Fabric Java toouse projets à partir de **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="7ba94-165">You can add hello dependencies in hello ``pom.xml`` or ``build.gradle`` of your projects toouse Service Fabric Java libraries from **mavenCentral**.</span></span>

### <a name="actors"></a><span data-ttu-id="7ba94-166">Acteurs</span><span class="sxs-lookup"><span data-stu-id="7ba94-166">Actors</span></span>

<span data-ttu-id="7ba94-167">Assistance Reliable Actor de Service Fabric pour votre application.</span><span class="sxs-lookup"><span data-stu-id="7ba94-167">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="7ba94-168">Services</span><span class="sxs-lookup"><span data-stu-id="7ba94-168">Services</span></span>

<span data-ttu-id="7ba94-169">Assistance des services sans état de Service Fabric pour votre application.</span><span class="sxs-lookup"><span data-stu-id="7ba94-169">Service Fabric Stateless Service support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="7ba94-170">Autres</span><span class="sxs-lookup"><span data-stu-id="7ba94-170">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="7ba94-171">Transport</span><span class="sxs-lookup"><span data-stu-id="7ba94-171">Transport</span></span>

<span data-ttu-id="7ba94-172">Assistance de la couche transport pour application Java Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7ba94-172">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="7ba94-173">Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service, sauf si vous effectuez la programmation au niveau de la couche de transport hello.</span><span class="sxs-lookup"><span data-stu-id="7ba94-173">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications, unless you program at hello transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="7ba94-174">Assista,ce Fabric</span><span class="sxs-lookup"><span data-stu-id="7ba94-174">Fabric support</span></span>

<span data-ttu-id="7ba94-175">Support de niveau système pour l’infrastructure de Service qui communique avec le runtime du Service Fabric toonative.</span><span class="sxs-lookup"><span data-stu-id="7ba94-175">System level support for Service Fabric, which talks toonative Service Fabric runtime.</span></span> <span data-ttu-id="7ba94-176">Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service.</span><span class="sxs-lookup"><span data-stu-id="7ba94-176">You do not need tooexplicitly add this dependency tooyour Reliable Actor or Service applications.</span></span> <span data-ttu-id="7ba94-177">Il obtient extraites automatiquement à partir de Maven, lorsque vous incluez hello autres dépendances ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7ba94-177">This gets fetched automatically from Maven, when you include hello other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a><span data-ttu-id="7ba94-178">Migration d’ancien toobe d’applications Java de l’infrastructure de Service utilisé avec Maven</span><span class="sxs-lookup"><span data-stu-id="7ba94-178">Migrating old Service Fabric Java applications toobe used with Maven</span></span>
<span data-ttu-id="7ba94-179">Nous avons déplacé récemment bibliothèques Service Fabric Java à partir du référentiel de tooMaven Service Fabric Java SDK.</span><span class="sxs-lookup"><span data-stu-id="7ba94-179">We have recently moved Service Fabric Java libraries from Service Fabric Java SDK tooMaven repository.</span></span> <span data-ttu-id="7ba94-180">Alors que hello nouvelles applications vous générez à l’aide de Yeoman ou Eclipse, générera une dernière version des projets mis à jour (qui seront en mesure de toowork avec Maven), vous pouvez mettre à jour votre Service Fabric existant sans état ou les applications Java acteur, qui utilisaient l’hello Service L’infrastructure du SDK Java précédemment, dépendances de Service Fabric Java hello toouse à partir de Maven.</span><span class="sxs-lookup"><span data-stu-id="7ba94-180">While hello new applications you generate using Yeoman or Eclipse, will generate latest updated projects (which will be able toowork with Maven), you can update your existing Service Fabric stateless or actor Java applications, which were using hello Service Fabric Java SDK earlier, toouse hello Service Fabric Java dependencies from Maven.</span></span> <span data-ttu-id="7ba94-181">Suivez les étapes de hello mentionnés [ici](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure votre ancienne application fonctionne avec Maven.</span><span class="sxs-lookup"><span data-stu-id="7ba94-181">Please follow hello steps mentioned [here](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure your older application works with Maven.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ba94-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7ba94-182">Next steps</span></span>

* [<span data-ttu-id="7ba94-183">Création de votre première application Java Service Fabric sur Linux à l’aide d’Eclipse</span><span class="sxs-lookup"><span data-stu-id="7ba94-183">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="7ba94-184">Présentation des Acteurs fiables Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ba94-184">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="7ba94-185">Interagir avec des clusters Service Fabric à l’aide de hello CLI de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="7ba94-185">Interact with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="7ba94-186">En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="7ba94-186">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="7ba94-187">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7ba94-187">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
