---
title: aaaCreate ASP.NET web application dans Azure | Documents Microsoft
description: "Découvrez comment toorun les applications web dans Azure App Service en déployant la valeur par défaut de hello ASP.NET web app."
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
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a><span data-ttu-id="e8361-103">Création d’une application web ASP.NET dans Azure</span><span class="sxs-lookup"><span data-stu-id="e8361-103">Create an ASP.NET web app in Azure</span></span>

<span data-ttu-id="e8361-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) offre un service d’hébergement web hautement évolutif appliquant des mises à jour correctives automatiques.</span><span class="sxs-lookup"><span data-stu-id="e8361-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="e8361-105">Ce démarrage rapide montre comment toodeploy votre première application ASP.NET web application tooAzure les applications Web.</span><span class="sxs-lookup"><span data-stu-id="e8361-105">This quickstart shows how toodeploy your first ASP.NET web app tooAzure Web Apps.</span></span> <span data-ttu-id="e8361-106">Lorsque vous aurez terminé, vous disposerez d’un groupe de ressources constitué d’un plan App Service et d’une application web Azure avec une application web déployée.</span><span class="sxs-lookup"><span data-stu-id="e8361-106">When you're finished, you'll have a resource group that consists of an App Service plan and an Azure web app with a deployed web application.</span></span>

<span data-ttu-id="e8361-107">Regardez les toosee vidéo hello ce démarrage rapide en action, puis suivez hello étapes vous-même toopublish votre première application .NET sur Azure.</span><span class="sxs-lookup"><span data-stu-id="e8361-107">Watch hello video toosee this quickstart in action and then follow hello steps yourself toopublish your first .NET app on Azure.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a><span data-ttu-id="e8361-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e8361-108">Prerequisites</span></span>

<span data-ttu-id="e8361-109">toocomplete ce didacticiel :</span><span class="sxs-lookup"><span data-stu-id="e8361-109">toocomplete this tutorial:</span></span>

* <span data-ttu-id="e8361-110">Installer [Visual Studio 2017](https://www.visualstudio.com/downloads/) avec hello suivant les charges de travail :</span><span class="sxs-lookup"><span data-stu-id="e8361-110">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
    - <span data-ttu-id="e8361-111">**Développement web et ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="e8361-111">**ASP.NET and web development**</span></span>
    - <span data-ttu-id="e8361-112">**Développement Azure**</span><span class="sxs-lookup"><span data-stu-id="e8361-112">**Azure development**</span></span>

    ![Développement web et ASP.NET et Développement Azure (sous Web et cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="e8361-114">Créez une application web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e8361-114">Create an ASP.NET web app</span></span>

<span data-ttu-id="e8361-115">Dans Visual Studio, créez un projet en sélectionnant **Fichier > Nouveau > Projet**.</span><span class="sxs-lookup"><span data-stu-id="e8361-115">In Visual Studio, create a project by selecting **File > New > Project**.</span></span> 

<span data-ttu-id="e8361-116">Bonjour **nouveau projet** boîte de dialogue, sélectionnez **Visual c# > Web > ASP.NET Web Application (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e8361-116">In hello **New Project** dialog, select **Visual C# > Web > ASP.NET Web Application (.NET Framework)**.</span></span>

<span data-ttu-id="e8361-117">Nommez l’application hello _myFirstAzureWebApp_, puis sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8361-117">Name hello application _myFirstAzureWebApp_, and then select **OK**.</span></span>
   
![Boîte de dialogue Nouveau projet](./media/app-service-web-get-started-dotnet/new-project.png)

<span data-ttu-id="e8361-119">Vous pouvez déployer tout type d’ASP.NET web application tooAzure.</span><span class="sxs-lookup"><span data-stu-id="e8361-119">You can deploy any type of ASP.NET web app tooAzure.</span></span> <span data-ttu-id="e8361-120">Pour ce démarrage rapide, sélectionnez hello **MVC** modèle et assurez-vous que l’authentification est définie trop**aucune authentification**.</span><span class="sxs-lookup"><span data-stu-id="e8361-120">For this quickstart, select hello **MVC** template, and make sure authentication is set too**No Authentication**.</span></span>
      
<span data-ttu-id="e8361-121">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8361-121">Select **OK**.</span></span>

![Boîte de dialogue New ASP.NET Project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

<span data-ttu-id="e8361-123">Dans le menu de hello, sélectionnez **Déboguer > Démarrer sans débogage** toorun hello web application localement.</span><span class="sxs-lookup"><span data-stu-id="e8361-123">From hello menu, select **Debug > Start without Debugging** toorun hello web app locally.</span></span>

![Exécuter l’application localement](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a><span data-ttu-id="e8361-125">Publication tooAzure</span><span class="sxs-lookup"><span data-stu-id="e8361-125">Publish tooAzure</span></span>

<span data-ttu-id="e8361-126">Bonjour **l’Explorateur de solutions**, avec le bouton hello **myFirstAzureWebApp** de projet et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="e8361-126">In hello **Solution Explorer**, right-click hello **myFirstAzureWebApp** project and select **Publish**.</span></span>

![Publier à partir de l’Explorateur de solutions](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

<span data-ttu-id="e8361-128">Assurez-vous que **Microsoft Azure App Service** est sélectionné, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="e8361-128">Make sure that **Microsoft Azure App Service** is selected and select **Publish**.</span></span>

![Publier à partir de la page de présentation du projet](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

<span data-ttu-id="e8361-130">Cette opération ouvre hello **créer un Service application** boîte de dialogue qui vous permet de créer tous les hello ressources Azure nécessaires toorun hello web d’application ASP.NET dans Azure.</span><span class="sxs-lookup"><span data-stu-id="e8361-130">This opens hello **Create App Service** dialog, which helps you create all hello necessary Azure resources toorun hello ASP.NET web app in Azure.</span></span>

## <a name="sign-in-tooazure"></a><span data-ttu-id="e8361-131">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="e8361-131">Sign in tooAzure</span></span>

<span data-ttu-id="e8361-132">Bonjour **créer un Service application** boîte de dialogue, sélectionnez **ajouter un compte**et vous connecter tooyour abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e8361-132">In hello **Create App Service** dialog, select **Add an account**, and sign in tooyour Azure subscription.</span></span> <span data-ttu-id="e8361-133">Si vous êtes déjà connecté, compte hello select contenant hello souhaité abonnement à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="e8361-133">If you're already signed in, select hello account containing hello desired subscription from hello dropdown.</span></span>

> [!NOTE]
> <span data-ttu-id="e8361-134">Si vous êtes déjà connecté, ne sélectionnez pas encore **Créer**.</span><span class="sxs-lookup"><span data-stu-id="e8361-134">If you're already signed in, don't select **Create** yet.</span></span>
>
>
   
![Connectez-vous à tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a><span data-ttu-id="e8361-136">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="e8361-136">Create a resource group</span></span>

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

<span data-ttu-id="e8361-137">Suivant trop**groupe de ressources**, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="e8361-137">Next too**Resource Group**, select **New**.</span></span>

<span data-ttu-id="e8361-138">Groupe de ressources de nom hello **myResourceGroup** et sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8361-138">Name hello resource group **myResourceGroup** and select **OK**.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="e8361-139">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="e8361-139">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e8361-140">Suivant trop**du Plan App Service**, sélectionnez **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="e8361-140">Next too**App Service Plan**, select **New**.</span></span> 

<span data-ttu-id="e8361-141">Bonjour **configurer un Plan App Service** boîte de dialogue, utiliser les paramètres de table hello suivant capture d’écran de hello hello.</span><span class="sxs-lookup"><span data-stu-id="e8361-141">In hello **Configure App Service Plan** dialog, use hello settings in hello table following hello screenshot.</span></span>

![Créer un plan App Service](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| <span data-ttu-id="e8361-143">Paramètre</span><span class="sxs-lookup"><span data-stu-id="e8361-143">Setting</span></span> | <span data-ttu-id="e8361-144">Valeur suggérée</span><span class="sxs-lookup"><span data-stu-id="e8361-144">Suggested Value</span></span> | <span data-ttu-id="e8361-145">Description</span><span class="sxs-lookup"><span data-stu-id="e8361-145">Description</span></span> |
|-|-|-|
|<span data-ttu-id="e8361-146">Plan App Service</span><span class="sxs-lookup"><span data-stu-id="e8361-146">App Service Plan</span></span>| <span data-ttu-id="e8361-147">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e8361-147">myAppServicePlan</span></span> | <span data-ttu-id="e8361-148">Nom du plan App Service de hello.</span><span class="sxs-lookup"><span data-stu-id="e8361-148">Name of hello App Service plan.</span></span> |
| <span data-ttu-id="e8361-149">Lieu</span><span class="sxs-lookup"><span data-stu-id="e8361-149">Location</span></span> | <span data-ttu-id="e8361-150">Europe de l'Ouest</span><span class="sxs-lookup"><span data-stu-id="e8361-150">West Europe</span></span> | <span data-ttu-id="e8361-151">Bonjour centre de données où l’application hello web est hébergée.</span><span class="sxs-lookup"><span data-stu-id="e8361-151">hello datacenter where hello web app is hosted.</span></span> |
| <span data-ttu-id="e8361-152">Taille</span><span class="sxs-lookup"><span data-stu-id="e8361-152">Size</span></span> | <span data-ttu-id="e8361-153">Gratuit</span><span class="sxs-lookup"><span data-stu-id="e8361-153">Free</span></span> | <span data-ttu-id="e8361-154">Le [niveau tarifaire](https://azure.microsoft.com/pricing/details/app-service/) détermine les fonctionnalités d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="e8361-154">[Pricing tier](https://azure.microsoft.com/pricing/details/app-service/) determines hosting features.</span></span> |

<span data-ttu-id="e8361-155">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="e8361-155">Select **OK**.</span></span>

## <a name="create-and-publish-hello-web-app"></a><span data-ttu-id="e8361-156">Créer et publier l’application web hello</span><span class="sxs-lookup"><span data-stu-id="e8361-156">Create and publish hello web app</span></span>

<span data-ttu-id="e8361-157">Dans **nom de l’application Web**, tapez un nom d’application unique (les caractères valides sont `a-z`, `0-9`, et `-`), ou acceptez le nom unique est généré automatiquement par un hello.</span><span class="sxs-lookup"><span data-stu-id="e8361-157">In **Web App Name**, type a unique app name (valid characters are `a-z`, `0-9`, and `-`), or accept hello automatically generated unique name.</span></span> <span data-ttu-id="e8361-158">l’URL de l’application web hello Hello est `http://<app_name>.azurewebsites.net`, où `<app_name>` est le nom de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e8361-158">hello URL of hello web app is `http://<app_name>.azurewebsites.net`, where `<app_name>` is your web app name.</span></span>

<span data-ttu-id="e8361-159">Sélectionnez **créer** toostart création hello ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e8361-159">Select **Create** toostart creating hello Azure resources.</span></span>

![Configurer le nom de l’application web](./media/app-service-web-get-started-dotnet/web-app-name.png)

<span data-ttu-id="e8361-161">Une fois l’Assistant de hello terminé, il publie hello ASP.NET web application tooAzure, et puis lance hello application dans le navigateur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="e8361-161">Once hello wizard completes, it publishes hello ASP.NET web app tooAzure, and then launches hello app in hello default browser.</span></span>

![Application web ASP.NET publiée dans Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

<span data-ttu-id="e8361-163">nom de l’application web Hello spécifié dans hello [créer et publier étape](#create-and-publish-the-web-app) est utilisé comme hello préfixe d’URL au format de hello `http://<app_name>.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="e8361-163">hello web app name specified in hello [create and publish step](#create-and-publish-the-web-app) is used as hello URL prefix in hello format `http://<app_name>.azurewebsites.net`.</span></span>

<span data-ttu-id="e8361-164">Félicitations, votre application web ASP.NET s’exécute en temps réel dans Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="e8361-164">Congratulations, your ASP.NET web app is running live in Azure App Service.</span></span>

## <a name="update-hello-app-and-redeploy"></a><span data-ttu-id="e8361-165">Redéploiement et application hello de mise à jour</span><span class="sxs-lookup"><span data-stu-id="e8361-165">Update hello app and redeploy</span></span>

<span data-ttu-id="e8361-166">À partir de hello **l’Explorateur de solutions**, ouvrez _Views\Home\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="e8361-166">From hello **Solution Explorer**, open _Views\Home\Index.cshtml_.</span></span>

<span data-ttu-id="e8361-167">Recherche hello `<div class="jumbotron">` HTML balise haut hello et élément tout entier de hello par hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="e8361-167">Find hello `<div class="jumbotron">` HTML tag near hello top, and replace hello entire element with hello following code:</span></span>

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

<span data-ttu-id="e8361-168">tooredeploy tooAzure, avec le bouton hello **myFirstAzureWebApp** projet **l’Explorateur de solutions** et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="e8361-168">tooredeploy tooAzure, right-click hello **myFirstAzureWebApp** project in **Solution Explorer** and select **Publish**.</span></span>

<span data-ttu-id="e8361-169">Bonjour, une page de publication, sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="e8361-169">In hello publish page, select **Publish**.</span></span>

<span data-ttu-id="e8361-170">Lorsque la publication est terminée, Visual Studio lance une URL toohello du navigateur de l’application web hello.</span><span class="sxs-lookup"><span data-stu-id="e8361-170">When publishing completes, Visual Studio launches a browser toohello URL of hello web app.</span></span>

![Application web ASP.NET mise à jour dans Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="e8361-172">Gérer l’application web Azure de hello</span><span class="sxs-lookup"><span data-stu-id="e8361-172">Manage hello Azure web app</span></span>

<span data-ttu-id="e8361-173">Accédez toohello <a href="https://portal.azure.com" target="_blank">portail Azure</a> toomanage hello web app.</span><span class="sxs-lookup"><span data-stu-id="e8361-173">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app.</span></span>

<span data-ttu-id="e8361-174">Dans le menu de gauche hello, sélectionnez **des Services d’application**, puis sélectionnez le nom hello de votre application web Azure.</span><span class="sxs-lookup"><span data-stu-id="e8361-174">From hello left menu, select **App Services**, and then select hello name of your Azure web app.</span></span>

![Application de navigation du portail tooAzure web](./media/app-service-web-get-started-dotnet/access-portal.png)

<span data-ttu-id="e8361-176">Vous voyez apparaître la page Vue d’ensemble de votre application web.</span><span class="sxs-lookup"><span data-stu-id="e8361-176">You see your web app's Overview page.</span></span> <span data-ttu-id="e8361-177">Ici, vous pouvez également des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple).</span><span class="sxs-lookup"><span data-stu-id="e8361-177">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Panneau App Service sur le portail Azure](./media/app-service-web-get-started-dotnet/web-app-blade.png)

<span data-ttu-id="e8361-179">menu de gauche Hello fournit différentes pages de configuration de votre application.</span><span class="sxs-lookup"><span data-stu-id="e8361-179">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="e8361-180">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8361-180">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e8361-181">ASP.NET avec SQL Database</span><span class="sxs-lookup"><span data-stu-id="e8361-181">ASP.NET with SQL Database</span></span>](app-service-web-tutorial-dotnet-sqldatabase.md)
