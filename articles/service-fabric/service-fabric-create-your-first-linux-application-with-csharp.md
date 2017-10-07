---
title: "aaaCreate votre première application Azure microservices sur Linux à l’aide de C# | Documents Microsoft"
description: "Créer et déployer une application Service Fabric à l’aide de C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="248c0-103">Créer votre première application Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="248c0-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="248c0-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="248c0-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="248c0-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="248c0-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="248c0-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="248c0-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="248c0-107">Service Fabric fournit des Kits de développement logiciel (SDK) pour générer des services Linux dans .NET Core et Java.</span><span class="sxs-lookup"><span data-stu-id="248c0-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="248c0-108">Dans ce didacticiel, nous abordons la façon dont une application pour Linux et génération d’un service à l’aide de c# (.NET Core) de toocreate.</span><span class="sxs-lookup"><span data-stu-id="248c0-108">In this tutorial, we look at how toocreate an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="248c0-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="248c0-109">Prerequisites</span></span>
<span data-ttu-id="248c0-110">Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="248c0-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="248c0-111">Si vous utilisez Mac OS X, vous pouvez [configurer un environnement Linux à boîtier unique sur une machine virtuelle à l’aide de Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="248c0-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="248c0-112">Vous pouvez également tooinstall hello [CLI de l’infrastructure de Service](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="248c0-112">You will also want tooinstall hello [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-hello-generators-for-csharp"></a><span data-ttu-id="248c0-113">Installer et configurer des générateurs de hello pour CSharp</span><span class="sxs-lookup"><span data-stu-id="248c0-113">Install and set up hello generators for CSharp</span></span>
<span data-ttu-id="248c0-114">Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric CSharp à partir du terminal à l’aide du générateur de modèles Yeoman.</span><span class="sxs-lookup"><span data-stu-id="248c0-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="248c0-115">Veuillez suivre les étapes de hello ci-dessous tooensure que vous avez Générateur de modèle yeoman hello Service Fabric pour CSharp vous travaillez sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="248c0-115">Please follow hello steps below tooensure you have hello Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="248c0-116">Installer nodejs et NPM sur votre machine</span><span class="sxs-lookup"><span data-stu-id="248c0-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="248c0-117">Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="248c0-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="248c0-118">Installer le Générateur d’applications hello Service Fabric yo Java à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="248c0-118">Install hello Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a><span data-ttu-id="248c0-119">Créer l’application hello</span><span class="sxs-lookup"><span data-stu-id="248c0-119">Create hello application</span></span>
<span data-ttu-id="248c0-120">Une application de Service Fabric peut contenir un ou plusieurs services, chacun avec un rôle spécifique dans la fonctionnalité de l’application hello de remise.</span><span class="sxs-lookup"><span data-stu-id="248c0-120">A Service Fabric application can contain one or more services, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="248c0-121">Hello Service Fabric [Yeoman](http://yeoman.io/) toocreate facile rend générateur pour CSharp, que vous avez installés dans la dernière étape, votre premier service et tooadd plus ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="248c0-121">hello Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy toocreate your first service and tooadd more later.</span></span> <span data-ttu-id="248c0-122">Nous allons utiliser Yeoman toocreate une application avec un seul service.</span><span class="sxs-lookup"><span data-stu-id="248c0-122">Let's use Yeoman toocreate an application with a single service.</span></span>

1. <span data-ttu-id="248c0-123">Dans un terminal, tapez Bonjour suivant toostart commande Création de la structure de hello :`yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="248c0-123">In a terminal, type hello following command toostart building hello scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="248c0-124">Donnez un nom à votre application.</span><span class="sxs-lookup"><span data-stu-id="248c0-124">Name your application.</span></span>
3. <span data-ttu-id="248c0-125">Choisissez le type hello de votre premier service et nommez-le.</span><span class="sxs-lookup"><span data-stu-id="248c0-125">Choose hello type of your first service and name it.</span></span> <span data-ttu-id="248c0-126">Pour des raisons de hello de ce didacticiel, nous choisissons un Service d’acteur fiable.</span><span class="sxs-lookup"><span data-stu-id="248c0-126">For hello purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Générateur Yeoman Service Fabric pour C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="248c0-128">Pour plus d’informations sur les options de hello, consultez [Service Fabric, vue d’ensemble du modèle de programmation](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="248c0-128">For more information about hello options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-hello-application"></a><span data-ttu-id="248c0-129">Générez l’application hello</span><span class="sxs-lookup"><span data-stu-id="248c0-129">Build hello application</span></span>
<span data-ttu-id="248c0-130">modèles de Service Fabric Yeoman Hello incluent un script de génération que vous pouvez utiliser l’application hello toobuild hello terminal (après la navigation dans le dossier d’application toohello).</span><span class="sxs-lookup"><span data-stu-id="248c0-130">hello Service Fabric Yeoman templates include a build script that you can use toobuild hello app from hello terminal (after navigating toohello application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-hello-application"></a><span data-ttu-id="248c0-131">Déployer l’application hello</span><span class="sxs-lookup"><span data-stu-id="248c0-131">Deploy hello application</span></span>

<span data-ttu-id="248c0-132">Une fois que l’application hello est générée, vous pouvez le déployer de cluster local de toohello.</span><span class="sxs-lookup"><span data-stu-id="248c0-132">Once hello application is built, you can deploy it toohello local cluster.</span></span>

1. <span data-ttu-id="248c0-133">Connectez le cluster Service Fabric local de toohello.</span><span class="sxs-lookup"><span data-stu-id="248c0-133">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="248c0-134">Exécuter le script d’installation hello fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-134">Run hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="248c0-135">L’application hello généré déploiement est même hello comme toute autre application de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="248c0-135">Deploying hello built application is hello same as any other Service Fabric application.</span></span> <span data-ttu-id="248c0-136">Consultez la documentation de hello sur [gérer une application Service Fabric avec hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="248c0-136">See hello documentation on [managing a Service Fabric application with hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="248c0-137">Commandes de toothese de paramètres sont accessibles dans les manifestes hello généré à l’intérieur du package d’application hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-137">Parameters toothese commands can be found in hello generated manifests inside hello application package.</span></span>

<span data-ttu-id="248c0-138">Une fois que l’application hello a été déployée, ouvrez un navigateur et accédez à [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) à [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="248c0-138">Once hello application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="248c0-139">Développez ensuite hello **Applications** nœud et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-139">Then, expand hello **Applications** node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

## <a name="start-hello-test-client-and-perform-a-failover"></a><span data-ttu-id="248c0-140">Démarrer le client test hello et effectuer un basculement</span><span class="sxs-lookup"><span data-stu-id="248c0-140">Start hello test client and perform a failover</span></span>
<span data-ttu-id="248c0-141">Les projets d’acteur n’effectuent aucune opération automatiquement.</span><span class="sxs-lookup"><span data-stu-id="248c0-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="248c0-142">Ils ont besoin d’un autre toosend de service ou le client les messages.</span><span class="sxs-lookup"><span data-stu-id="248c0-142">They require another service or client toosend them messages.</span></span> <span data-ttu-id="248c0-143">modèle d’acteur Hello inclut un script de test simple que vous pouvez utiliser toointeract avec le service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-143">hello actor template includes a simple test script that you can use toointeract with hello actor service.</span></span>

1. <span data-ttu-id="248c0-144">Exécutez le script hello à l’aide de la sortie de hello hello espion utilitaire toosee du service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-144">Run hello script using hello watch utility toosee hello output of hello actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="248c0-145">Dans l’Explorateur de l’infrastructure de Service, recherchez le nœud qui héberge le réplica principal de hello pour le service d’acteur hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-145">In Service Fabric Explorer, locate node hosting hello primary replica for hello actor service.</span></span> <span data-ttu-id="248c0-146">Dans la capture d’écran de hello ci-dessous, il est nœud 3.</span><span class="sxs-lookup"><span data-stu-id="248c0-146">In hello screenshot below, it is node 3.</span></span>

    ![Réplica principal de recherche hello dans Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="248c0-148">Cliquez sur le nœud hello vous trouvé à l’étape précédente de hello, puis sélectionnez **désactiver (Redémarrer)** à partir du menu d’Actions hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-148">Click hello node you found in hello previous step, then select **Deactivate (restart)** from hello Actions menu.</span></span> <span data-ttu-id="248c0-149">Cette action redémarre un seul nœud dans votre application forcée d’un réplica secondaire de basculement tooa, en cours d’exécution sur un autre nœud de cluster local.</span><span class="sxs-lookup"><span data-stu-id="248c0-149">This action restarts one node in your local cluster forcing a failover tooa secondary replica running on another node.</span></span> <span data-ttu-id="248c0-150">Quand vous effectuez cette action, payer sortie de toohello une attention particulière à partir de client de test hello et notez que ce compteur hello continue tooincrement malgré hello basculement.</span><span class="sxs-lookup"><span data-stu-id="248c0-150">As you perform this action, pay attention toohello output from hello test client and note that hello counter continues tooincrement despite hello failover.</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="248c0-151">Ajout d’application existante de plusieurs services tooan</span><span class="sxs-lookup"><span data-stu-id="248c0-151">Adding more services tooan existing application</span></span>

<span data-ttu-id="248c0-152">tooadd une autre application de tooan service déjà créé à l’aide de `yo`, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="248c0-152">tooadd another service tooan application already created using `yo`, perform hello following steps:</span></span>
1. <span data-ttu-id="248c0-153">Modifier la racine toohello du répertoire d’application existant hello.</span><span class="sxs-lookup"><span data-stu-id="248c0-153">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="248c0-154">Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.</span><span class="sxs-lookup"><span data-stu-id="248c0-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="248c0-155">Exécutez `yo azuresfcsharp:AddService`.</span><span class="sxs-lookup"><span data-stu-id="248c0-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-toocsproj"></a><span data-ttu-id="248c0-156">Migration à partir de project.json too.csproj</span><span class="sxs-lookup"><span data-stu-id="248c0-156">Migrating from project.json too.csproj</span></span>
1. <span data-ttu-id="248c0-157">Vous pouvez migrer les format hello project.json toocsproj 'dotnet migrate' dans le répertoire racine du projet en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="248c0-157">Running 'dotnet migrate' in project root directory will migrate all hello project.json toocsproj format.</span></span>
2. <span data-ttu-id="248c0-158">Mise à jour hello projet référence en conséquence les fichiers toocsproj dans les fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="248c0-158">Update hello project references accordingly toocsproj files in project files.</span></span>
3. <span data-ttu-id="248c0-159">Mettre à jour hello fichier noms toocsproj fichiers projet dans build.sh.</span><span class="sxs-lookup"><span data-stu-id="248c0-159">Update hello project file names toocsproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="248c0-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="248c0-160">Next steps</span></span>

* [<span data-ttu-id="248c0-161">Présentation des Acteurs fiables Service Fabric</span><span class="sxs-lookup"><span data-stu-id="248c0-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="248c0-162">Interaction avec les clusters de l’infrastructure de Service à l’aide de hello CLI de l’infrastructure de Service</span><span class="sxs-lookup"><span data-stu-id="248c0-162">Interacting with Service Fabric clusters using hello Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="248c0-163">En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="248c0-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="248c0-164">Prise en main de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="248c0-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
