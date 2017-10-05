---
title: "Créer une application web ASP.NET dans Azure | Microsoft Docs"
description: "Découvrez comment exécuter des applications web dans Azure App Service en déployant l’application web ASP.NET par défaut."
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 0f0035f6fef03ddcbb500b78f3445ced5b749808
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="0c526-103">Création d’une application web ASP.NET dans Azure</span><span class="sxs-lookup"><span data-stu-id="0c526-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="0c526-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="0c526-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="0c526-105">Ce guide de démarrage rapide vous indique comment déployer votre première application web ASP.NET dans Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="0c526-105">This quickstart shows how to deploy your first ASP.NET web app to Azure Web Apps.</span></span> <span data-ttu-id="0c526-106">Lorsque vous aurez terminé, vous disposerez d’un groupe de ressources constitué d’un plan App Service et d’une application web Azure avec une application web déployée.</span><span class="sxs-lookup"><span data-stu-id="0c526-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="0c526-107">Regardez la vidéo pour voir ce démarrage rapide en action et suivez les étapes pour publier votre première application .NET sur Azure.</span><span class="sxs-lookup"><span data-stu-id="0c526-107">Watch the video to see this quickstart in action and then follow the steps yourself to publish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="0c526-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0c526-108">Prerequisites</span></span>

<span data-ttu-id="0c526-109">Pour suivre ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="0c526-109">To complete this tutorial:</span></span>

* <span data-ttu-id="0c526-110">Installez [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec les charges de travail suivantes :</span><span class="sxs-lookup"><span data-stu-id="0c526-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
    - <span data-ttu-id="0c526-111">**Développement web et ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="0c526-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="0c526-112">**Développement Azure**</span><span class="sxs-lookup"><span data-stu-id="0c526-112">**Azure development**</span></span>

    ![Développement web et ASP.NET et Développement Azure (sous Web et cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="0c526-114">Créez une application web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="0c526-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="0c526-115">Dans Visual Studio, créez un projet en sélectionnant **Fichier > Nouveau > Projet**.</span><span class="sxs-lookup"><span data-stu-id="0c526-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="0c526-116">Dans la boîte de dialogue **Nouveau projet**, sélectionnez **Visual C# > Web > Application web ASP.NET (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="0c526-116">In the **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="0c526-117">Nommez l’application _myFirstAzureWebApp_, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c526-117">Name the application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Boîte de dialogue Nouveau projet](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="0c526-119">Vous pouvez déployer n’importe quel type d’application web ASP.NET dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0c526-119">You can deploy any type of ASP.NET web app to Azure.</span></span> <span data-ttu-id="0c526-120">Pour ce guide de démarrage rapide, sélectionnez le modèle **MVC** et assurez-vous que l’authentification est définie sur **Aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="0c526-120">For this quickstart, select the **MVC** template, and make sure authentication is set to **No Authentication**.</span></span>
      
<span data-ttu-id="0c526-121">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c526-121">Select **OK**.</span></span>

![Boîte de dialogue New ASP.NET Project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="0c526-123">Dans le menu, sélectionnez **Déboguer > Exécuter sans débogage** pour exécuter l’application web localement.</span><span class="sxs-lookup"><span data-stu-id="0c526-123">From the menu, select **Debug > Start without Debugging** to run the web app locally.</span></span>

![Exécuter l’application localement](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-to-azure"></a><span data-ttu-id="0c526-125">Publication dans Azure</span><span class="sxs-lookup"><span data-stu-id="0c526-125">Publish to Azure</span></span>

<span data-ttu-id="0c526-126">Dans **l’Explorateur de solutions**, cliquez avec le bouton droit sur le projet **myFirstAzureWebApp**, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0c526-126">In the **Solution Explorer**, right-click the **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publier à partir de l’Explorateur de solutions](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="0c526-128">Assurez-vous que **Microsoft Azure App Service** est sélectionné, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0c526-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publier à partir de la page de présentation du projet](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="0c526-130">Cette opération affiche la boîte de dialogue **Créer App Service**, qui vous permet de créer toutes les ressources Azure nécessaires pour exécuter l’application web ASP.NET dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0c526-130">This opens the **Create App Service** dialog, which helps you create all the necessary Azure resources to run the ASP.NET web app in Azure.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="0c526-131">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="0c526-131">Sign in to Azure</span></span>

<span data-ttu-id="0c526-132">Dans la boîte de dialogue **Créer App Service**, sélectionnez **Ajouter un compte**, puis connectez-vous à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0c526-132">In the **Create App Service** dialog, select **Add an account**, and sign in to your Azure subscription.</span></span> <span data-ttu-id="0c526-133">Si vous êtes déjà connecté, sélectionnez le compte qui contient l’abonnement souhaité dans la liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="0c526-133">If you're already signed in, select the account containing the desired subscription from the dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="0c526-134">Si vous êtes déjà connecté, ne sélectionnez pas encore **Créer**.</span><span class="sxs-lookup"><span data-stu-id="0c526-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Connexion à Azure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="0c526-136">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="0c526-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="0c526-137">En regard de **Groupe de ressources**, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="0c526-137">Next to **Resource Group**, select **New**.</span></span>

<span data-ttu-id="0c526-138">Nommez le groupe de ressources **myResourceGroup**, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c526-138">Name the resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="0c526-139">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="0c526-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="0c526-140">En regard de **Plan App Service**, sélectionnez **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="0c526-140">Next to **App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="0c526-141">Dans la boîte de dialogue **Configurer le plan App Service**, utilisez les paramètres spécifiés dans la table sous la capture d’écran ci-après.</span><span class="sxs-lookup"><span data-stu-id="0c526-141">In the **Configure App Service Plan** dialog, use the settings in the table following the screenshot.</span></span>

![Créer un plan App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="0c526-143">Paramètre</span><span class="sxs-lookup"><span data-stu-id="0c526-143">Setting</span></span> | <span data-ttu-id="0c526-144">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="0c526-144">Suggested Value</span></span> | <span data-ttu-id="0c526-145">Description</span><span class="sxs-lookup"><span data-stu-id="0c526-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="0c526-146">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="0c526-146">App Service Plan</span></span>| <span data-ttu-id="0c526-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0c526-147">myAppServicePlan</span></span> | <span data-ttu-id="0c526-148">Nom du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="0c526-148">Name of the App Service plan.</span></span> |
| <span data-ttu-id="0c526-149">Lieu</span><span class="sxs-lookup"><span data-stu-id="0c526-149">Location</span></span> | <span data-ttu-id="0c526-150">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="0c526-150">West Europe</span></span> | <span data-ttu-id="0c526-151">Centre de données dans lequel l’application web est hébergée.</span><span class="sxs-lookup"><span data-stu-id="0c526-151">The datacenter where the web app is hosted.</span></span> |
| <span data-ttu-id="0c526-152">Taille</span><span class="sxs-lookup"><span data-stu-id="0c526-152">Size</span></span> | <span data-ttu-id="0c526-153">Gratuit</span><span class="sxs-lookup"><span data-stu-id="0c526-153">Free</span></span> | <span data-ttu-id="0c526-154">Le [niveau tarifaire](https://azure.microsoft.com/pricing/details/app-service/) détermine les fonctionnalités d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="0c526-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="0c526-155">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="0c526-155">Select **OK**.</span></span>

## <a name="create-and-publish-the-web-app"></a><span data-ttu-id="0c526-156">Créer et publier l’application web</span><span class="sxs-lookup"><span data-stu-id="0c526-156">Create and publish the web app</span></span>

<span data-ttu-id="0c526-157">Dans **Nom de l’application web**, tapez un nom d’application unique (les caractères valides sont `a-z`, `0-9` et `-`) ou acceptez le nom unique généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="0c526-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept the automatically generated unique name.</span></span> <span data-ttu-id="0c526-158">L’URL de l’application web est `http://<app_name>.azurewebsites.net`, où `<app_name>` correspond au nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="0c526-158">The URL of the web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="0c526-159">Sélectionnez **Créer** pour commencer à créer les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0c526-159">Select **Create** to start creating the Azure resources.</span></span>

![Configurer le nom de l’application web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="0c526-161">Une fois que l’Assistant a terminé, il publie l’application web ASP.NET dans Azure, puis lance l’application dans le navigateur par défaut.</span><span class="sxs-lookup"><span data-stu-id="0c526-161">Once the wizard completes, it publishes the ASP.NET web app to Azure, and then launches the app in the default browser.</span></span>

![Application web ASP.NET publiée dans Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="0c526-163">Le nom de l’application web spécifié à [l’étape de création et de publication](#create-and-publish-the-web-app) est utilisé en tant que préfixe d’URL au format `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="0c526-163">The web app name specified in the [create and publish step](#create-and-publish-the-web-app) is used as the URL prefix in the format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="0c526-164">Félicitations, votre application web ASP.NET s’exécute en temps réel dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0c526-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-the-app-and-redeploy"></a><span data-ttu-id="0c526-165">Mise à jour de l’application et redéploiement</span><span class="sxs-lookup"><span data-stu-id="0c526-165">Update the app and redeploy</span></span>

<span data-ttu-id="0c526-166">À partir de **l’Explorateur de solutions**, ouvrez _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="0c526-166">From the **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="0c526-167">Recherchez la balise HTML `<div class="jumbotron">` vers le début, puis remplacez la totalité de l’élément par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0c526-167">Find the `<div class="jumbotron">` HTML tag near the top, and replace the entire element with the following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how to deploy a .NET app to Azure App Service.</p>
</div>
```

<span data-ttu-id="0c526-168">Pour effectuer un redéploiement dans Azure, cliquez avec le bouton droit sur le projet **myFirstAzureWebApp** dans **l’Explorateur de solutions**, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0c526-168">To redeploy to Azure, right-click the **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="0c526-169">Dans la page de publication, sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="0c526-169">In the publish page, select **Publish**.</span></span>

<span data-ttu-id="0c526-170">Une fois la publication terminée, Visual Studio lance un navigateur en accédant à l’URL de l’application web.</span><span class="sxs-lookup"><span data-stu-id="0c526-170">When publishing completes, Visual Studio launches a browser to the URL of the web app.</span></span>

![Application web ASP.NET mise à jour dans Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="0c526-172">Gérer l’application web Azure</span><span class="sxs-lookup"><span data-stu-id="0c526-172">Manage the Azure web app</span></span>

<span data-ttu-id="0c526-173">Accédez au <a href="https://portal.azure.com" target="_blank">Portail Azure</a> pour gérer l’application web.</span><span class="sxs-lookup"><span data-stu-id="0c526-173">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app.</span></span>

<span data-ttu-id="0c526-174">Dans le menu de gauche, sélectionnez **App Services**, puis sélectionnez le nom de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="0c526-174">From the left menu, select **App Services**, and then select the name of your Azure web app.</span></span>

![Navigation au sein du portail pour accéder à l’application web Azure](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="0c526-176">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="0c526-176">You see your web app's Overview page.</span></span> <span data-ttu-id="0c526-177">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="0c526-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Panneau App Service sur le portail Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="0c526-179">Le menu de gauche fournit différentes pages vous permettant de configurer votre application.</span><span class="sxs-lookup"><span data-stu-id="0c526-179">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="0c526-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0c526-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0c526-181">ASP.NET avec SQL Database</span><span class="sxs-lookup"><span data-stu-id="0c526-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
