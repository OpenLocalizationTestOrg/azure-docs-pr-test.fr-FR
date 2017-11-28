---
title: aaaCreate une application web ASP.NET Core Visual Studio Code
description: "Ce didacticiel illustre comment toocreate un noyau ASP.NET web application à l’aide de Visual Studio Code."
services: app-service\web
documentationcenter: .net
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 877bff08-9ef7-405a-a1ca-1194f33c55f2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: cephalin
ms.openlocfilehash: 1c18c94984d71e88d2a5b792d68cb1c81e4a96d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="dad7c-103">Créer une application web ASP.NET Core dans Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="dad7c-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="dad7c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dad7c-104">Overview</span></span>
<span data-ttu-id="dad7c-105">Ce didacticiel vous montre comment toocreate une ASP.NET Core web à l’aide de l’application [Visual Studio Code (Visual Studio Code)](http://code.visualstudio.com//Docs/whyvscode) et déployez-le trop[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="dad7c-105">This tutorial shows you how toocreate an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it too[Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="dad7c-106">Bien que cet article fait référence à des applications de tooweb, elle s’applique également tooAPI applications et des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="dad7c-106">Although this article refers tooweb apps, it also applies tooAPI apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="dad7c-107">ASP.NET Core est une refonte importante d’ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="dad7c-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="dad7c-108">ASP.NET Core est un nouveau framework open source et interplateforme qui vous permet de créer des applications web modernes basées sur le cloud à l’aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="dad7c-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="dad7c-109">Pour plus d’informations, consultez [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="dad7c-109">For more information, see [Introduction tooASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="dad7c-110">Pour plus d'informations sur les applications Web Azure App Service, consultez la [Vue d'ensemble de Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dad7c-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="dad7c-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dad7c-111">Prerequisites</span></span>
* <span data-ttu-id="dad7c-112">Installation de [VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="dad7c-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="dad7c-113">Installation de Git - vous pouvez l’installer depuis l’un de ces emplacements : [Chocolatey](https://chocolatey.org/packages/git) ou [git-scm.com](http://git-scm.com/downloads). Si vous êtes tooGit nouveau, choisissez [git-scm.com](http://git-scm.com/downloads) et l’option hello trop**utiliser Git à partir de hello invite de commandes Windows**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads). If you are new tooGit, choose [git-scm.com](http://git-scm.com/downloads) and select hello option too**Use Git from hello Windows Command Prompt**.</span></span> <span data-ttu-id="dad7c-114">Une fois que vous installez Git, vous devez également e-mail et le nom d’utilisateur tooset hello Git comme il est requis plus loin dans le didacticiel de hello (lorsque vous effectuez une validation à partir de Code de Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="dad7c-114">Once you install Git, you'll also need tooset hello Git user name and email as it's required later in hello tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="dad7c-115">Installer ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="dad7c-115">Install ASP.NET Core</span></span>
<span data-ttu-id="dad7c-116">ASP.NET Core est une pile .NET lean conçue pour créer des applications web et cloud modernes capables de s’exécuter sur OS X, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="dad7c-116">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="dad7c-117">Il a été construit à partir de hello tooprovide d’arrière-plan une infrastructure de développement optimisé pour les applications qui sont soit cloud toohello déployé ou exécutés localement.</span><span class="sxs-lookup"><span data-stu-id="dad7c-117">It has been built from hello ground up tooprovide an optimized development framework for apps that are either deployed toohello cloud or run on-premises.</span></span> <span data-ttu-id="dad7c-118">Elle inclut des composants modulaires associés à des frais généraux réduits. Ainsi, vous bénéficiez d’une certaine flexibilité lors de la création de vos solutions.</span><span class="sxs-lookup"><span data-stu-id="dad7c-118">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="dad7c-119">Ce didacticiel est conçu tooget que vous avez démarré la création d’applications avec les dernières versions de développement hello de ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="dad7c-119">This tutorial is designed tooget you started building applications with hello latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="dad7c-120">Hello, suivant les instructions est tooWindows spécifique.</span><span class="sxs-lookup"><span data-stu-id="dad7c-120">hello following instructions are specific tooWindows.</span></span> <span data-ttu-id="dad7c-121">Pour obtenir des instructions d’installation sur OS X, Linux et Windows, consultez [Bien démarrer avec ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="dad7c-121">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="dad7c-122">Pour obtenir des instructions d’installation plus détaillées pour OS X, Linux et Windows, consultez [Installation d’ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="dad7c-122">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-hello-web-app"></a><span data-ttu-id="dad7c-123">Créer une application web de hello</span><span class="sxs-lookup"><span data-stu-id="dad7c-123">Create hello web app</span></span>
<span data-ttu-id="dad7c-124">Cette section vous montre comment tooscaffold une nouvelle application ASP.NET web application à l’aide d’outil de .NET CLI hello.</span><span class="sxs-lookup"><span data-stu-id="dad7c-124">This section shows you how tooscaffold a new app ASP.NET web app using hello .NET CLI tool.</span></span> 

1. <span data-ttu-id="dad7c-125">Entrez hello qui suit à l’invite de commandes toocreate hello projet dossier et une vue de structure hello application hello.</span><span class="sxs-lookup"><span data-stu-id="dad7c-125">Enter hello following at hello command prompt toocreate hello project folder and scaffold hello app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI dotnet - Générateur ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="dad7c-127">toorestore hello NuGet packages requis, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dad7c-127">toorestore hello necessary NuGet packages, run hello following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-hello-web-app-locally"></a><span data-ttu-id="dad7c-128">Exécuter l’application hello web localement</span><span class="sxs-lookup"><span data-stu-id="dad7c-128">Run hello web app locally</span></span>
<span data-ttu-id="dad7c-129">Maintenant que vous avez créé des hello web app et de récupérer tous les packages NuGet hello application hello, vous pouvez exécuter l’application hello web localement.</span><span class="sxs-lookup"><span data-stu-id="dad7c-129">Now that you have created hello web app and retrieved all hello NuGet packages for hello app, you can run hello web app locally.</span></span>

1. <span data-ttu-id="dad7c-130">Exécutez l’application hello (hello `dotnet run` commande générerez une application hello lorsqu’il est à jour) :</span><span class="sxs-lookup"><span data-stu-id="dad7c-130">Run hello app  (hello `dotnet run` command will build hello app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="dad7c-131">Ouvrez un navigateur et accédez toohello suivant l’URL.</span><span class="sxs-lookup"><span data-stu-id="dad7c-131">Open a browser and navigate toohello following URL.</span></span>
   
    <span data-ttu-id="dad7c-132">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="dad7c-132">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="dad7c-133">page par défaut de Hello de hello web app s’affiche comme suit.</span><span class="sxs-lookup"><span data-stu-id="dad7c-133">hello default page of hello web app will appear as follows.</span></span>
   
    ![Application Web locale dans un navigateur](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="dad7c-135">Fermez votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="dad7c-135">Close your browser.</span></span> <span data-ttu-id="dad7c-136">Bonjour **fenêtre commande**, appuyez sur **Ctrl + C** tooshut application hello et fermer hello **fenêtre commande**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-136">In hello **Command Window**, press **Ctrl+C** tooshut down hello application and close hello **Command Window**.</span></span> 

## <a name="create-a-web-app-in-hello-azure-portal"></a><span data-ttu-id="dad7c-137">Créer une application web Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="dad7c-137">Create a web app in hello Azure Portal</span></span>
<span data-ttu-id="dad7c-138">Hello suit vous guide dans la création d’une application web Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-138">hello following steps will guide you through creating a web app in hello Azure Portal.</span></span>

1. <span data-ttu-id="dad7c-139">Connectez-vous à toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dad7c-139">Log in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dad7c-140">Cliquez sur **nouveau** à hello haut à gauche du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="dad7c-140">Click **NEW** at hello top left of hello Portal.</span></span>
3. <span data-ttu-id="dad7c-141">Cliquez sur **Applications web > Application web**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-141">Click **Web Apps > Web App**.</span></span>
   
    ![Nouvelle application Web Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="dad7c-143">Entrez une valeur pour **Nom**, par exemple **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-143">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="dad7c-144">Notez que ce nom doit toobe unique, et le portail de hello qui appliquera lorsque vous essayez de nom de hello tooenter.</span><span class="sxs-lookup"><span data-stu-id="dad7c-144">Note that this name needs toobe unique, and hello portal will enforce that when you attempt tooenter hello name.</span></span> <span data-ttu-id="dad7c-145">Par conséquent, si vous sélectionnez une entrée une valeur différente, vous devez toosubstitute cette valeur pour chaque occurrence de **SampleWebAppDemo** que vous voyez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dad7c-145">Therefore, if you select a enter a different value, you'll need toosubstitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="dad7c-146">Sélectionnez un **plan App Service** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="dad7c-146">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="dad7c-147">Si vous créez un plan, sélectionnez hello niveau tarifaire, emplacement et autres options.</span><span class="sxs-lookup"><span data-stu-id="dad7c-147">If you create a new plan, select hello pricing tier, location, and other options.</span></span> <span data-ttu-id="dad7c-148">Pour plus d’informations sur les plans de Service d’applications, consultez l’article hello, [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dad7c-148">For more information on App Service plans, see hello article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Panneau Nouvelle application Web Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="dad7c-150">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-150">Click **Create**.</span></span>
   
    ![Panneau Application Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-hello-new-web-app"></a><span data-ttu-id="dad7c-152">Activer la publication Git de l’application web hello</span><span class="sxs-lookup"><span data-stu-id="dad7c-152">Enable Git publishing for hello new web app</span></span>
<span data-ttu-id="dad7c-153">GIT est un système de contrôle de version distribuée que vous pouvez utiliser toodeploy de votre application web de Service d’applications Azure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-153">Git is a distributed version control system that you can use toodeploy your Azure App Service web app.</span></span> <span data-ttu-id="dad7c-154">Vous allez stocker le code hello que vous écrivez pour votre application web dans un référentiel Git local et que vous déploierez votre tooAzure code en appuyant sur le référentiel distant de tooa.</span><span class="sxs-lookup"><span data-stu-id="dad7c-154">You'll store hello code you write for your web app in a local Git repository, and you'll deploy your code tooAzure by pushing tooa remote repository.</span></span>   

1. <span data-ttu-id="dad7c-155">Ouvrez une session sur hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="dad7c-155">Log into hello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="dad7c-156">Cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-156">Click **Browse**.</span></span>
3. <span data-ttu-id="dad7c-157">Cliquez sur **Web Apps** tooview une liste d’applications web de hello associés à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-157">Click **Web Apps** tooview a list of hello web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="dad7c-158">Sélectionnez l’application web hello que vous avez créé dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dad7c-158">Select hello web app you created in this tutorial.</span></span>
5. <span data-ttu-id="dad7c-159">Dans le panneau de l’application hello web, cliquez sur **paramètres** > **déploiement continu**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-159">In hello web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Hôte d’application Web Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="dad7c-161">Cliquez sur **Choisir la source > Référentiel Git local**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-161">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="dad7c-162">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-162">Click **OK**.</span></span>
   
    ![Référentiel Git local dans Microsoft Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="dad7c-164">Si vous n'avez pas précédemment configuré les informations d'identification de déploiement pour la publication d'une application Web ou d'une autre application App Service, configurez-les maintenant :</span><span class="sxs-lookup"><span data-stu-id="dad7c-164">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="dad7c-165">Cliquez sur **Paramètres** > **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-165">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="dad7c-166">Hello **définir les informations d’identification de déploiement** panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="dad7c-166">hello **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="dad7c-167">Créez un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="dad7c-167">Create a user name and password.</span></span>  <span data-ttu-id="dad7c-168">Vous aurez besoin de ce mot de passe lorsque vous configurerez Git.</span><span class="sxs-lookup"><span data-stu-id="dad7c-168">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="dad7c-169">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-169">Click **Save**.</span></span>
9. <span data-ttu-id="dad7c-170">Dans le panneau de l’application web, cliquez sur **Paramètres > Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-170">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="dad7c-171">URL de Hello du référentiel Git distant hello que vous allez déployer toois figurant sous **URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-171">hello URL of hello remote Git repository that you'll deploy toois shown under **GIT URL**.</span></span>
10. <span data-ttu-id="dad7c-172">Hello de copie **URL GIT** valeur pour une utilisation ultérieure dans le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="dad7c-172">Copy hello **GIT URL** value for later use in hello tutorial.</span></span>
    
    ![URL Git de Microsoft Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-tooazure-app-service"></a><span data-ttu-id="dad7c-174">Publier votre tooAzure d’application web du Service d’applications</span><span class="sxs-lookup"><span data-stu-id="dad7c-174">Publish your web app tooAzure App Service</span></span>
<span data-ttu-id="dad7c-175">Dans cette section, vous créez un référentiel Git local et push à partir de ce toodeploy tooAzure de référentiel votre tooAzure d’application web.</span><span class="sxs-lookup"><span data-stu-id="dad7c-175">In this section, you will create a local Git repository and push from that repository tooAzure toodeploy your web app tooAzure.</span></span>

1. <span data-ttu-id="dad7c-176">Dans le Code de Visual Studio, sélectionnez hello **Git** option dans la barre de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="dad7c-176">In VS Code, select hello **Git** option in hello left navigation bar.</span></span>
   
    ![Icône Git dans VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="dad7c-178">Sélectionnez **référentiel git de Initialize** toomake que votre espace de travail est sous contrôle de code source git.</span><span class="sxs-lookup"><span data-stu-id="dad7c-178">Select **Initialize git repository** toomake sure your workspace is under git source control.</span></span> 
   
    ![Initialiser Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="dad7c-180">Ouvrez hello fenêtre de commande et modifiez le répertoire de toohello de répertoires de votre application web.</span><span class="sxs-lookup"><span data-stu-id="dad7c-180">Open hello Command Window and change directories toohello directory of your web app.</span></span> <span data-ttu-id="dad7c-181">Ensuite, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="dad7c-181">Then, enter hello following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="dad7c-182">Cette commande empêche un problème lié au texte impliquant des terminaisons CRLF et des terminaisons LF.</span><span class="sxs-lookup"><span data-stu-id="dad7c-182">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="dad7c-183">Dans Visual Studio Code, ajoutez un message de validation, puis cliquez sur hello **validation tous les** icône de coche.</span><span class="sxs-lookup"><span data-stu-id="dad7c-183">In VS Code, add a commit message and click hello **Commit All** check icon.</span></span>
   
    ![Git - valider tout ](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="dad7c-185">Une fois Git a terminé le traitement, vous verrez qu’il n’y a aucun fichier répertorié dans la fenêtre de Git hello sous **modifications**.</span><span class="sxs-lookup"><span data-stu-id="dad7c-185">After Git has completed processing, you'll see that there are no files listed in hello Git window under **Changes**.</span></span> 
   
    ![Git - aucune modification](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="dad7c-187">Modifiez toohello arrière fenêtre de commande où invite de commandes hello pointe toohello répertoire où se trouve votre application web.</span><span class="sxs-lookup"><span data-stu-id="dad7c-187">Change back toohello Command Window where hello command prompt points toohello directory where your web app is located.</span></span>
7. <span data-ttu-id="dad7c-188">Créer une référence à distance pour pousser des mises à jour tooyour web app à l’aide de hello URL Git (numéro se termine par « .git ») que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="dad7c-188">Create a remote reference for pushing updates tooyour web app by using hello Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="dad7c-189">Configurer Git toosave vos informations d’identification localement afin qu’ils seront les commandes de push tooyour ajoutée automatiquement générées à partir de Code de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dad7c-189">Configure Git toosave your credentials locally so that they will be automatically appended tooyour push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="dad7c-190">Push tooAzure de vos modifications en entrant hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="dad7c-190">Push your changes tooAzure by entering hello following command.</span></span> <span data-ttu-id="dad7c-191">Cette tooAzure par émission de données initiale, vous serez en mesure de toodo par émission de données hello toutes les commandes à partir de Code de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dad7c-191">After this initial push tooAzure, you will be able toodo all hello push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="dad7c-192">Vous êtes invité au mot de passe hello créé précédemment dans Azure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-192">You are prompted for hello password you created earlier in Azure.</span></span> <span data-ttu-id="dad7c-193">**Remarque : votre mot de passe ne sera pas visible.**</span><span class="sxs-lookup"><span data-stu-id="dad7c-193">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="dad7c-194">sortie de Hello de hello au-dessus de commande se termine par un message que le déploiement a réussi.</span><span class="sxs-lookup"><span data-stu-id="dad7c-194">hello output from hello above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        toohttps://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="dad7c-195">Si vous apportez des modifications tooyour application, vous pouvez republier directement dans le Code de Visual Studio à l’aide d’une fonctionnalité intégrée Git hello en sélectionnant hello **valider tous les** option suivie hello **Push** option.</span><span class="sxs-lookup"><span data-stu-id="dad7c-195">If you make changes tooyour app, you can republish directly in VS Code using hello built-in Git functionality by selecting hello **Commit All** option followed by hello **Push** option.</span></span> <span data-ttu-id="dad7c-196">Vous trouverez hello **Push** option disponible dans toohello suivant du menu déroulant hello **valider tous les** et **Actualiser** boutons.</span><span class="sxs-lookup"><span data-stu-id="dad7c-196">You will find hello **Push** option available in hello drop-down menu next toohello **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="dad7c-197">Si vous devez toocollaborate sur un projet, vous devez envisager de pousser tooGitHub entre en exécutant un push tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-197">If you need toocollaborate on a project, you should consider pushing tooGitHub in between pushing tooAzure.</span></span>

## <a name="run-hello-app-in-azure"></a><span data-ttu-id="dad7c-198">Exécutez l’application hello dans Azure</span><span class="sxs-lookup"><span data-stu-id="dad7c-198">Run hello app in Azure</span></span>
<span data-ttu-id="dad7c-199">Maintenant que vous avez déployé votre application web, nous allons exécuter application hello tandis que hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-199">Now that you have deployed your web app, let's run hello app while hosted in Azure.</span></span> 

<span data-ttu-id="dad7c-200">Cette opération peut être réalisée de deux manières :</span><span class="sxs-lookup"><span data-stu-id="dad7c-200">This can be done in two ways:</span></span>

* <span data-ttu-id="dad7c-201">Ouvrez un navigateur et entrez le nom hello de votre application web comme suit.</span><span class="sxs-lookup"><span data-stu-id="dad7c-201">Open a browser and enter hello name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="dad7c-202">Dans hello portail Azure, recherchez le panneau de l’application hello web pour votre application web, puis cliquez sur **Parcourir** tooview votre application</span><span class="sxs-lookup"><span data-stu-id="dad7c-202">In hello Azure Portal, locate hello web app blade for your web app, and click **Browse** tooview your app</span></span> 
* <span data-ttu-id="dad7c-203">dans votre navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="dad7c-203">in your default browser.</span></span>

![Application Web Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="dad7c-205">Résumé</span><span class="sxs-lookup"><span data-stu-id="dad7c-205">Summary</span></span>
<span data-ttu-id="dad7c-206">Dans ce didacticiel, vous avez appris comment toocreate une application web dans le Code de Visual Studio et déployez-le tooAzure.</span><span class="sxs-lookup"><span data-stu-id="dad7c-206">In this tutorial, you learned how toocreate a web app in VS Code and deploy it tooAzure.</span></span> <span data-ttu-id="dad7c-207">Pour plus d’informations sur le Code de Visual Studio, consultez l’article hello, [pourquoi Visual Studio Code ?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="dad7c-207">For more information about VS Code, see hello article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="dad7c-208">Pour plus d’informations sur les applications web App Service, consultez [Vue d’ensemble des applications web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dad7c-208">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

