---
title: "aaaQuickly déployer un cluster de Azure Service Fabric application tooan existant"
description: Utilisez un toohost de cluster Azure Service Fabric une application Node.js existante avec Visual Studio.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="dcd51-103">Héberger une application Node.js sur Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="dcd51-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="dcd51-104">Ce démarrage rapide vous permet de déployer un cluster de l’infrastructure de Service de tooa (Node.js dans cet exemple) d’application existant en cours d’exécution sur Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd51-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcd51-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dcd51-105">Prerequisites</span></span>

<span data-ttu-id="dcd51-106">Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="dcd51-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="dcd51-107">Qui inclut l’installation de type hello Service Fabric SDK et Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="dcd51-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="dcd51-108">Vous devez également toohave une application Node.js existante pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="dcd51-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="dcd51-109">Ce démarrage rapide utilise un site web Node.js simple qui peut être téléchargé [ici][download-sample].</span><span class="sxs-lookup"><span data-stu-id="dcd51-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="dcd51-110">Extraire ce fichier tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` dossier après avoir créé un projet de hello dans l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="dcd51-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="dcd51-111">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit][create-account].</span><span class="sxs-lookup"><span data-stu-id="dcd51-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="dcd51-112">Créer le service de hello</span><span class="sxs-lookup"><span data-stu-id="dcd51-112">Create hello service</span></span>

<span data-ttu-id="dcd51-113">Lancez Visual Studio en tant qu’**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="dcd51-114">Créer un projet avec `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="dcd51-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="dcd51-115">Bonjour **nouveau projet** boîte de dialogue, choisissez **Cloud > Application Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="dcd51-116">Nommez l’application hello **MyGuestApp** et appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="dcd51-117">Node.js peuvent facilement s’interrompre hello 260 caractères pour les tracés qui dispose de windows.</span><span class="sxs-lookup"><span data-stu-id="dcd51-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="dcd51-118">Utilisez un chemin d’accès court pour le projet hello lui-même comme **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Boîte de dialogue Nouveau projet dans Visual Studio][new-project]

<span data-ttu-id="dcd51-120">Vous pouvez créer n’importe quel type de service Service Fabric à partir de la boîte de dialogue suivante hello.</span><span class="sxs-lookup"><span data-stu-id="dcd51-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="dcd51-121">Pour ce démarrage rapide, choisissez **Exécutable invité**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="dcd51-122">Nom de votre service de hello **MyGuestService** et définir les options de hello sur toohello de droite hello des valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="dcd51-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="dcd51-123">Paramètre</span><span class="sxs-lookup"><span data-stu-id="dcd51-123">Setting</span></span>                   | <span data-ttu-id="dcd51-124">Valeur</span><span class="sxs-lookup"><span data-stu-id="dcd51-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="dcd51-125">Dossier du package de code</span><span class="sxs-lookup"><span data-stu-id="dcd51-125">Code Package Folder</span></span>       | <span data-ttu-id="dcd51-126">_&lt;dossier Hello avec votre application Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="dcd51-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="dcd51-127">Comportement du package de code</span><span class="sxs-lookup"><span data-stu-id="dcd51-127">Code Package Behavior</span></span>     | <span data-ttu-id="dcd51-128">Copiez le dossier contenu tooproject</span><span class="sxs-lookup"><span data-stu-id="dcd51-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="dcd51-129">Programme</span><span class="sxs-lookup"><span data-stu-id="dcd51-129">Program</span></span>                   | <span data-ttu-id="dcd51-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="dcd51-130">node.exe</span></span> |
| <span data-ttu-id="dcd51-131">Arguments</span><span class="sxs-lookup"><span data-stu-id="dcd51-131">Arguments</span></span>                 | <span data-ttu-id="dcd51-132">server.js</span><span class="sxs-lookup"><span data-stu-id="dcd51-132">server.js</span></span> |
| <span data-ttu-id="dcd51-133">Dossier de travail</span><span class="sxs-lookup"><span data-stu-id="dcd51-133">Working Folder</span></span>            | <span data-ttu-id="dcd51-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="dcd51-134">CodePackage</span></span> |

<span data-ttu-id="dcd51-135">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-135">Press **OK**.</span></span>

![Boîte de dialogue Nouveau service dans Visual Studio.][new-service]

<span data-ttu-id="dcd51-137">Visual Studio crée le projet d’application hello et de projet de service d’acteur hello et les affiche dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="dcd51-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="dcd51-138">projet d’application Hello (**MyGuestApp**) ne contient pas de code directement.</span><span class="sxs-lookup"><span data-stu-id="dcd51-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="dcd51-139">Au lieu de cela, il fait référence à un ensemble de projets de service.</span><span class="sxs-lookup"><span data-stu-id="dcd51-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="dcd51-140">En outre, il contient trois autres types de contenu :</span><span class="sxs-lookup"><span data-stu-id="dcd51-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="dcd51-141">**Profils de publication**</span><span class="sxs-lookup"><span data-stu-id="dcd51-141">**Publish profiles**</span></span>  
<span data-ttu-id="dcd51-142">Préférences d’outils pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="dcd51-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="dcd51-143">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="dcd51-143">**Scripts**</span></span>  
<span data-ttu-id="dcd51-144">Script PowerShell de déploiement/mise à niveau de votre application.</span><span class="sxs-lookup"><span data-stu-id="dcd51-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="dcd51-145">**Définition d’application**</span><span class="sxs-lookup"><span data-stu-id="dcd51-145">**Application definition**</span></span>  
<span data-ttu-id="dcd51-146">Inclut le manifeste de l’application hello sous *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="dcd51-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="dcd51-147">Fichiers de paramètres d’application associée sont sous *ApplicationParameters*, qui définissent l’application hello et vous tooconfigure spécifiquement pour un environnement donné.</span><span class="sxs-lookup"><span data-stu-id="dcd51-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="dcd51-148">Pour une vue d’ensemble du contenu hello hello du projet de service, consultez [prise en main des Services fiables](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="dcd51-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="dcd51-149">Configurer la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="dcd51-149">Set up networking</span></span>

<span data-ttu-id="dcd51-150">exemple Hello application Node.js nous mettons déploiement utilise le port **80** et nous devons tootell Service Fabric dont nous avons besoin que le port exposé.</span><span class="sxs-lookup"><span data-stu-id="dcd51-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="dcd51-151">Ouvrez hello **ServiceManifest.xml** fichier de projet de hello.</span><span class="sxs-lookup"><span data-stu-id="dcd51-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="dcd51-152">Bas hello du manifeste de hello, il existe un `<Resources> \ <Endpoints>` avec une entrée déjà définie.</span><span class="sxs-lookup"><span data-stu-id="dcd51-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="dcd51-153">Modifier cette entrée tooadd `Port`, `Protocol`, et `Type`.</span><span class="sxs-lookup"><span data-stu-id="dcd51-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="dcd51-154">Déployer tooAzure</span><span class="sxs-lookup"><span data-stu-id="dcd51-154">Deploy tooAzure</span></span>

<span data-ttu-id="dcd51-155">Si vous appuyez sur **F5** et exécutez hello projet, il est déployé toohello les cluster local.</span><span class="sxs-lookup"><span data-stu-id="dcd51-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="dcd51-156">Toutefois, nous allons déployer tooAzure à la place.</span><span class="sxs-lookup"><span data-stu-id="dcd51-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="dcd51-157">Avec le bouton droit sur le projet de hello et choisissez **publier...**  qui ouvre un tooAzure toopublish de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dcd51-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Boîte de dialogue tooazure pour un service service fabric publier][publish]

<span data-ttu-id="dcd51-159">Sélectionnez hello **PublishProfiles\Cloud.xml** cibler profile.</span><span class="sxs-lookup"><span data-stu-id="dcd51-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="dcd51-160">Si vous n’avez pas précédemment, choisissez un toodeploy compte Azure à.</span><span class="sxs-lookup"><span data-stu-id="dcd51-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="dcd51-161">Si vous n’en avez pas, [obtenez-en un][create-account].</span><span class="sxs-lookup"><span data-stu-id="dcd51-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="dcd51-162">Sous **point de terminaison de connexion**, sélectionnez hello toodeploy du cluster Service Fabric pour.</span><span class="sxs-lookup"><span data-stu-id="dcd51-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="dcd51-163">Si vous n’avez pas une option, sélectionnez  **&lt;créer un nouveau Cluster... &gt;**  qui ouvre toohello de fenêtre de navigateur web portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd51-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="dcd51-164">Pour plus d’informations, consultez [créer un cluster dans le portail de hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="dcd51-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="dcd51-165">Lorsque vous créez le cluster Service Fabric de hello, assurez-vous que tooset hello **les points de terminaison personnalisé** aussi un paramètre**80**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Configuration de type nœud Service Fabric avec le point de terminaison personnalisé][custom-endpoint]

<span data-ttu-id="dcd51-167">Création d’un nouveau cluster Service Fabric prend quelques toocomplete de temps.</span><span class="sxs-lookup"><span data-stu-id="dcd51-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="dcd51-168">Une fois qu’il a été créé, accédez toohello arrière boîte de dialogue Publier et sélectionnez  **&lt;Actualiser&gt;**.</span><span class="sxs-lookup"><span data-stu-id="dcd51-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="dcd51-169">nouveau cluster de Hello est répertorié dans la zone de liste déroulante hello. Sélectionnez-la.</span><span class="sxs-lookup"><span data-stu-id="dcd51-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="dcd51-170">Appuyez sur **publier** et attendez hello déploiement toofinish.</span><span class="sxs-lookup"><span data-stu-id="dcd51-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="dcd51-171">Cela peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="dcd51-171">This may take a few minutes.</span></span> <span data-ttu-id="dcd51-172">Après avoir terminé, il peut prendre quelques minutes pour toobe d’application hello entièrement disponible.</span><span class="sxs-lookup"><span data-stu-id="dcd51-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="dcd51-173">Site Web de test hello</span><span class="sxs-lookup"><span data-stu-id="dcd51-173">Test hello website</span></span>

<span data-ttu-id="dcd51-174">Une fois que votre service a été publié, testez-le dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="dcd51-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="dcd51-175">Tout d’abord, ouvrez hello portail Azure et trouver votre service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dcd51-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="dcd51-176">Vérifiez le panneau de vue d’ensemble de hello d’adresse de service hello.</span><span class="sxs-lookup"><span data-stu-id="dcd51-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="dcd51-177">Nom de domaine hello utilisation à partir de hello _point de terminaison de connexion Client_ propriété.</span><span class="sxs-lookup"><span data-stu-id="dcd51-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="dcd51-178">Par exemple, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="dcd51-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Panneau de vue d’ensemble de l’infrastructure de service sur hello portail Azure][overview]

<span data-ttu-id="dcd51-180">Accédez adresse toothis où vous verrez hello `HELLO WORLD` réponse.</span><span class="sxs-lookup"><span data-stu-id="dcd51-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="dcd51-181">Supprimer le cluster de hello</span><span class="sxs-lookup"><span data-stu-id="dcd51-181">Delete hello cluster</span></span>

<span data-ttu-id="dcd51-182">N’oubliez pas de toodelete toutes les ressources hello que vous avez créé pour ce démarrage rapide, en tant que vous êtes facturés pour ces ressources.</span><span class="sxs-lookup"><span data-stu-id="dcd51-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dcd51-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dcd51-183">Next steps</span></span>
<span data-ttu-id="dcd51-184">Apprenez-en davantage sur les [exécutables invités](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="dcd51-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F