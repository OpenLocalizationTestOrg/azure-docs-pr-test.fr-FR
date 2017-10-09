---
title: "aaaUse .NET Core dans l’application Web sur Linux | Documents Microsoft"
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
ms.openlocfilehash: 9b7fb7185dff2c99ed88e7937d455177504937b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-core-in-an-azure-web-app-on-linux"></a><span data-ttu-id="95b0d-104">Utiliser .NET Core dans une application web Azure sur Linux</span><span class="sxs-lookup"><span data-stu-id="95b0d-104">Use .NET Core in an Azure web app on Linux</span></span> #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="95b0d-105">[Application Web](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) sur Linux fournit un service d’hébergement web hautement évolutifs et correction automatique à l’aide du système d’exploitation de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="95b0d-105">[Web App](https://docs.microsoft.com/azure/app-service-web/app-service-linux-intro) on Linux provides a highly scalable, self-patching web hosting service using hello Linux operating system.</span></span> <span data-ttu-id="95b0d-106">Ce didacticiel contient des instructions pas à pas montrant comment toocreate un [.NET Core](https://docs.microsoft.com/aspnet/core/) application sur l’application web Azure sous Linux.</span><span class="sxs-lookup"><span data-stu-id="95b0d-106">This tutorial contains step-by-step instructions showing how toocreate a [.NET Core](https://docs.microsoft.com/aspnet/core/) app on Azure web app on Linux.</span></span> 

![Application web sous Linux][10]

<span data-ttu-id="95b0d-108">Vous pouvez suivre les étapes de hello ci-dessous à l’aide d’un ordinateur Mac, Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="95b0d-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95b0d-109">Composants requis</span><span class="sxs-lookup"><span data-stu-id="95b0d-109">Prerequisites</span></span> ##

<span data-ttu-id="95b0d-110">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="95b0d-110">toocomplete this tutorial:</span></span> 

* <span data-ttu-id="95b0d-111">Installer hello [le Kit de développement .NET Core](https://www.microsoft.com/net/download/core).</span><span class="sxs-lookup"><span data-stu-id="95b0d-111">Install hello [.NET Core SDK](https://www.microsoft.com/net/download/core).</span></span>
* <span data-ttu-id="95b0d-112">Installez [Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="95b0d-112">Install [Git](https://git-scm.com/downloads).</span></span>

[!INCLUDE [Free trial note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-local-net-core-application"></a><span data-ttu-id="95b0d-113">Créer une application .NET Core locale</span><span class="sxs-lookup"><span data-stu-id="95b0d-113">Create a local .NET Core application</span></span> ##

<span data-ttu-id="95b0d-114">Démarrez une nouvelle session de terminal.</span><span class="sxs-lookup"><span data-stu-id="95b0d-114">Start a new terminal session.</span></span> <span data-ttu-id="95b0d-115">Créez un répertoire nommé `hellodotnetcore`et modifier hello Active directory tooit.</span><span class="sxs-lookup"><span data-stu-id="95b0d-115">Create a directory named `hellodotnetcore`, and change hello current directory tooit.</span></span> <span data-ttu-id="95b0d-116">Puis tapez ce qui suit hello :</span><span class="sxs-lookup"><span data-stu-id="95b0d-116">Then type hello following:</span></span> 

```
dotnet new web
``` 

  <span data-ttu-id="95b0d-117">Cette commande crée trois fichiers (*hellodotnetcore.csproj*, *Program.cs*, et *Startup.cs*) et un dossier vide (*wwwroot /*) sous le répertoire en cours de hello.</span><span class="sxs-lookup"><span data-stu-id="95b0d-117">This command creates three files (*hellodotnetcore.csproj*, *Program.cs*, and *Startup.cs*) and one empty folder (*wwwroot/*) under hello current directory.</span></span> <span data-ttu-id="95b0d-118">Hello contenu de `.csproj` fichier doit ressembler à hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="95b0d-118">hello content of `.csproj` file should look like hello following:</span></span> 

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

<span data-ttu-id="95b0d-119">Étant donné que cette application est une application web, un tooan référence package ASP.NET Core a été automatiquement ajouté toohello *hellodotnetcore.csproj* fichier.</span><span class="sxs-lookup"><span data-stu-id="95b0d-119">Since this app is a web application, a reference tooan ASP.NET Core package was automatically added toohello *hellodotnetcore.csproj* file.</span></span> <span data-ttu-id="95b0d-120">numéro de version de Hello du package de hello est définie en fonction de toohello choisi framework.</span><span class="sxs-lookup"><span data-stu-id="95b0d-120">hello version number of hello package is set according toohello chosen framework.</span></span> <span data-ttu-id="95b0d-121">Cet exemple fait référence à ASP.NET Core version 1.1.2, car .NET Core 1.1 est utilisé.</span><span class="sxs-lookup"><span data-stu-id="95b0d-121">This example is referencing ASP.NET Core version 1.1.2 because .NET Core 1.1 is used.</span></span>

## <a name="build-and-test-hello-application-locally"></a><span data-ttu-id="95b0d-122">Générer et tester l’application hello localement</span><span class="sxs-lookup"><span data-stu-id="95b0d-122">Build and test hello application locally</span></span> ##

<span data-ttu-id="95b0d-123">Vous pouvez générer et exécuter votre application .NET Core par hello `dotnet restore` commande suivie hello `dotnet run` de commande, comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="95b0d-123">You can build and run your .NET Core app with hello `dotnet restore` command followed by hello `dotnet run` command, as shown here:</span></span>

```
dotnet restore
dotnet run
```


<span data-ttu-id="95b0d-124">Lors de l’application hello démarre, il affiche un message indiquant l’application hello est à l’écoute des demandes tooincoming à un port.</span><span class="sxs-lookup"><span data-stu-id="95b0d-124">When hello application starts, it displays a message indicating hello app is listening tooincoming requests at a port.</span></span> 

```bash
Hosting environment: Production
Content root path: C:\hellodotnetcore
Now listening on: http://localhost:5000
Application started. Press Ctrl+C tooshut down.
```

<span data-ttu-id="95b0d-125">Testez-le en parcourant trop`http://localhost:5000/` avec votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="95b0d-125">Test it by browsing too`http://localhost:5000/` with your browser.</span></span> <span data-ttu-id="95b0d-126">Si tout fonctionne correctement, vous voyez « Hello World! »</span><span class="sxs-lookup"><span data-stu-id="95b0d-126">If everything works fine, you see "Hello World!"</span></span> <span data-ttu-id="95b0d-127">en tant que texte hello du résultat.</span><span class="sxs-lookup"><span data-stu-id="95b0d-127">as hello result text.</span></span>

![Tester avec un navigateur][7]

## <a name="create-a-net-core-app-in-hello-azure-portal"></a><span data-ttu-id="95b0d-129">Créer une application .NET Core Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="95b0d-129">Create a .NET Core app in hello Azure Portal</span></span> ##

<span data-ttu-id="95b0d-130">Tout d’abord, vous devez toocreate une application web vide.</span><span class="sxs-lookup"><span data-stu-id="95b0d-130">First you need toocreate an empty web app.</span></span> <span data-ttu-id="95b0d-131">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) et créer un nouveau [l’application Web sur Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span><span class="sxs-lookup"><span data-stu-id="95b0d-131">Log in toohello [Azure portal](https://portal.azure.com/) and create a new [Web App on Linux](https://portal.azure.com/#create/Microsoft.AppSvcLinux).</span></span>

![Création d’une application web][1]

<span data-ttu-id="95b0d-133">Hello lorsque **créer** s’ouvre, fournissez des détails sur votre application web :</span><span class="sxs-lookup"><span data-stu-id="95b0d-133">When hello **Create** page opens, provide details about your web app:</span></span>

![Choix d’une pile d’exécution .NET Core][2]

<span data-ttu-id="95b0d-135">Suivant de hello d’utilisation de table comme un toofill guide out hello **créer** page, puis sélectionnez **OK** et **créer** toocreate hello application.</span><span class="sxs-lookup"><span data-stu-id="95b0d-135">Use hello following table as a guide toofill out hello **Create** page, then select **OK** and **Create** toocreate hello app.</span></span>

| <span data-ttu-id="95b0d-136">Paramètre</span><span class="sxs-lookup"><span data-stu-id="95b0d-136">Setting</span></span>      | <span data-ttu-id="95b0d-137">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="95b0d-137">Suggested value</span></span>  | <span data-ttu-id="95b0d-138">Description</span><span class="sxs-lookup"><span data-stu-id="95b0d-138">Description</span></span>                                        |
| ------------ | ---------------- | -------------------------------------------------- |
| <span data-ttu-id="95b0d-139">Nom de l’application</span><span class="sxs-lookup"><span data-stu-id="95b0d-139">App name</span></span> | <span data-ttu-id="95b0d-140">hellodotnetcore</span><span class="sxs-lookup"><span data-stu-id="95b0d-140">hellodotnetcore</span></span>  | <span data-ttu-id="95b0d-141">nom Hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="95b0d-141">hello name of your app.</span></span> <span data-ttu-id="95b0d-142">Ce nom doit être unique.</span><span class="sxs-lookup"><span data-stu-id="95b0d-142">This name must be unique.</span></span> |
| <span data-ttu-id="95b0d-143">Abonnement</span><span class="sxs-lookup"><span data-stu-id="95b0d-143">Subscription</span></span> | <span data-ttu-id="95b0d-144">Choisir un abonnement existant</span><span class="sxs-lookup"><span data-stu-id="95b0d-144">Choose an existing subscription</span></span> | <span data-ttu-id="95b0d-145">Hello abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="95b0d-145">hello Azure subscription.</span></span> |
| <span data-ttu-id="95b0d-146">Groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="95b0d-146">Resource Group</span></span> | <span data-ttu-id="95b0d-147">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="95b0d-147">myResourceGroup</span></span> |  <span data-ttu-id="95b0d-148">ressource Azure groupe toocontain hello web application Hello.</span><span class="sxs-lookup"><span data-stu-id="95b0d-148">hello Azure resource group toocontain hello web app.</span></span> |
| <span data-ttu-id="95b0d-149">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="95b0d-149">App Service Plan</span></span> | <span data-ttu-id="95b0d-150">Nom de plan App Service existant</span><span class="sxs-lookup"><span data-stu-id="95b0d-150">Existing App Service Plan name</span></span> |  <span data-ttu-id="95b0d-151">Hello plan App Service.</span><span class="sxs-lookup"><span data-stu-id="95b0d-151">hello App Service plan.</span></span>  |
| <span data-ttu-id="95b0d-152">Configurer le conteneur</span><span class="sxs-lookup"><span data-stu-id="95b0d-152">Configure Container</span></span> | <span data-ttu-id="95b0d-153">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="95b0d-153">.NET Core 1.1</span></span> | <span data-ttu-id="95b0d-154">type de conteneur pour cette application web de Hello : Registre intégrées, Docker ou Private.</span><span class="sxs-lookup"><span data-stu-id="95b0d-154">hello type of container for this web app: Built-in, Docker, or Private registry.</span></span> |
| <span data-ttu-id="95b0d-155">Source d’image</span><span class="sxs-lookup"><span data-stu-id="95b0d-155">Image source</span></span>  | <span data-ttu-id="95b0d-156">Intégration</span><span class="sxs-lookup"><span data-stu-id="95b0d-156">Built-in</span></span>  |  <span data-ttu-id="95b0d-157">source de Hello d’image de hello.</span><span class="sxs-lookup"><span data-stu-id="95b0d-157">hello source of hello image.</span></span> |
| <span data-ttu-id="95b0d-158">Pile d’exécution</span><span class="sxs-lookup"><span data-stu-id="95b0d-158">Runtime Stack</span></span>  | <span data-ttu-id="95b0d-159">.NET Core 1.1</span><span class="sxs-lookup"><span data-stu-id="95b0d-159">.NET Core 1.1</span></span>  | <span data-ttu-id="95b0d-160">pile de runtime Hello et la version.</span><span class="sxs-lookup"><span data-stu-id="95b0d-160">hello runtime stack and version.</span></span>  |

## <a name="deploy-your-application-via-git"></a><span data-ttu-id="95b0d-161">Déployer votre application via Git</span><span class="sxs-lookup"><span data-stu-id="95b0d-161">Deploy your application via Git</span></span> ##

<span data-ttu-id="95b0d-162">Utiliser Git toodeploy hello .NET Core application tooAzure application de Service d’applications Web sur Linux.</span><span class="sxs-lookup"><span data-stu-id="95b0d-162">Use Git toodeploy hello .NET Core application tooAzure App Service Web App on Linux.</span></span>

<span data-ttu-id="95b0d-163">application web Azure Hello possède déjà un déploiement Git configuré.</span><span class="sxs-lookup"><span data-stu-id="95b0d-163">hello new Azure web app already has Git deployment configured.</span></span> <span data-ttu-id="95b0d-164">Vous trouverez des URL de déploiement Git hello en naviguant toohello suivant URL après avoir inséré le nom de votre application web :</span><span class="sxs-lookup"><span data-stu-id="95b0d-164">You will find hello Git deployment URL by navigating toohello following URL after inserting your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/api/scm/info```

<span data-ttu-id="95b0d-165">Hello URL Git a hello suivant du formulaire basé sur le nom de votre application web :</span><span class="sxs-lookup"><span data-stu-id="95b0d-165">hello Git URL has hello following form based on your web app name:</span></span>

```https://{your web app name}.scm.azurewebsites.net/{your web app name}.git```

<span data-ttu-id="95b0d-166">Exécutez hello suivant de commandes toodeploy hello application locale tooyour Azure web app :</span><span class="sxs-lookup"><span data-stu-id="95b0d-166">Run hello following commands toodeploy hello local application tooyour Azure web app:</span></span> 
 
```bash
git init
git remote add azure <Git deployment URL from above>
git add *.csproj *.cs
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="95b0d-167">Vous n’avez pas besoin toopush tous les fichiers sous *bin /* ou *obj /* répertoires, car votre application est générée dans le cloud de hello lorsque hello l’application fichiers sources sont envoyées tooAzure.</span><span class="sxs-lookup"><span data-stu-id="95b0d-167">You don't need toopush any files under *bin/* or *obj/* directories because your application is built in hello cloud when hello application's source files are pushed tooAzure.</span></span> <span data-ttu-id="95b0d-168">Une fois le processus de génération hello est terminée, les fichiers binaires sont copiés dans le répertoire de l’application hello dans */home/site/wwwroot/*.</span><span class="sxs-lookup"><span data-stu-id="95b0d-168">After hello build process is complete, binary files are copied into hello application's directory at */home/site/wwwroot/*.</span></span>

<span data-ttu-id="95b0d-169">Vérifiez que les opérations de déploiement à distance de hello signalent la réussite.</span><span class="sxs-lookup"><span data-stu-id="95b0d-169">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="95b0d-170">Les opérations de push peuvent prendre un certain temps depuis la résolution de package et s’exécutent dans le cloud de hello de processus de génération.</span><span class="sxs-lookup"><span data-stu-id="95b0d-170">Push operations may take a while since package resolution and build process run in hello cloud.</span></span> <span data-ttu-id="95b0d-171">Plusieurs messages d’état s’afficheront, y compris ceux indiquant que les fichiers ont été copiés.</span><span class="sxs-lookup"><span data-stu-id="95b0d-171">You will see several status messages, including ones stating that files have been copied.</span></span> <span data-ttu-id="95b0d-172">sortie de Hello doit ressembler similaire toohello suivantes :</span><span class="sxs-lookup"><span data-stu-id="95b0d-172">hello output should look similar toohello following:</span></span>

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
toohttps://hellodotnetcore.scm.azurewebsites.net/
 * [new branch]           master -> master

```

<span data-ttu-id="95b0d-173">Une fois le déploiement de hello est terminée, redémarrez votre application web pour effet de tootake déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="95b0d-173">Once hello deployment has completed, restart your web app for hello deployment tootake effect.</span></span> <span data-ttu-id="95b0d-174">toodo, accédez toohello portail Azure et accédez toohello **vue d’ensemble** page de votre application web.</span><span class="sxs-lookup"><span data-stu-id="95b0d-174">toodo this, go toohello Azure portal and navigate toohello **Overview** page of your web app.</span></span> <span data-ttu-id="95b0d-175">Sélectionnez hello **redémarrer** bouton dans la page de hello.</span><span class="sxs-lookup"><span data-stu-id="95b0d-175">Select hello **Restart** button in hello page.</span></span> <span data-ttu-id="95b0d-176">Quand une fenêtre contextuelle s’affiche, sélectionnez **Oui** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="95b0d-176">When a popup window shows up, select **Yes** tooconfirm.</span></span> <span data-ttu-id="95b0d-177">Vous pouvez ensuite parcourir votre application web, comme illustré ici :</span><span class="sxs-lookup"><span data-stu-id="95b0d-177">You can then browse your web app, as shown here:</span></span>

![Navigation .NET Core application déployée tooAzure du Service d’applications sur Linux][10]

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="95b0d-179">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="95b0d-179">Next steps</span></span>
* [<span data-ttu-id="95b0d-180">FAQ de l’application web Azure App Service sur Linux</span><span class="sxs-lookup"><span data-stu-id="95b0d-180">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md)

[1]: ./media/app-service-linux-using-dotnetcore/top-level-create.png
[2]: ./media/app-service-linux-using-dotnetcore/dotnet-new-webapp.png
[7]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-local.png
[10]: ./media/app-service-linux-using-dotnetcore/dotnet-browse-azure.png
