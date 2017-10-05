---
title: "Déployer rapidement une application existante dans un cluster Microsoft Azure Service Fabric"
description: "Utilisez un cluster Microsoft Azure Service Fabric pour héberger une application Node.js existante avec Visual Studio."
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
ms.openlocfilehash: 3601b73872bbea4b4e5324382eb97b7384ca6e13
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="86a85-103">Héberger une application Node.js sur Microsoft Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="86a85-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="86a85-104">Ce démarrage rapide vous permet de déployer une application existante (Node.js dans cet exemple) dans un cluster Service Fabric s’exécutant sur Azure.</span><span class="sxs-lookup"><span data-stu-id="86a85-104">This quickstart helps you deploy an existing application (Node.js in this example) to a Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86a85-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="86a85-105">Prerequisites</span></span>

<span data-ttu-id="86a85-106">Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="86a85-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="86a85-107">Cela inclut l’installation du kit de développement logiciel (SDK) de Service Fabric et de Visual Studio 2017 ou 2015.</span><span class="sxs-lookup"><span data-stu-id="86a85-107">Which includes installing the Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="86a85-108">Vous devez également disposer d’une application Node.js existante pour le déploiement.</span><span class="sxs-lookup"><span data-stu-id="86a85-108">You also need to have an existing Node.js application for deployment.</span></span> <span data-ttu-id="86a85-109">Ce démarrage rapide utilise un site web Node.js simple qui peut être téléchargé [ici][download-sample].</span><span class="sxs-lookup"><span data-stu-id="86a85-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="86a85-110">Extrayez ce fichier vers votre dossier `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` après avoir créé le projet dans l’étape suivante.</span><span class="sxs-lookup"><span data-stu-id="86a85-110">Extract this file to your `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create the project in the next step.</span></span>

<span data-ttu-id="86a85-111">Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit][create-account].</span><span class="sxs-lookup"><span data-stu-id="86a85-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-the-service"></a><span data-ttu-id="86a85-112">Créer le service</span><span class="sxs-lookup"><span data-stu-id="86a85-112">Create the service</span></span>

<span data-ttu-id="86a85-113">Lancez Visual Studio en tant qu’**administrateur**.</span><span class="sxs-lookup"><span data-stu-id="86a85-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="86a85-114">Créer un projet avec `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="86a85-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="86a85-115">Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Cloud > Application Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="86a85-115">In the **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="86a85-116">Nommez l’application **MyGuestApp**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="86a85-116">Name the application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="86a85-117">Node.js peut facilement dépasser la limite de 260 caractères pour les chemins d’accès de Windows.</span><span class="sxs-lookup"><span data-stu-id="86a85-117">Node.js can easily break the 260 character limit for paths that windows has.</span></span> <span data-ttu-id="86a85-118">Utilisez un chemin d’accès court pour le projet en lui-même, par exemple **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="86a85-118">Use a short path for the project itself such as **c:\code\svc1**.</span></span>
   
![Boîte de dialogue Nouveau projet dans Visual Studio][new-project]

<span data-ttu-id="86a85-120">Vous pouvez créer n’importe quel type de service Service Fabric à partir de la boîte de dialogue suivante.</span><span class="sxs-lookup"><span data-stu-id="86a85-120">You can create any type of Service Fabric service from the next dialog.</span></span> <span data-ttu-id="86a85-121">Pour ce démarrage rapide, choisissez **Exécutable invité**.</span><span class="sxs-lookup"><span data-stu-id="86a85-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="86a85-122">Nommez le service **MyGuestService** et définissez les options à droite sur les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="86a85-122">Name the service **MyGuestService** and set the options on the right to the following values:</span></span>

| <span data-ttu-id="86a85-123">Paramètre</span><span class="sxs-lookup"><span data-stu-id="86a85-123">Setting</span></span>                   | <span data-ttu-id="86a85-124">Valeur</span><span class="sxs-lookup"><span data-stu-id="86a85-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="86a85-125">Dossier du package de code</span><span class="sxs-lookup"><span data-stu-id="86a85-125">Code Package Folder</span></span>       | <span data-ttu-id="86a85-126">_&lt;le dossier avec votre application Node.js&gt;_</span><span class="sxs-lookup"><span data-stu-id="86a85-126">_&lt;the folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="86a85-127">Comportement du package de code</span><span class="sxs-lookup"><span data-stu-id="86a85-127">Code Package Behavior</span></span>     | <span data-ttu-id="86a85-128">Copiez le contenu du dossier vers le projet</span><span class="sxs-lookup"><span data-stu-id="86a85-128">Copy folder contents to project</span></span> |
| <span data-ttu-id="86a85-129">Programme</span><span class="sxs-lookup"><span data-stu-id="86a85-129">Program</span></span>                   | <span data-ttu-id="86a85-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="86a85-130">node.exe</span></span> |
| <span data-ttu-id="86a85-131">Arguments</span><span class="sxs-lookup"><span data-stu-id="86a85-131">Arguments</span></span>                 | <span data-ttu-id="86a85-132">server.js</span><span class="sxs-lookup"><span data-stu-id="86a85-132">server.js</span></span> |
| <span data-ttu-id="86a85-133">Dossier de travail</span><span class="sxs-lookup"><span data-stu-id="86a85-133">Working Folder</span></span>            | <span data-ttu-id="86a85-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="86a85-134">CodePackage</span></span> |

<span data-ttu-id="86a85-135">Appuyez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="86a85-135">Press **OK**.</span></span>

![Boîte de dialogue Nouveau service dans Visual Studio.][new-service]

<span data-ttu-id="86a85-137">Visual Studio crée le projet d’application et le projet de service d’acteur et les affiche dans l’Explorateur de solutions.</span><span class="sxs-lookup"><span data-stu-id="86a85-137">Visual Studio creates the application project and the actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="86a85-138">Le projet d’application (**MyGuestApp**) ne contient pas de code directement.</span><span class="sxs-lookup"><span data-stu-id="86a85-138">The application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="86a85-139">Au lieu de cela, il fait référence à un ensemble de projets de service.</span><span class="sxs-lookup"><span data-stu-id="86a85-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="86a85-140">En outre, il contient trois autres types de contenu :</span><span class="sxs-lookup"><span data-stu-id="86a85-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="86a85-141">**Profils de publication**</span><span class="sxs-lookup"><span data-stu-id="86a85-141">**Publish profiles**</span></span>  
<span data-ttu-id="86a85-142">Préférences d’outils pour différents environnements.</span><span class="sxs-lookup"><span data-stu-id="86a85-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="86a85-143">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="86a85-143">**Scripts**</span></span>  
<span data-ttu-id="86a85-144">Script PowerShell de déploiement/mise à niveau de votre application.</span><span class="sxs-lookup"><span data-stu-id="86a85-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="86a85-145">**Définition d’application**</span><span class="sxs-lookup"><span data-stu-id="86a85-145">**Application definition**</span></span>  
<span data-ttu-id="86a85-146">Inclut le manifeste d’application dans le dossier *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="86a85-146">Includes the application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="86a85-147">Les fichiers de paramètres d’application associés, qui définissent l’application et vous permettent de la configurer spécifiquement pour un environnement donné, se trouvent dans le dossier *ApplicationParameters*.</span><span class="sxs-lookup"><span data-stu-id="86a85-147">Associated application parameter files are under *ApplicationParameters*, which define the application and allow you to configure it specifically for a given environment.</span></span>
    
<span data-ttu-id="86a85-148">Pour avoir une vue d’ensemble du contenu du projet de service, consultez l’article [Prise en main de Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="86a85-148">For an overview of the contents of the service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="86a85-149">Configurer la mise en réseau</span><span class="sxs-lookup"><span data-stu-id="86a85-149">Set up networking</span></span>

<span data-ttu-id="86a85-150">L’exemple d’application Node.js que nous déployons utilise le port **80**, et nous devons indiquer à Service Fabric que nous avons besoin que ce port soit exposé.</span><span class="sxs-lookup"><span data-stu-id="86a85-150">The example Node.js app we're deploying uses port **80** and we need to tell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="86a85-151">Ouvrez le fichier **ServiceManifest.xml** dans le projet.</span><span class="sxs-lookup"><span data-stu-id="86a85-151">Open the **ServiceManifest.xml** file in the project.</span></span> <span data-ttu-id="86a85-152">Au bas du manifeste, il existe un `<Resources> \ <Endpoints>` avec une entrée déjà définie.</span><span class="sxs-lookup"><span data-stu-id="86a85-152">At the bottom of the manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="86a85-153">Modifiez cette entrée pour ajouter `Port`, `Protocol` et `Type`.</span><span class="sxs-lookup"><span data-stu-id="86a85-153">Modify that entry to add `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-to-azure"></a><span data-ttu-id="86a85-154">Déployer dans Azure</span><span class="sxs-lookup"><span data-stu-id="86a85-154">Deploy to Azure</span></span>

<span data-ttu-id="86a85-155">Si vous appuyez sur **F5** et exécutez le projet, il est déployé dans le cluster local.</span><span class="sxs-lookup"><span data-stu-id="86a85-155">If you press **F5** and run the project, it is deployed to the local cluster.</span></span> <span data-ttu-id="86a85-156">Toutefois, nous allons le déployer vers Azure.</span><span class="sxs-lookup"><span data-stu-id="86a85-156">However, let's deploy to Azure instead.</span></span>

<span data-ttu-id="86a85-157">Cliquez avec le bouton droit sur le projet et choisissez **Publier...**, qui ouvre une boîte de dialogue de publication sur Azure.</span><span class="sxs-lookup"><span data-stu-id="86a85-157">Right-click on the project and choose **Publish...** which opens a dialog to publish to Azure.</span></span>

![Boîte de dialogue de publication sur Azure pour un service Service Fabric][publish]

<span data-ttu-id="86a85-159">Sélectionnez le profil cible **PublishProfiles\Cloud.xml**.</span><span class="sxs-lookup"><span data-stu-id="86a85-159">Select the **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="86a85-160">Si vous ne l’avez pas fait précédemment, choisissez un compte Azure vers lequel effectuer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="86a85-160">If you haven't previously, choose an Azure account to deploy to.</span></span> <span data-ttu-id="86a85-161">Si vous n’en avez pas, [obtenez-en un][create-account].</span><span class="sxs-lookup"><span data-stu-id="86a85-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="86a85-162">Sous **Point de terminaison de connexion**, sélectionnez le cluster Service Fabric vers lequel effectuer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="86a85-162">Under **Connection Endpoint**, select the Service Fabric cluster to deploy to.</span></span> <span data-ttu-id="86a85-163">Si vous n’en avez pas, sélectionnez **&lt;Créer un cluster...&gt;** qui ouvre la fenêtre de navigateur web sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="86a85-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window to the Azure portal.</span></span> <span data-ttu-id="86a85-164">Pour plus d’informations, consultez [Création d’un cluster dans le portail Azure](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="86a85-164">For more information, see [create a cluster in the portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="86a85-165">Lorsque vous créez le cluster Service Fabric, veillez à définir le paramètre **Points de terminaison personnalisés** sur **80**.</span><span class="sxs-lookup"><span data-stu-id="86a85-165">When you create the Service Fabric cluster, make sure to set the **Custom endpoints** setting to **80**.</span></span>

![Configuration de type nœud Service Fabric avec le point de terminaison personnalisé][custom-endpoint]

<span data-ttu-id="86a85-167">La création d’un cluster Service Fabric prend un certain temps.</span><span class="sxs-lookup"><span data-stu-id="86a85-167">Creating a new Service Fabric cluster takes some time to complete.</span></span> <span data-ttu-id="86a85-168">Une fois qu’il a été créé, revenez à la boîte de dialogue de publication et sélectionnez **&lt;Actualiser&gt;**.</span><span class="sxs-lookup"><span data-stu-id="86a85-168">Once it has been created, go back to the publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="86a85-169">Le nouveau cluster est répertorié dans la zone de liste déroulante ; sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="86a85-169">The new cluster is listed in the drop-down box; select it.</span></span>

<span data-ttu-id="86a85-170">Appuyez sur **Publier** et attendez que le déploiement se termine.</span><span class="sxs-lookup"><span data-stu-id="86a85-170">Press **Publish** and wait for the deployment to finish.</span></span>

<span data-ttu-id="86a85-171">Cela peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="86a85-171">This may take a few minutes.</span></span> <span data-ttu-id="86a85-172">Une fois terminé, quelques minutes peuvent être nécessaires pour que l’application soit totalement disponible.</span><span class="sxs-lookup"><span data-stu-id="86a85-172">After it completes, it may take a few more minutes for the application to be fully available.</span></span>

## <a name="test-the-website"></a><span data-ttu-id="86a85-173">Tester le site web</span><span class="sxs-lookup"><span data-stu-id="86a85-173">Test the website</span></span>

<span data-ttu-id="86a85-174">Une fois que votre service a été publié, testez-le dans un navigateur web.</span><span class="sxs-lookup"><span data-stu-id="86a85-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="86a85-175">Tout d’abord, ouvrez le portail Azure et recherchez votre service Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="86a85-175">First, open the Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="86a85-176">Consultez le panneau Vue d’ensemble de l’adresse du service.</span><span class="sxs-lookup"><span data-stu-id="86a85-176">Check the overview blade of the service address.</span></span> <span data-ttu-id="86a85-177">Utilisez le nom de domaine de la propriété _Point de terminaison de connexion du client_.</span><span class="sxs-lookup"><span data-stu-id="86a85-177">Use the domain name from the _Client connection endpoint_ property.</span></span> <span data-ttu-id="86a85-178">Par exemple, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="86a85-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Panneau Vue d’ensemble de Service Fabric sur le portail Azure][overview]

<span data-ttu-id="86a85-180">Accédez à cette adresse où vous verrez la réponse `HELLO WORLD`.</span><span class="sxs-lookup"><span data-stu-id="86a85-180">Navigate to this address where you will see the `HELLO WORLD` response.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="86a85-181">Suppression du cluster</span><span class="sxs-lookup"><span data-stu-id="86a85-181">Delete the cluster</span></span>

<span data-ttu-id="86a85-182">N’oubliez pas de supprimer toutes les ressources que vous avez créées pour ce démarrage rapide, car celles-ci vous sont facturées.</span><span class="sxs-lookup"><span data-stu-id="86a85-182">Do not forget to delete all of the resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a85-183">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="86a85-183">Next steps</span></span>
<span data-ttu-id="86a85-184">Apprenez-en davantage sur les [exécutables invités](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="86a85-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F