---
title: "Créer une application web ASP.NET Core dans Visual Studio Code"
description: "Ce tutoriel montre comment créer une application web ASP.NET Core via Visual Studio Code."
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
ms.openlocfilehash: 46e3852dc84265de41bb358f482dec06608e7efa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-visual-studio-code"></a><span data-ttu-id="78aff-103">Créer une application web ASP.NET Core dans Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="78aff-103">Create an ASP.NET Core web app in Visual Studio Code</span></span>
## <a name="overview"></a><span data-ttu-id="78aff-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="78aff-104">Overview</span></span>
<span data-ttu-id="78aff-105">Ce tutoriel vous montre comment créer une application web ASP.NET Core à l’aide de [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) et comment la déployer dans [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="78aff-105">This tutorial shows you how to create an ASP.NET Core web app using [Visual Studio Code (VS Code)](http://code.visualstudio.com//Docs/whyvscode) and deploy it to [Azure App Service](../app-service/app-service-value-prop-what-is.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="78aff-106">Même si cet article fait référence aux applications Web, il s’applique également aux applications API et aux applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="78aff-106">Although this article refers to web apps, it also applies to API apps and mobile apps.</span></span> 
> 
> 

<span data-ttu-id="78aff-107">ASP.NET Core est une refonte importante d’ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="78aff-107">ASP.NET Core is a significant redesign of ASP.NET.</span></span> <span data-ttu-id="78aff-108">ASP.NET Core est un nouveau framework open source et interplateforme qui vous permet de créer des applications web modernes basées sur le cloud à l’aide de .NET.</span><span class="sxs-lookup"><span data-stu-id="78aff-108">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based web apps using .NET.</span></span> <span data-ttu-id="78aff-109">Pour plus d’informations, consultez la page [Présentation d’ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span><span class="sxs-lookup"><span data-stu-id="78aff-109">For more information, see [Introduction to ASP.NET Core](http://docs.asp.net/latest/conceptual-overview/aspnet.html).</span></span> <span data-ttu-id="78aff-110">Pour plus d'informations sur les applications Web Azure App Service, consultez la [Vue d'ensemble de Web Apps](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78aff-110">For information about Azure App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span>

[!INCLUDE [app-service-web-try-app-service.md](../../includes/app-service-web-try-app-service.md)]

## <a name="prerequisites"></a><span data-ttu-id="78aff-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="78aff-111">Prerequisites</span></span>
* <span data-ttu-id="78aff-112">Installation de [VS Code](http://code.visualstudio.com/Docs/setup).</span><span class="sxs-lookup"><span data-stu-id="78aff-112">Install [VS Code](http://code.visualstudio.com/Docs/setup).</span></span>
* <span data-ttu-id="78aff-113">Installation de Git - vous pouvez l’installer depuis l’un de ces emplacements : [Chocolatey](https://chocolatey.org/packages/git) ou [git-scm.com](http://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="78aff-113">Install Git - You can install it from either of these locations: [Chocolatey](https://chocolatey.org/packages/git) or [git-scm.com](http://git-scm.com/downloads).</span></span> <span data-ttu-id="78aff-114">Si vous n’êtes pas familiarisé avec Git, choisissez [git-scm.com](http://git-scm.com/downloads) et sélectionnez l’option vous permettant d’ **utiliser Git à partir de l’invite de commandes Windows**.</span><span class="sxs-lookup"><span data-stu-id="78aff-114">If you are new to Git, choose [git-scm.com](http://git-scm.com/downloads) and select the option to **Use Git from the Windows Command Prompt**.</span></span> <span data-ttu-id="78aff-115">Une fois Git installé, vous devrez également définir le nom d'utilisateur et l’adresse de messagerie Git qui vous seront ultérieurement demandés dans ce didacticiel (lorsque vous effectuerez une validation à partir de VS Code).</span><span class="sxs-lookup"><span data-stu-id="78aff-115">Once you install Git, you'll also need to set the Git user name and email as it's required later in the tutorial (when performing a commit from VS Code).</span></span>  

## <a name="install-aspnet-core"></a><span data-ttu-id="78aff-116">Installer ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="78aff-116">Install ASP.NET Core</span></span>
<span data-ttu-id="78aff-117">ASP.NET Core est une pile .NET lean conçue pour créer des applications web et cloud modernes capables de s’exécuter sur OS X, Linux et Windows.</span><span class="sxs-lookup"><span data-stu-id="78aff-117">ASP.NET Core is a lean .NET stack for building modern cloud and web apps that run on OS X, Linux, and Windows.</span></span> <span data-ttu-id="78aff-118">Elle a été construite intégralement pour fournir une infrastructure de développement optimisée pour les applications qui sont déployées sur le cloud ou qui sont exécutées en local.</span><span class="sxs-lookup"><span data-stu-id="78aff-118">It has been built from the ground up to provide an optimized development framework for apps that are either deployed to the cloud or run on-premises.</span></span> <span data-ttu-id="78aff-119">Elle inclut des composants modulaires associés à des frais généraux réduits. Ainsi, vous bénéficiez d’une certaine flexibilité lors de la création de vos solutions.</span><span class="sxs-lookup"><span data-stu-id="78aff-119">It consists of modular components with minimal overhead, so you retain flexibility while constructing your solutions.</span></span>

<span data-ttu-id="78aff-120">Ce tutoriel vise à vous aider à créer des applications à l’aide des dernières versions de développement d’ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="78aff-120">This tutorial is designed to get you started building applications with the latest development versions of ASP.NET Core.</span></span> <span data-ttu-id="78aff-121">Les instructions suivantes sont spécifiques à Windows.</span><span class="sxs-lookup"><span data-stu-id="78aff-121">The following instructions are specific to Windows.</span></span> <span data-ttu-id="78aff-122">Pour obtenir des instructions d’installation sur OS X, Linux et Windows, consultez [Bien démarrer avec ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span><span class="sxs-lookup"><span data-stu-id="78aff-122">For installation instructions on OS X, Linux, and Windows, see [Getting Started with ASP.NET Core](https://docs.microsoft.com/aspnet/core/getting-started).</span></span> 


> [!NOTE]
> <span data-ttu-id="78aff-123">Pour obtenir des instructions d’installation plus détaillées pour OS X, Linux et Windows, consultez [Installation d’ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span><span class="sxs-lookup"><span data-stu-id="78aff-123">For more detailed installation instructions for OS X, Linux, and Windows, see [Installing ASP.NET Core](https://code.visualstudio.com/Docs/ASPnet5#_installing-aspnet-5-and-dnx).</span></span> 
> 
> 

## <a name="create-the-web-app"></a><span data-ttu-id="78aff-124">Créer l’application web</span><span class="sxs-lookup"><span data-stu-id="78aff-124">Create the web app</span></span>
<span data-ttu-id="78aff-125">Cette section vous montre comment structurer une nouvelle application web ASP.NET à l’aide de l’outil CLI .NET.</span><span class="sxs-lookup"><span data-stu-id="78aff-125">This section shows you how to scaffold a new app ASP.NET web app using the .NET CLI tool.</span></span> 

1. <span data-ttu-id="78aff-126">Entrez la commande suivante dans l'invite de commandes pour créer le dossier du projet et structurer l'application.</span><span class="sxs-lookup"><span data-stu-id="78aff-126">Enter the following at the command prompt to create the project folder and scaffold the app.</span></span>
   
```terminal
mkdir SampleWebApp
cd SampleWebApp
dotnet new mvc
```
![CLI dotnet - Générateur ASP.NET Core](./media/web-sites-create-web-app-using-vscode/dotnetcore-mvc-01.png)

2. <span data-ttu-id="78aff-128">Pour restaurer les packages NuGet nécessaires, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="78aff-128">To restore the necessary NuGet packages, run the following command:</span></span>
   
    ```terminal
    dotnet restore
    ```

## <a name="run-the-web-app-locally"></a><span data-ttu-id="78aff-129">Exécuter l’application web localement</span><span class="sxs-lookup"><span data-stu-id="78aff-129">Run the web app locally</span></span>
<span data-ttu-id="78aff-130">Maintenant que vous avez créé l'application Web et extrait tous les packages NuGet pour l'application, vous pouvez exécuter l'application Web localement.</span><span class="sxs-lookup"><span data-stu-id="78aff-130">Now that you have created the web app and retrieved all the NuGet packages for the app, you can run the web app locally.</span></span>

1. <span data-ttu-id="78aff-131">Exécutez l’application (la commande `dotnet run` génère l’application quand elle est obsolète) :</span><span class="sxs-lookup"><span data-stu-id="78aff-131">Run the app  (the `dotnet run` command will build the app when it's out of date):</span></span>
    ```terminal
    dotnet run
    ```
2. <span data-ttu-id="78aff-132">Ouvrez un navigateur et accédez à l'URL suivante.</span><span class="sxs-lookup"><span data-stu-id="78aff-132">Open a browser and navigate to the following URL.</span></span>
   
    <span data-ttu-id="78aff-133">**http://localhost:5000**</span><span class="sxs-lookup"><span data-stu-id="78aff-133">**http://localhost:5000**</span></span>
   
    <span data-ttu-id="78aff-134">La page par défaut de l’application Web apparaîtra comme suit.</span><span class="sxs-lookup"><span data-stu-id="78aff-134">The default page of the web app will appear as follows.</span></span>
   
    ![Application Web locale dans un navigateur](./media/web-sites-create-web-app-using-vscode/08-web-app.png)
3. <span data-ttu-id="78aff-136">Fermez votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="78aff-136">Close your browser.</span></span> <span data-ttu-id="78aff-137">Dans la **Fenêtre de commande**, appuyez sur **Ctrl+C** pour arrêter l’application et fermer la **Fenêtre de commande**.</span><span class="sxs-lookup"><span data-stu-id="78aff-137">In the **Command Window**, press **Ctrl+C** to shut down the application and close the **Command Window**.</span></span> 

## <a name="create-a-web-app-in-the-azure-portal"></a><span data-ttu-id="78aff-138">Créer une application web dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="78aff-138">Create a web app in the Azure Portal</span></span>
<span data-ttu-id="78aff-139">La procédure suivante vous guidera dans la création d'une application Web dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-139">The following steps will guide you through creating a web app in the Azure Portal.</span></span>

1. <span data-ttu-id="78aff-140">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78aff-140">Log in to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78aff-141">Cliquez sur **NOUVEAU** en haut à gauche du portail.</span><span class="sxs-lookup"><span data-stu-id="78aff-141">Click **NEW** at the top left of the Portal.</span></span>
3. <span data-ttu-id="78aff-142">Cliquez sur **Applications web > Application web**.</span><span class="sxs-lookup"><span data-stu-id="78aff-142">Click **Web Apps > Web App**.</span></span>
   
    ![Nouvelle application Web Azure](./media/web-sites-create-web-app-using-vscode/09-azure-newwebapp.png)
4. <span data-ttu-id="78aff-144">Entrez une valeur pour **Nom**, par exemple **SampleWebAppDemo**.</span><span class="sxs-lookup"><span data-stu-id="78aff-144">Enter a value for **Name**, such as **SampleWebAppDemo**.</span></span> <span data-ttu-id="78aff-145">Notez que ce nom doit être unique et qu’il sera imposé par le portail lorsque vous essayerez d'entrer le nom.</span><span class="sxs-lookup"><span data-stu-id="78aff-145">Note that this name needs to be unique, and the portal will enforce that when you attempt to enter the name.</span></span> <span data-ttu-id="78aff-146">Par conséquent, si vous décidez d’entrer une valeur différente, vous devez remplacer cette valeur pour chaque occurrence de **SampleWebAppDemo** que vous apercevez dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78aff-146">Therefore, if you select a enter a different value, you'll need to substitute that value for each occurrence of **SampleWebAppDemo** that you see in this tutorial.</span></span> 
5. <span data-ttu-id="78aff-147">Sélectionnez un **plan App Service** existant ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="78aff-147">Select an existing **App Service Plan** or create a new one.</span></span> <span data-ttu-id="78aff-148">Si vous créez un plan, sélectionnez le niveau de tarification, l’emplacement et d’autres options.</span><span class="sxs-lookup"><span data-stu-id="78aff-148">If you create a new plan, select the pricing tier, location, and other options.</span></span> <span data-ttu-id="78aff-149">Pour plus d’informations sur les plans App Service, consultez la rubrique [Présentation détaillée des plans d’Azure App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78aff-149">For more information on App Service plans, see the article, [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
    ![Panneau Nouvelle application Web Azure](./media/web-sites-create-web-app-using-vscode/10-azure-newappblade.png)
6. <span data-ttu-id="78aff-151">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="78aff-151">Click **Create**.</span></span>
   
    ![Panneau Application Web](./media/web-sites-create-web-app-using-vscode/11-azure-webappblade.png)

## <a name="enable-git-publishing-for-the-new-web-app"></a><span data-ttu-id="78aff-153">Activer la publication Git pour la nouvelle application Web</span><span class="sxs-lookup"><span data-stu-id="78aff-153">Enable Git publishing for the new web app</span></span>
<span data-ttu-id="78aff-154">Git est un système de contrôle de version distribué permettant de déployer votre application Web Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="78aff-154">Git is a distributed version control system that you can use to deploy your Azure App Service web app.</span></span> <span data-ttu-id="78aff-155">Vous stockerez le code que vous écrivez pour votre application Web dans un référentiel Git local, et vous déploierez votre code dans Azure par transmission de type Push vers un référentiel distant.</span><span class="sxs-lookup"><span data-stu-id="78aff-155">You'll store the code you write for your web app in a local Git repository, and you'll deploy your code to Azure by pushing to a remote repository.</span></span>   

1. <span data-ttu-id="78aff-156">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78aff-156">Log into the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="78aff-157">Cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="78aff-157">Click **Browse**.</span></span>
3. <span data-ttu-id="78aff-158">Cliquez sur **Applications Web** pour afficher la liste des applications Web associées à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-158">Click **Web Apps** to view a list of the web apps associated with your Azure subscription.</span></span>
4. <span data-ttu-id="78aff-159">Sélectionnez l'application Web que vous avez créée dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78aff-159">Select the web app you created in this tutorial.</span></span>
5. <span data-ttu-id="78aff-160">Dans le panneau de l’application web, cliquez sur **Paramètres** > **Déploiement continu**.</span><span class="sxs-lookup"><span data-stu-id="78aff-160">In the web app blade, click **Settings** > **Continuous deployment**.</span></span> 
   
    ![Hôte d’application Web Azure](./media/web-sites-create-web-app-using-vscode/14-azure-deployment.png)
6. <span data-ttu-id="78aff-162">Cliquez sur **Choisir la source > Référentiel Git local**.</span><span class="sxs-lookup"><span data-stu-id="78aff-162">Click **Choose Source > Local Git Repository**.</span></span>
7. <span data-ttu-id="78aff-163">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="78aff-163">Click **OK**.</span></span>
   
    ![Référentiel Git local dans Microsoft Azure](./media/web-sites-create-web-app-using-vscode/15-azure-localrepository.png)
8. <span data-ttu-id="78aff-165">Si vous n'avez pas précédemment configuré les informations d'identification de déploiement pour la publication d'une application Web ou d'une autre application App Service, configurez-les maintenant :</span><span class="sxs-lookup"><span data-stu-id="78aff-165">If you have not previously set up deployment credentials for publishing a web app or other App Service app, set them up now:</span></span>
   
   * <span data-ttu-id="78aff-166">Cliquez sur **Paramètres** > **Informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="78aff-166">Click **Settings** > **Deployment credentials**.</span></span> <span data-ttu-id="78aff-167">Le panneau **Définir les informations d’identification de déploiement** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="78aff-167">The **Set deployment credentials** blade will be displayed.</span></span>
   * <span data-ttu-id="78aff-168">Créez un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="78aff-168">Create a user name and password.</span></span>  <span data-ttu-id="78aff-169">Vous aurez besoin de ce mot de passe lorsque vous configurerez Git.</span><span class="sxs-lookup"><span data-stu-id="78aff-169">You'll need this password later when setting up Git.</span></span>
   * <span data-ttu-id="78aff-170">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="78aff-170">Click **Save**.</span></span>
9. <span data-ttu-id="78aff-171">Dans le panneau de l’application web, cliquez sur **Paramètres > Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="78aff-171">In your web app's blade, click **Settings > Properties**.</span></span> <span data-ttu-id="78aff-172">L'URL du référentiel Git distant vers lequel vous allez déployer se trouve sous **URL GIT**.</span><span class="sxs-lookup"><span data-stu-id="78aff-172">The URL of the remote Git repository that you'll deploy to is shown under **GIT URL**.</span></span>
10. <span data-ttu-id="78aff-173">Copiez la valeur **URL GIT** pour pouvoir l’utiliser plus tard dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="78aff-173">Copy the **GIT URL** value for later use in the tutorial.</span></span>
    
    ![URL Git de Microsoft Azure](./media/web-sites-create-web-app-using-vscode/17-azure-giturl.png)

## <a name="publish-your-web-app-to-azure-app-service"></a><span data-ttu-id="78aff-175">Publier votre application Web sur Azure App Service</span><span class="sxs-lookup"><span data-stu-id="78aff-175">Publish your web app to Azure App Service</span></span>
<span data-ttu-id="78aff-176">Dans cette section, vous créerez un référentiel Git local et vous effectuerez une transmission de type Push depuis ce référentiel vers Azure pour déployer votre application Web sur Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-176">In this section, you will create a local Git repository and push from that repository to Azure to deploy your web app to Azure.</span></span>

1. <span data-ttu-id="78aff-177">Dans VS Code, sélectionnez l’option **Git** dans la barre de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="78aff-177">In VS Code, select the **Git** option in the left navigation bar.</span></span>
   
    ![Icône Git dans VS Code](./media/web-sites-create-web-app-using-vscode/git-icon.png)
2. <span data-ttu-id="78aff-179">Sélectionnez **Initialiser le référentiel Git** pour vous assurer que votre espace de travail est sous le contrôle de code source Git.</span><span class="sxs-lookup"><span data-stu-id="78aff-179">Select **Initialize git repository** to make sure your workspace is under git source control.</span></span> 
   
    ![Initialiser Git](./media/web-sites-create-web-app-using-vscode/19-initgit.png)
3. <span data-ttu-id="78aff-181">Ouvrez la fenêtre de commande et remplacez les répertoires par le répertoire hébergeant votre application web.</span><span class="sxs-lookup"><span data-stu-id="78aff-181">Open the Command Window and change directories to the directory of your web app.</span></span> <span data-ttu-id="78aff-182">Puis, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="78aff-182">Then, enter the following command:</span></span>
   
        git config core.autocrlf false
   
    <span data-ttu-id="78aff-183">Cette commande empêche un problème lié au texte impliquant des terminaisons CRLF et des terminaisons LF.</span><span class="sxs-lookup"><span data-stu-id="78aff-183">This command prevents an issue about text where CRLF endings and LF endings are involved.</span></span>
4. <span data-ttu-id="78aff-184">Dans VS Code, ajoutez un message de validation, puis cliquez sur l’icône de coche **Valider tout** .</span><span class="sxs-lookup"><span data-stu-id="78aff-184">In VS Code, add a commit message and click the **Commit All** check icon.</span></span>
   
    ![Git - valider tout ](./media/web-sites-create-web-app-using-vscode/20-git-commit.png)
5. <span data-ttu-id="78aff-186">Une fois le traitement de Git terminé, vous apercevrez qu'il n'y a aucun fichier répertorié dans la fenêtre Git sous **Modifications**.</span><span class="sxs-lookup"><span data-stu-id="78aff-186">After Git has completed processing, you'll see that there are no files listed in the Git window under **Changes**.</span></span> 
   
    ![Git - aucune modification](./media/web-sites-create-web-app-using-vscode/no-changes.png)
6. <span data-ttu-id="78aff-188">Rétablissez la fenêtre de commande où l'invite de commande désigne le répertoire où se trouve votre application web.</span><span class="sxs-lookup"><span data-stu-id="78aff-188">Change back to the Command Window where the command prompt points to the directory where your web app is located.</span></span>
7. <span data-ttu-id="78aff-189">Créez une référence distante pour envoyer les mises à jour vers l'application Web en utilisant l'URL Git (finissant par « .git ») que vous avez copiée plus tôt.</span><span class="sxs-lookup"><span data-stu-id="78aff-189">Create a remote reference for pushing updates to your web app by using the Git URL (ending in ".git") that you copied earlier.</span></span>
   
        git remote add azure [URL for remote repository]
8. <span data-ttu-id="78aff-190">Configurez Git pour enregistrer vos informations d'identification localement afin qu'elles soient automatiquement ajoutées à vos commandes push générées à partir de VS Code.</span><span class="sxs-lookup"><span data-stu-id="78aff-190">Configure Git to save your credentials locally so that they will be automatically appended to your push commands generated from VS Code.</span></span>
   
        git config credential.helper store
9. <span data-ttu-id="78aff-191">Envoyez vos modifications dans Azure en entrant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="78aff-191">Push your changes to Azure by entering the following command.</span></span> <span data-ttu-id="78aff-192">Après cette commande push initiale vers Azure, vous pourrez exécuter toutes les commandes push à partir de VS Code.</span><span class="sxs-lookup"><span data-stu-id="78aff-192">After this initial push to Azure, you will be able to do all the push commands from VS Code.</span></span> 
   
        git push -u azure master
   
    <span data-ttu-id="78aff-193">Vous êtes invité à entrer le mot de passe que vous avez créé précédemment dans Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-193">You are prompted for the password you created earlier in Azure.</span></span> <span data-ttu-id="78aff-194">**Remarque : votre mot de passe ne sera pas visible.**</span><span class="sxs-lookup"><span data-stu-id="78aff-194">**Note: Your password will not be visible.**</span></span>
   
    <span data-ttu-id="78aff-195">La sortie de la commande mentionnée ci-dessus se termine par un message indiquant que le déploiement a réussi.</span><span class="sxs-lookup"><span data-stu-id="78aff-195">The output from the above command ends with a message that deployment is successful.</span></span>
   
        remote: Deployment successful.
        To https://user@testsite.scm.azurewebsites.net/testsite.git
        [new branch]      master -> master

> [!NOTE]
> <span data-ttu-id="78aff-196">Si vous apportez des modifications à votre application, vous pouvez republier directement dans VS Code à l’aide de la fonctionnalité intégrée de Git en sélectionnant l’option **Valider tout** suivie de l’option **Push**.</span><span class="sxs-lookup"><span data-stu-id="78aff-196">If you make changes to your app, you can republish directly in VS Code using the built-in Git functionality by selecting the **Commit All** option followed by the **Push** option.</span></span> <span data-ttu-id="78aff-197">Vous trouverez l’option **Push** dans le menu déroulant à côté des boutons **Valider tout** et **Actualiser**.</span><span class="sxs-lookup"><span data-stu-id="78aff-197">You will find the **Push** option available in the drop-down menu next to the **Commit All** and **Refresh** buttons.</span></span>
> 
> 

<span data-ttu-id="78aff-198">Si vous avez besoin de collaborer sur un projet, envisagez d'alterner les commandes push vers GitHub et les commandes push vers Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-198">If you need to collaborate on a project, you should consider pushing to GitHub in between pushing to Azure.</span></span>

## <a name="run-the-app-in-azure"></a><span data-ttu-id="78aff-199">Exécuter l’application dans Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="78aff-199">Run the app in Azure</span></span>
<span data-ttu-id="78aff-200">Maintenant que vous avez déployé votre application Web, exécutez l'application lorsque celle-ci est hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-200">Now that you have deployed your web app, let's run the app while hosted in Azure.</span></span> 

<span data-ttu-id="78aff-201">Cette opération peut être réalisée de deux manières :</span><span class="sxs-lookup"><span data-stu-id="78aff-201">This can be done in two ways:</span></span>

* <span data-ttu-id="78aff-202">Ouvrez un navigateur et entrez le nom de votre application Web comme suit.</span><span class="sxs-lookup"><span data-stu-id="78aff-202">Open a browser and enter the name of your web app as follows.</span></span>   
  
        http://SampleWebAppDemo.azurewebsites.net
* <span data-ttu-id="78aff-203">Dans le portail Azure, localisez le panneau de l’application web pour votre application web, puis cliquez sur **Parcourir** pour afficher votre application</span><span class="sxs-lookup"><span data-stu-id="78aff-203">In the Azure Portal, locate the web app blade for your web app, and click **Browse** to view your app</span></span> 
* <span data-ttu-id="78aff-204">dans votre navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="78aff-204">in your default browser.</span></span>

![Application Web Azure](./media/web-sites-create-web-app-using-vscode/21-azurewebapp.png)

## <a name="summary"></a><span data-ttu-id="78aff-206">Résumé</span><span class="sxs-lookup"><span data-stu-id="78aff-206">Summary</span></span>
<span data-ttu-id="78aff-207">Dans ce didacticiel, vous avez appris à créer une application Web dans VS Code et à le déployer dans Azure.</span><span class="sxs-lookup"><span data-stu-id="78aff-207">In this tutorial, you learned how to create a web app in VS Code and deploy it to Azure.</span></span> <span data-ttu-id="78aff-208">Pour plus d’informations sur VS Code, consultez l’article [Pourquoi Visual Studio Code ?](https://code.visualstudio.com/Docs/)</span><span class="sxs-lookup"><span data-stu-id="78aff-208">For more information about VS Code, see the article, [Why Visual Studio Code?](https://code.visualstudio.com/Docs/)</span></span> <span data-ttu-id="78aff-209">Pour plus d’informations sur les applications web App Service, consultez [Vue d’ensemble des applications web](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="78aff-209">For information about App Service web apps, see [Web Apps Overview](app-service-web-overview.md).</span></span> 

