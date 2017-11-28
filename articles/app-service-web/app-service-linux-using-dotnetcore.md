---
title: "Utiliser .NET Core dans une application web sur Linux | Microsoft Docs"
description: Utilisez .NET Core dans une application web sur Linux.
keywords: azure app service, application web, dotnet, core, linux, oss
services: app-service
documentationCenter: 
authors: michimune, rachelappel
manager: erikre
editor: 
ms.assetid: c02959e6-7220-496a-a417-9b2147638e2e
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: aelnably;wesmc;mikono;rachelap
ms.openlocfilehash: 9226dfb90e52ac2cae2cfc4af7c0705a93f56b44
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="8b2f1-104">Utiliser .NET Core dans une application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="8b2f1-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="8b2f1-105">Une [application web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) sur Linux fournit un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques à l’aide du système d’exploitation Linux.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using the Linux operating system.</span></span> <span data-ttu-id="8b2f1-106">Ce didacticiel contient des instructions détaillées montrant comment créer une application [.NET Core](https://docs.microsoft.com/aspnet/core/) sur une application web Azure sur Linux.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-106">This tutorial contains step-by-step instructions showing how to create a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Application web sous Linux][10]

<span data-ttu-id="8b2f1-108">Vous pouvez suivre les étapes ci-dessous en utilisant un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b2f1-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="8b2f1-109">Prerequisites</span></span> ##

<span data-ttu-id="8b2f1-110">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-110">To complete this tutorial:</span></span> 

* <span data-ttu-id="8b2f1-111">Installez le [kit de développement logiciel (SDK) .NET Core](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="8b2f1-111">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="8b2f1-112">Installez [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="8b2f1-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="8b2f1-113">Créer une application .NET Core locale</span><span class="sxs-lookup"><span data-stu-id="8b2f1-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="8b2f1-114">Démarrez une nouvelle session de terminal.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-114">Start a new terminal session.</span></span> <span data-ttu-id="8b2f1-115">Créez un répertoire nommé `hellodotnetcore` et remplacez le répertoire actuel par ce dernier.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-115">Create a directory named `hellodotnetcore`, and change the current directory to it.</span></span> <span data-ttu-id="8b2f1-116">Tapez ensuite la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-116">Then type the following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="8b2f1-117">Cette commande crée trois fichiers (*hellodotnetcore.csproj*, *Program.cs* et *Startup.cs*) et un dossier vide (*wwwroot/*) sous le répertoire actuel.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under the current directory.</span></span> <span data-ttu-id="8b2f1-118">Le contenu du fichier `.csproj` doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-118">The content of `.csproj` file should look like the following:</span></span> 

```xml
  <!-- Empty lines are omitted. -->

  <Project Sdk="Microsoft.NET.Sdk.Web">
        <PropertyGroup>
        <TargetFramework>netcoreapp1.1</TargetFramework>
        </PropertyGroup>
        <ItemGroup>
        <Folder Include="wwwroot\" />
        </ItemGroup>
        <ItemGroup>
        <PackageReference Include="Microsoft.AspNetCore" Version="1.1.2" />
        </ItemGroup>
  </Project>
```

<span data-ttu-id="8b2f1-119">Étant donné que cette application est une application web, une référence à un package ASP.NET Core a été automatiquement ajoutée au fichier *hellodotnetcore.csproj*.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-119">Since this app is a web application, a reference to an ASP.NET Core package was automatically added to the *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="8b2f1-120">Le numéro de version du package est défini en fonction de l’infrastructure choisie.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-120">The version number of the package is set according to the chosen framework.</span></span> <span data-ttu-id="8b2f1-121">Cet exemple fait référence à ASP.NET Core version 1.1.2, car .NET Core 1.1 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-the-application-locally"></a><span data-ttu-id="8b2f1-122">Générer et tester l’application localement</span><span class="sxs-lookup"><span data-stu-id="8b2f1-122">Build and test the application locally</span></span> ##

<span data-ttu-id="8b2f1-123">Vous pouvez générer et exécuter votre application .NET Core avec la commande `dotnet restore` suivie de la commande `dotnet run`, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-123">You can build and run your .NET Core app with the `dotnet restore` command followed by the `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="8b2f1-124">Lorsque l’application démarre, elle affiche un message indiquant que l’application écoute les demandes entrantes au niveau d’un port.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-124">When the application starts, it displays a message indicating the app is listening to incoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

<span data-ttu-id="8b2f1-125">Testez-la en accédant à `http://localhost:5000/` avec votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-125">Test it by browsing to `http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="8b2f1-126">Si tout fonctionne correctement, vous voyez « Hello World! »</span><span class="sxs-lookup"><span data-stu-id="8b2f1-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="8b2f1-127">comme texte de résultat.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-127">as the result text.</span></span>

![Tester avec un navigateur][7]

## <a name="create-a-net-core-app-in-the-azure-portal"></a><span data-ttu-id="8b2f1-129">Créer une application .NET Core dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="8b2f1-129">Create a .NET Core app in the Azure Portal</span></span> ##

<span data-ttu-id="8b2f1-130">Vous devez d’abord créer une application web vide.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-130">First you need to create an empty web app.</span></span> <span data-ttu-id="8b2f1-131">Connectez-vous au [portail Azure](https://portal.azure.com/) et créez une [application web sur Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="8b2f1-131">Log in to the [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Création d’une application web][1]

<span data-ttu-id="8b2f1-133">Lorsque la page **Créer** s’ouvre, fournissez des détails sur votre application web :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-133">When the **Create** page opens, provide details about your web app:</span></span>

![Choix d’une pile d’exécution .NET Core][2]

<span data-ttu-id="8b2f1-135">Utilisez le tableau suivant comme guide pour remplir la page **Créer**, puis sélectionnez **OK** et **Créer** pour créer l’application.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-135">Use the following table as a guide to fill out the **Create** page, then select **OK** and **Create** to create the app.</span></span>

| <span data-ttu-id="8b2f1-136">Paramètre</span><span class="sxs-lookup"><span data-stu-id="8b2f1-136">Setting</span></span>      | <span data-ttu-id="8b2f1-137">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="8b2f1-137">Suggested value</span></span>  | <span data-ttu-id="8b2f1-138">Description</span><span class="sxs-lookup"><span data-stu-id="8b2f1-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="8b2f1-139">Nom de l’application</span><span class="sxs-lookup"><span data-stu-id="8b2f1-139">App name</span></span> | <span data-ttu-id="8b2f1-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="8b2f1-140">hellodotnetcore</span></span>  | <span data-ttu-id="8b2f1-141">Nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-141">The name of your app.</span></span> <span data-ttu-id="8b2f1-142">Ce nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-142">This name must be unique.</span></span> |
| <span data-ttu-id="8b2f1-143">Abonnement</span><span class="sxs-lookup"><span data-stu-id="8b2f1-143">Subscription</span></span> | <span data-ttu-id="8b2f1-144">Choisir un abonnement existant</span><span class="sxs-lookup"><span data-stu-id="8b2f1-144">Choose an existing subscription</span></span> | <span data-ttu-id="8b2f1-145">Abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-145">The Azure subscription.</span></span> |
| <span data-ttu-id="8b2f1-146">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="8b2f1-146">Resource Group</span></span> | <span data-ttu-id="8b2f1-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8b2f1-147">myResourceGroup</span></span> |  <span data-ttu-id="8b2f1-148">Groupe de ressources Azure qui hébergera l’application web.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-148">The Azure resource group to contain the web app.</span></span> |
| <span data-ttu-id="8b2f1-149">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="8b2f1-149">App Service Plan</span></span> | <span data-ttu-id="8b2f1-150">Nom de plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="8b2f1-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="8b2f1-151">Plan App Service.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-151">The App Service plan.</span></span>  |
| <span data-ttu-id="8b2f1-152">Configurer le conteneur</span><span class="sxs-lookup"><span data-stu-id="8b2f1-152">Configure Container</span></span> | <span data-ttu-id="8b2f1-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="8b2f1-153">.NET Core 1.1</span></span> | <span data-ttu-id="8b2f1-154">Type de conteneur pour cette application web : intégré, Docker ou registre privé.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-154">The type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="8b2f1-155">Source d’image</span><span class="sxs-lookup"><span data-stu-id="8b2f1-155">Image source</span></span>  | <span data-ttu-id="8b2f1-156">Intégration</span><span class="sxs-lookup"><span data-stu-id="8b2f1-156">Built-in</span></span>  |  <span data-ttu-id="8b2f1-157">Source de l’image.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-157">The source of the image.</span></span> |
| <span data-ttu-id="8b2f1-158">Pile d’exécution</span><span class="sxs-lookup"><span data-stu-id="8b2f1-158">Runtime Stack</span></span>  | <span data-ttu-id="8b2f1-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="8b2f1-159">.NET Core 1.1</span></span>  | <span data-ttu-id="8b2f1-160">Version et pile d’exécution.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-160">The runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="8b2f1-161">Déployer votre application via Git</span><span class="sxs-lookup"><span data-stu-id="8b2f1-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="8b2f1-162">Utilisez Git pour déployer l’application .NET Core sur une application web Azure App Service sur Linux.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-162">Use Git to deploy the .NET Core application to Azure App Service Web App on Linux.</span></span>

<span data-ttu-id="8b2f1-163">Un déploiement Git est déjà configuré sur la nouvelle application web Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-163">The new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="8b2f1-164">Vous trouverez l’URL de déploiement Git en suivant l’URL suivante après avoir inséré le nom de votre application web :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-164">You will find the Git deployment URL by navigating to the following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="8b2f1-165">L’URL Git a la forme suivante, selon le nom de votre application web :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-165">The Git URL has the following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="8b2f1-166">Exécutez les commandes suivantes pour déployer l’application locale sur votre application web Azure :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-166">Run the following commands to deploy the local application to your Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="8b2f1-167">Vous n’avez pas besoin d’envoyer de fichiers sous les répertoires *bin/* ou *obj/*, car votre application est générée dans le cloud lorsque les fichiers source de l’application sont envoyés à Azure.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-167">You don't need to push any files under *bin/* or *obj/* directories because your application is built in the cloud when the application's source files are pushed to Azure.</span></span> <span data-ttu-id="8b2f1-168">Une fois le processus de génération terminé, les fichiers binaires sont copiés dans le répertoire de l’application à l’emplacement */home/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-168">After the build process is complete, binary files are copied into the application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="8b2f1-169">Vérifiez que les opérations de déploiement à distance réussissent.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-169">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="8b2f1-170">L’envoi des opérations peut prendre un certain temps, car la résolution de package et le processus de génération s’exécutent dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-170">Push operations may take a while since package resolution and build process run in the cloud.</span></span> <span data-ttu-id="8b2f1-171">Plusieurs messages d’état s’afficheront, y compris ceux indiquant que les fichiers ont été copiés.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="8b2f1-172">Le résultat doit être semblable à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-172">The output should look similar to the following:</span></span>

```bash
/* some output has been removed for brevity */
remote: Copying file: 'System.Net.Websockets.dll' 
remote: Copying file: 'System.Runtime.CompilerServices.Unsafe.dll' 
remote: Copying file: 'System.Runtime.Serialization.Primitives.dll' 
remote: Copying file: 'System.Text.Encodings.Web.dll' 
remote: Copying file: 'hellodotnetcore.deps.json' 
remote: Copying file: 'hellodotnetcore.dll' 
remote: Omitting next output lines...
remote: Finished successfully.
remote: Running post deployment commands...
remote: Deployment successful.
To https://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="8b2f1-173">Une fois le déploiement terminé, redémarrez votre application web pour que le déploiement prenne effet.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-173">Once the deployment has completed, restart your web app for the deployment to take effect.</span></span> <span data-ttu-id="8b2f1-174">Pour ce faire, accédez au portail Azure, puis à la page **Vue d’ensemble** de votre application web.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-174">To do this, go to the Azure portal and navigate to the **Overview** page of your web app.</span></span> <span data-ttu-id="8b2f1-175">Sélectionnez le bouton **Redémarrer** sur la page.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-175">Select the **Restart** button in the page.</span></span> <span data-ttu-id="8b2f1-176">Quand une fenêtre contextuelle s’affiche, sélectionnez **Oui** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="8b2f1-176">When a popup window shows up, select **Yes** to confirm.</span></span> <span data-ttu-id="8b2f1-177">Vous pouvez ensuite parcourir votre application web, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="8b2f1-177">You can then browse your web app, as shown here:</span></span>

![Exploration de l’application .NET Core déployée sur Azure App Service sur Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="8b2f1-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="8b2f1-179">Next steps</span></span>
* [<span data-ttu-id="8b2f1-180">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="8b2f1-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
