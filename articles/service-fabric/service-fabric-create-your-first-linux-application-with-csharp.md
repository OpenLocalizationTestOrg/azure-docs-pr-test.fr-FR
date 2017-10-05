---
title: "Créer votre première application de microservices Azure sur Linux à l’aide de C# | Microsoft Docs"
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
ms.openlocfilehash: adcafaa5522fcddc0a01eb1dc8deba04ebfc38f2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="f2dcf-103">Créer votre première application Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2dcf-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2dcf-104">C# - Windows</span><span class="sxs-lookup"><span data-stu-id="f2dcf-104">C# - Windows</span></span>](service-fabric-create-your-first-application-in-visual-studio.md)
> * [<span data-ttu-id="f2dcf-105">Java - Linux</span><span class="sxs-lookup"><span data-stu-id="f2dcf-105">Java - Linux</span></span>](service-fabric-create-your-first-linux-application-with-java.md)
> * [<span data-ttu-id="f2dcf-106">C# - Linux</span><span class="sxs-lookup"><span data-stu-id="f2dcf-106">C# - Linux</span></span>](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="f2dcf-107">Service Fabric fournit des Kits de développement logiciel (SDK) pour générer des services Linux dans .NET Core et Java.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="f2dcf-108">Dans ce didacticiel, nous apprenons à créer une application pour Linux et à générer un service à l’aide de C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="f2dcf-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2dcf-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f2dcf-109">Prerequisites</span></span>
<span data-ttu-id="f2dcf-110">Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f2dcf-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="f2dcf-111">Si vous utilisez Mac OS X, vous pouvez [configurer un environnement Linux à boîtier unique sur une machine virtuelle à l’aide de Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="f2dcf-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="f2dcf-112">Il vous sera également utile d’installer l’[interface de ligne de commande Service Fabric](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f2dcf-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-the-generators-for-csharp"></a><span data-ttu-id="f2dcf-113">Installer et configurer les générateurs de CSharp</span><span class="sxs-lookup"><span data-stu-id="f2dcf-113">Install and set up the generators for CSharp</span></span>
<span data-ttu-id="f2dcf-114">Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric CSharp à partir du terminal à l’aide du générateur de modèles Yeoman.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric CSharp application from terminal using Yeoman template generator.</span></span> <span data-ttu-id="f2dcf-115">Suivez les étapes ci-dessous pour vous assurer que le générateur de modèle yeoman Service Fabric de CSharp est en état de fonctionnement sur votre machine.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-115">Please follow the steps below to ensure you have the Service Fabric yeoman template generator for CSharp working on your machine.</span></span>
1. <span data-ttu-id="f2dcf-116">Installer nodejs et NPM sur votre machine</span><span class="sxs-lookup"><span data-stu-id="f2dcf-116">Install nodejs and NPM on your machine</span></span>

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. <span data-ttu-id="f2dcf-117">Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="f2dcf-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  sudo npm install -g yo
  ```
3. <span data-ttu-id="f2dcf-118">Installer le générateur d’applications Service Fabric Yeo Java à partir de NPM</span><span class="sxs-lookup"><span data-stu-id="f2dcf-118">Install the Service Fabric Yeo Java application generator from NPM</span></span>

  ```bash
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-the-application"></a><span data-ttu-id="f2dcf-119">Création de l’application</span><span class="sxs-lookup"><span data-stu-id="f2dcf-119">Create the application</span></span>
<span data-ttu-id="f2dcf-120">Une application Service Fabric peut contenir un ou plusieurs services, chacun ayant un rôle précis pour la fourniture de la fonctionnalité d’application.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="f2dcf-121">Le générateur Service Fabric [Yeoman](http://yeoman.io/) de CSharp, que vous avez installé lors de la dernière étape, facilite la création de votre premier service et vous aide à ajouter de nouveaux services ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for CSharp, which you installed in last step, makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="f2dcf-122">Nous utilisons Yeoman pour créer une application avec un seul service.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-122">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="f2dcf-123">Dans un terminal, tapez la commande suivante pour commencer la génération de modèles automatique : `yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="f2dcf-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="f2dcf-124">Donnez un nom à votre application.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-124">Name your application.</span></span>
3. <span data-ttu-id="f2dcf-125">Choisissez le type de votre premier service et nommez-le.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-125">Choose the type of your first service and name it.</span></span> <span data-ttu-id="f2dcf-126">Pour les besoins de ce didacticiel, nous choisissons un service Reliable Actors.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Générateur Yeoman Service Fabric pour C#][sf-yeoman]

> [!NOTE]
> <span data-ttu-id="f2dcf-128">Pour plus d’informations sur les options, voir [Vue d’ensemble des modèles de programmation Service Fabric](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="f2dcf-128">For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
>
>

## <a name="build-the-application"></a><span data-ttu-id="f2dcf-129">Création de l'application</span><span class="sxs-lookup"><span data-stu-id="f2dcf-129">Build the application</span></span>
<span data-ttu-id="f2dcf-130">Les modèles Yeoman Service Fabric incluent un script de build que vous pouvez utiliser pour générer l’application à partir du terminal (après avoir accédé au dossier l’application).</span><span class="sxs-lookup"><span data-stu-id="f2dcf-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="f2dcf-131">Déployer l’application</span><span class="sxs-lookup"><span data-stu-id="f2dcf-131">Deploy the application</span></span>

<span data-ttu-id="f2dcf-132">Une fois que l’application est générée, vous pouvez la déployer sur le cluster local.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-132">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="f2dcf-133">Connectez-vous au cluster Service Fabric local.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-133">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="f2dcf-134">Exécutez le script d’installation fourni dans le modèle pour copier le package d’application dans le magasin d’images du cluster, inscrire le type d’application et créer une instance de l’application.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="f2dcf-135">L’application générée se déploie de la même manière qu’une autre application Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-135">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="f2dcf-136">Consultez la documentation sur [la gestion d’une application Service Fabric avec l’interface de ligne de commande Service Fabric](service-fabric-application-lifecycle-sfctl.md) pour obtenir des instructions détaillées.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="f2dcf-137">Vous pourrez retrouver les paramètres de ces commandes dans les manifestes générés au sein du package d’application.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-137">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="f2dcf-138">Une fois l’application déployée, ouvrez un navigateur et accédez à [Service Fabric Explorer ](service-fabric-visualizing-your-cluster.md), à l’adresse [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="f2dcf-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="f2dcf-139">Ensuite, développez le nœud **Applications** et notez qu’il existe désormais une entrée pour votre type d’application et une autre pour la première instance de ce type.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="f2dcf-140">Démarrer le client de test et effectuer un basculement</span><span class="sxs-lookup"><span data-stu-id="f2dcf-140">Start the test client and perform a failover</span></span>
<span data-ttu-id="f2dcf-141">Les projets d’acteur n’effectuent aucune opération automatiquement.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-141">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="f2dcf-142">Ils ont besoin d’un autre service ou client pour leur envoyer des messages.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-142">They require another service or client to send them messages.</span></span> <span data-ttu-id="f2dcf-143">Le modèle d’acteur inclut un script de test simple que vous pouvez utiliser pour interagir avec le service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-143">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="f2dcf-144">Exécutez le script à l’aide de l’utilitaire watch pour afficher la sortie du service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-144">Run the script using the watch utility to see the output of the actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="f2dcf-145">Dans Service Fabric Explorer, recherchez le nœud qui héberge le réplica principal pour le service d’acteur.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-145">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="f2dcf-146">Dans la capture d’écran ci-dessous, il s’agit du nœud 3.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-146">In the screenshot below, it is node 3.</span></span>

    ![Recherche du réplica principal dans Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="f2dcf-148">Cliquez sur le nœud trouvé à l’étape précédente, puis sélectionnez **Désactiver (redémarrer)** à partir du menu Actions.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-148">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="f2dcf-149">Cette action redémarre un nœud de votre cluster local et force un basculement sur un réplica secondaire s’exécutant sur un autre nœud.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-149">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="f2dcf-150">Dans le même temps, prêtez attention à la sortie du client de test et notez que le compteur continue à être incrémenté malgré le basculement.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-150">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="f2dcf-151">Ajout d’autres services à une application existante</span><span class="sxs-lookup"><span data-stu-id="f2dcf-151">Adding more services to an existing application</span></span>

<span data-ttu-id="f2dcf-152">Pour ajouter un autre service à une application déjà créée à l’aide de `yo`, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="f2dcf-152">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="f2dcf-153">Accédez au répertoire à la racine de l’application existante.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-153">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="f2dcf-154">Par exemple, `cd ~/YeomanSamples/MyApplication`, si `MyApplication` est l’application créée par Yeoman.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-154">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="f2dcf-155">Exécutez `yo azuresfcsharp:AddService`.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-155">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="migrating-from-projectjson-to-csproj"></a><span data-ttu-id="f2dcf-156">Migration de project.json vers .csproj</span><span class="sxs-lookup"><span data-stu-id="f2dcf-156">Migrating from project.json to .csproj</span></span>
1. <span data-ttu-id="f2dcf-157">L’exécution de « dotnet migrate » dans le répertoire racine du projet entraîne la migration de tous les éléments project.json vers le format csproj.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-157">Running 'dotnet migrate' in project root directory will migrate all the project.json to csproj format.</span></span>
2. <span data-ttu-id="f2dcf-158">Mettez également à jour les références de projet pour qu’elles pointent les fichiers csproj dans les fichiers projet.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-158">Update the project references accordingly to csproj files in project files.</span></span>
3. <span data-ttu-id="f2dcf-159">Mettez à jour les noms de fichiers projet en fonction des fichiers csproj dans build.sh.</span><span class="sxs-lookup"><span data-stu-id="f2dcf-159">Update the project file names to csproj files in build.sh.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2dcf-160">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f2dcf-160">Next steps</span></span>

* [<span data-ttu-id="f2dcf-161">Présentation des Acteurs fiables Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2dcf-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="f2dcf-162">Interaction avec les clusters Service Fabric à l’aide de l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2dcf-162">Interacting with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="f2dcf-163">En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="f2dcf-163">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="f2dcf-164">Bien démarrer avec l’interface de ligne de commande Service Fabric</span><span class="sxs-lookup"><span data-stu-id="f2dcf-164">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
