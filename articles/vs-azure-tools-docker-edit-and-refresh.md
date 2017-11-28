---
title: applications aaaDebugging dans un conteneur Docker local | Documents Microsoft
description: "Découvrez comment toomodify une application qui s’exécute dans un conteneur Docker local, actualiser le conteneur hello via modifier et actualiser et définir des points d’arrêt de débogage"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="f3eda-103">Débogage d’applications dans un conteneur Docker local</span><span class="sxs-lookup"><span data-stu-id="f3eda-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="f3eda-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f3eda-104">Overview</span></span>
<span data-ttu-id="f3eda-105">Hello Visual Studio Tools pour Docker fournit un toodevelop de manière cohérente dans et valider votre application localement dans un conteneur Linux Docker.</span><span class="sxs-lookup"><span data-stu-id="f3eda-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="f3eda-106">Vous n’avez conteneur de hello toorestart chaque fois que vous modifiez un code.</span><span class="sxs-lookup"><span data-stu-id="f3eda-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="f3eda-107">Cet article explique comment toouse hello « Modifier et actualiser » fonctionnalité toostart une application ASP.NET Core Web dans un conteneur Docker local, apportez les modifications nécessaires, puis actualisez hello navigateur toosee ces modifications.</span><span class="sxs-lookup"><span data-stu-id="f3eda-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="f3eda-108">Cet article montre également comment tooset les points d’arrêt pour le débogage.</span><span class="sxs-lookup"><span data-stu-id="f3eda-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="f3eda-109">La prise en charge des conteneurs Windows sera proposée dans une version ultérieure</span><span class="sxs-lookup"><span data-stu-id="f3eda-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="f3eda-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f3eda-110">Prerequisites</span></span>
<span data-ttu-id="f3eda-111">Hello suivant outils doit être installé.</span><span class="sxs-lookup"><span data-stu-id="f3eda-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="f3eda-112">Dernière version de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3eda-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="f3eda-113">Kit de développement logiciel (SDK) Microsoft ASP.NET Core 1.0</span><span class="sxs-lookup"><span data-stu-id="f3eda-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="f3eda-114">toorun Docker localement des conteneurs, vous aurez besoin d’un client local docker.</span><span class="sxs-lookup"><span data-stu-id="f3eda-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="f3eda-115">Vous pouvez utiliser hello [boîte à outils Docker](https://www.docker.com/products/docker-toolbox), ce qui nécessite toobe Hyper-V désactivé, ou vous pouvez utiliser [Docker pour Windows](https://www.docker.com/get-docker), qui utilise Hyper-V et qui nécessite Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f3eda-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="f3eda-116">Si vous utilisez la boîte à outils Docker, vous devez trop[configurer hello Docker client](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="f3eda-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="f3eda-117">1. Créer une application web</span><span class="sxs-lookup"><span data-stu-id="f3eda-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="f3eda-118">2. Ajouter la prise en charge Docker</span><span class="sxs-lookup"><span data-stu-id="f3eda-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="f3eda-119">3. Modifier votre code et actualiser</span><span class="sxs-lookup"><span data-stu-id="f3eda-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="f3eda-120">tooquickly itérer au sein des modifications, vous pouvez démarrer votre application dans un conteneur et continuer toomake modifications, les afficher comme vous le feriez avec IIS Express.</span><span class="sxs-lookup"><span data-stu-id="f3eda-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="f3eda-121">Définir hello Configuration de Solution trop`Debug` et appuyez sur  **&lt;CTRL + F5 >** toobuild votre docker de l’image et l’exécuter localement.</span><span class="sxs-lookup"><span data-stu-id="f3eda-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="f3eda-122">Une fois l’image de conteneur hello a été généré et s’exécute dans un conteneur Docker, Visual Studio lance l’application Web de hello dans votre navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="f3eda-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="f3eda-123">Si vous utilisez le navigateur Microsoft Edge de hello ou comportent des erreurs, consultez [dépannage](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span><span class="sxs-lookup"><span data-stu-id="f3eda-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="f3eda-124">Accédez à toohello sur la page, ce qui est là que nous allons toomake nos modifications.</span><span class="sxs-lookup"><span data-stu-id="f3eda-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="f3eda-125">Retournez tooVisual Studio et ouvrez `Views\Home\About.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f3eda-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="f3eda-126">Ajouter hello suivant HTML toohello contenu de la fin du fichier de hello et enregistrez les modifications de hello.</span><span class="sxs-lookup"><span data-stu-id="f3eda-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="f3eda-127">Affichage de fenêtre de sortie hello, lorsque hello build de .NET est terminée et vous voyez ces lignes, commutateur tooyour arrière navigateur et hello sur la page d’actualisation.</span><span class="sxs-lookup"><span data-stu-id="f3eda-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="f3eda-128">Vos modifications ont été appliquées !</span><span class="sxs-lookup"><span data-stu-id="f3eda-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="f3eda-129">4. Déboguer à l’aide de points d’arrêt</span><span class="sxs-lookup"><span data-stu-id="f3eda-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="f3eda-130">Souvent, modifications devez davantage inspection, en tirant parti des fonctionnalités de Visual Studio de débogage de hello.</span><span class="sxs-lookup"><span data-stu-id="f3eda-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="f3eda-131">Retournez tooVisual Studio et ouvrez`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="f3eda-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="f3eda-132">Remplacez contenu hello de méthode de About() hello par hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="f3eda-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="f3eda-133">Ensemble d’un point d’arrêt toohello à gauche de hello `string message`... ligne.</span><span class="sxs-lookup"><span data-stu-id="f3eda-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="f3eda-134">Accès  **&lt;F5 >** toostart de débogage.</span><span class="sxs-lookup"><span data-stu-id="f3eda-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="f3eda-135">Accédez à toohello sur la page toohit votre point d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="f3eda-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="f3eda-136">Basculer le point d’arrêt de tooVisual Studio tooview hello et inspecter la valeur hello du message.</span><span class="sxs-lookup"><span data-stu-id="f3eda-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="f3eda-137">Résumé</span><span class="sxs-lookup"><span data-stu-id="f3eda-137">Summary</span></span>
<span data-ttu-id="f3eda-138">Avec [Visual Studio 2015 Tools pour Docker](https://aka.ms/DockerToolsForVS), vous pouvez obtenir la productivité hello de travailler localement, réalisme hello production de développement dans un conteneur Docker.</span><span class="sxs-lookup"><span data-stu-id="f3eda-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f3eda-139">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="f3eda-139">Troubleshooting</span></span>
[<span data-ttu-id="f3eda-140">Résolution des problèmes de développement avec Docker pour Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f3eda-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="f3eda-141">En savoir plus sur Docker avec Visual Studio, Windows et Azure</span><span class="sxs-lookup"><span data-stu-id="f3eda-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="f3eda-142">[Outils Docker pour Visual Studio](http://aka.ms/dockertoolsforvs) : développer votre code .NET Core dans un conteneur</span><span class="sxs-lookup"><span data-stu-id="f3eda-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="f3eda-143">[Outils Docker pour Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) : créez et déployez des conteneurs Docker</span><span class="sxs-lookup"><span data-stu-id="f3eda-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="f3eda-144">[Outils Docker pour Visual Studio Code](http://aka.ms/dockertoolsforvscode) : services linguistiques pour la modification de fichiers Docker, avec plus de scénarios E2E à venir</span><span class="sxs-lookup"><span data-stu-id="f3eda-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="f3eda-145">[Informations sur le conteneur Windows](http://aka.ms/containers): informations sur Windows Server et Nano Server</span><span class="sxs-lookup"><span data-stu-id="f3eda-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="f3eda-146">[Service de conteneur Azure](https://azure.microsoft.com/services/container-service/) - [Contenu du service de conteneur Azure](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="f3eda-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="f3eda-147">Pour plus d’exemples de l’utilisation de Docker, consultez [utilisation de Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) de hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 connexion [démonstration](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="f3eda-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="f3eda-148">Pour plus des Démarrages rapides à partir de la démonstration de HealthClinic.biz hello, consultez [Démarrages rapides outils de développement Azure](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="f3eda-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="f3eda-149">Divers outils Docker</span><span class="sxs-lookup"><span data-stu-id="f3eda-149">Various Docker tools</span></span>
[<span data-ttu-id="f3eda-150">D’excellents outils Docker (blog de Steve Lasker)</span><span class="sxs-lookup"><span data-stu-id="f3eda-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="f3eda-151">Articles intéressants</span><span class="sxs-lookup"><span data-stu-id="f3eda-151">Good articles</span></span>
[<span data-ttu-id="f3eda-152">Présentation des tooMicroservices de NGINX</span><span class="sxs-lookup"><span data-stu-id="f3eda-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="f3eda-153">Présentations</span><span class="sxs-lookup"><span data-stu-id="f3eda-153">Presentations</span></span>
* [<span data-ttu-id="f3eda-154">Steve Lasker : Visual Studio Live Las Vegas 2016 - E2E Docker</span><span class="sxs-lookup"><span data-stu-id="f3eda-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="f3eda-155">Introduction tooASP.NET Core @ build 2016 - où vous à démonstration</span><span class="sxs-lookup"><span data-stu-id="f3eda-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="f3eda-156">Développement d’applications .NET dans des conteneurs, Channel 9</span><span class="sxs-lookup"><span data-stu-id="f3eda-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
