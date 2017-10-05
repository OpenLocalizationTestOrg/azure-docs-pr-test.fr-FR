---
title: Utiliser le kit SDK du serveur backend .NET pour Azure Mobile Apps | Microsoft Docs
description: "Découvrez comment utiliser le Kit SDK du serveur backend .NET pour Azure App Service Mobile Apps."
keywords: "app service, azure app service, application mobile, service mobile, mise à l’échelle, évolutif, déploiement d’application, déploiement d’application azure"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 0620554f-9590-40a8-9f47-61c48c21076b
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 657fea16e47c15efd262c86d6a150a721476134a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="work-with-the-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="de5b0-104">Utiliser le kit SDK du serveur backend .NET pour Azure Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="de5b0-104">Work with the .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="de5b0-105">Cette rubrique montre comment utiliser le kit SDK du serveur backend .NET dans les scénarios Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="de5b0-105">This topic shows you how to use the .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="de5b0-106">Le Kit de développement logiciel (SDK) Azure Mobile Apps vous permet de travailler avec des clients mobiles à partir de votre application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="de5b0-106">The Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="de5b0-107">Le [Kit de développement logiciel (SDK) serveur .NET pour Azure Mobile Apps][2] est libre de droits sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="de5b0-107">The [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="de5b0-108">Le référentiel contient l’ensemble du code source, notamment la suite complète de tests unitaires du Kit de développement logiciel (SDK) serveur, et quelques exemples de projets.</span><span class="sxs-lookup"><span data-stu-id="de5b0-108">The repository contains all source code including the entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="de5b0-109">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="de5b0-109">Reference documentation</span></span>
<span data-ttu-id="de5b0-110">La documentation de référence du Kit de développement logiciel (SDK) serveur se trouve ici : [Référence .NET Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="de5b0-110">The reference documentation for the server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="de5b0-111"><a name="create-app"></a>Comment : créer un backend .NET Mobile App</span><span class="sxs-lookup"><span data-stu-id="de5b0-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="de5b0-112">Si vous démarrez un nouveau projet, vous pouvez créer une application App Service à l’aide du [portail Azure] ou de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de5b0-112">If you are starting a new project, you can create an App Service application using either the [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="de5b0-113">Vous pouvez exécuter l’application App Service en local ou publier le projet sur votre application mobile App Service hébergée sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="de5b0-113">You can run the App Service application locally or publish the project to your cloud-based App Service mobile app.</span></span>

<span data-ttu-id="de5b0-114">Si vous ajoutez des fonctionnalités mobiles à un projet existant, consultez la section [Télécharger et initialiser le Kit de développement logiciel (SDK)](#install-sdk) .</span><span class="sxs-lookup"><span data-stu-id="de5b0-114">If you are adding mobile capabilities to an existing project, see the [Download and initialize the SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-the-azure-portal"></a><span data-ttu-id="de5b0-115">Création d’un backend .NET à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="de5b0-115">Create a .NET backend using the Azure portal</span></span>
<span data-ttu-id="de5b0-116">Pour créer un backend mobile App Service, suivez le [didacticiel de démarrage rapide][3] ou procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="de5b0-116">To create an App Service mobile backend, either follow the [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="de5b0-117">Dans le panneau *Prise en main*, sous **Créer une table API**, sélectionnez **C#** en tant que **langue du backend**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-117">Back in the *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="de5b0-118">Cliquez sur **Télécharger**, extrayez les fichiers projets compressés sur votre ordinateur local, puis ouvrez la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de5b0-118">Click **Download**, extract the compressed project files to your local computer, and open the solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="de5b0-119">Créer un backend .NET à l’aide de Visual Studio 2013 et de Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="de5b0-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="de5b0-120">Pour créer un projet Azure Mobile Apps dans Visual Studio, installez le [Kit de développement logiciel (SDK) Azure pour .NET][4] (version 2.9.0 ou ultérieure).</span><span class="sxs-lookup"><span data-stu-id="de5b0-120">Install the [Azure SDK for .NET][4] (version 2.9.0 or later) to create an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="de5b0-121">Une fois que vous avez installé le SDK, créez une application ASP.NET en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="de5b0-121">Once you have installed the SDK, create an ASP.NET application using the following steps:</span></span>

1. <span data-ttu-id="de5b0-122">Ouvrez la boîte de dialogue **Nouveau projet** (dans le menu *Fichier* > **Nouveau** > **Projet...**).</span><span class="sxs-lookup"><span data-stu-id="de5b0-122">Open the **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="de5b0-123">Développez **Modèles** > **Visual C#**, puis sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="de5b0-124">Sélectionnez **Application web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="de5b0-125">Renseignez le nom du projet.</span><span class="sxs-lookup"><span data-stu-id="de5b0-125">Fill in the project name.</span></span> <span data-ttu-id="de5b0-126">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-126">Then click **OK**.</span></span>
5. <span data-ttu-id="de5b0-127">Sous *Modèles ASP.NET 4.5.2*, sélectionnez **Application mobile Azure**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="de5b0-128">Activez la case à cocher **Hôte dans le cloud** afin de créer un backend mobile dans le cloud pour la publication de ce projet.</span><span class="sxs-lookup"><span data-stu-id="de5b0-128">Check **Host in the cloud** to create a mobile backend in the cloud to which you can publish this project.</span></span>
6. <span data-ttu-id="de5b0-129">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-129">Click **OK**.</span></span>

## <span data-ttu-id="de5b0-130"><a name="install-sdk"></a>Télécharger et initialiser le Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="de5b0-130"><a name="install-sdk"></a>How to: Download and initialize the SDK</span></span>
<span data-ttu-id="de5b0-131">Le Kit de développement logiciel (SDK) est disponible sur [NuGet.org].</span><span class="sxs-lookup"><span data-stu-id="de5b0-131">The SDK is available on [NuGet.org].</span></span> <span data-ttu-id="de5b0-132">Ce package inclut les fonctionnalités de base requises pour utiliser le Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="de5b0-132">This package includes the base functionality required to get started using the SDK.</span></span> <span data-ttu-id="de5b0-133">Pour initialiser le Kit de développement logiciel (SDK), vous devez effectuer certaines actions sur l’objet **HttpConfiguration** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-133">To initialize the SDK, you need to perform actions on the **HttpConfiguration** object.</span></span>

### <a name="install-the-sdk"></a><span data-ttu-id="de5b0-134">Installer le Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="de5b0-134">Install the SDK</span></span>
<span data-ttu-id="de5b0-135">Pour installer le Kit de développement logiciel (SDK), cliquez avec le bouton droit de la souris sur le projet de serveur dans Visual Studio, sélectionnez **Gérer les packages NuGet**, recherchez le package [Microsoft.Azure.Mobile.Server], puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-135">To install the SDK, right-click on the server project in Visual Studio, select **Manage NuGet Packages**, search for the [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="de5b0-136"><a name="server-project-setup"></a> Initialiser le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="de5b0-136"><a name="server-project-setup"></a> Initialize the server project</span></span>
<span data-ttu-id="de5b0-137">Un projet de backend .NET est initialisé de la même façon que les autres projets ASP.NET, en incluant une classe de démarrage OWIN.</span><span class="sxs-lookup"><span data-stu-id="de5b0-137">A .NET backend server project is initialized similar to other ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="de5b0-138">Assurez-vous que vous avez référencé le package NuGet `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-138">Ensure that you have referenced the NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="de5b0-139">Pour ajouter cette classe dans Visual Studio, cliquez avec le bouton droit de la souris sur votre projet de serveur et sélectionnez **Ajouter** >
**Nouvel élément**, puis **Web** > **Général** > **Classe de démarrage OWIN**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-139">To add this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="de5b0-140">Une classe est générée avec l’attribut suivant :</span><span class="sxs-lookup"><span data-stu-id="de5b0-140">A class is generated with the following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="de5b0-141">Dans la méthode `Configuration()` de votre classe de démarrage OWIN, utilisez un objet **HttpConfiguration** pour configurer l’environnement Azure Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="de5b0-141">In the `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object to configure the Azure Mobile Apps environment.</span></span>
<span data-ttu-id="de5b0-142">L’exemple suivant initialise le projet de serveur sans fonctionnalités supplémentaires :</span><span class="sxs-lookup"><span data-stu-id="de5b0-142">The following example initializes the server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="de5b0-143">Pour activer des fonctionnalités spécifiques, vous devez appeler les méthodes d’extension sur l’objet **MobileAppConfiguration** avant d’appeler **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-143">To enable individual features, you must call extension methods on the **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="de5b0-144">Par exemple, le code suivant ajoute les itinéraires par défaut à tous les contrôleurs d’API avec l’attribut `[MobileAppController]` lors de l’initialisation :</span><span class="sxs-lookup"><span data-stu-id="de5b0-144">For example, the following code adds the default routes to all API controllers that have the attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="de5b0-145">Le démarrage rapide du serveur à partir du portail Azure appelle **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-145">The server quickstart from the Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="de5b0-146">Cette configuration s’apparente à celle-ci :</span><span class="sxs-lookup"><span data-stu-id="de5b0-146">This equivalent to the following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from the Home package
            .MapApiControllers()
            .AddTables(                               // from the Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from the Entity package
                )
            .AddPushNotifications()                   // from the Notifications package
            .MapLegacyCrossDomainController()         // from the CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="de5b0-147">Les méthodes d’extension utilisées sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="de5b0-147">The extension methods used are:</span></span>

* <span data-ttu-id="de5b0-148">`AddMobileAppHomeController()` fournit la page d’accueil Azure Mobile Apps par défaut.</span><span class="sxs-lookup"><span data-stu-id="de5b0-148">`AddMobileAppHomeController()` provides the default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="de5b0-149">`MapApiControllers()` fournit des fonctionnalités d’API personnalisées pour les contrôleurs WebAPI assortis de l’attribut `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-149">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with the `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="de5b0-150">`AddTables()` fournit un mappage des points de terminaison `/tables` aux contrôleurs de table.</span><span class="sxs-lookup"><span data-stu-id="de5b0-150">`AddTables()` provides a mapping of the `/tables` endpoints to table controllers.</span></span>
* <span data-ttu-id="de5b0-151">`AddTablesWithEntityFramework()` est un raccourci pour le mappage des points de terminaison `/tables` utilisant des contrôleurs basés contrôleurs basés sur Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="de5b0-151">`AddTablesWithEntityFramework()` is a short-hand for mapping the `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="de5b0-152">`AddPushNotifications()` fournit une méthode simple pour l’inscription d’appareils au service Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="de5b0-152">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="de5b0-153">`MapLegacyCrossDomainController()` fournit des en-têtes CORS standard pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="de5b0-153">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="de5b0-154">Extensions de Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="de5b0-154">SDK extensions</span></span>
<span data-ttu-id="de5b0-155">Les packages d’extension NuGet suivants fournissent différentes fonctionnalités mobiles que votre application peut utiliser.</span><span class="sxs-lookup"><span data-stu-id="de5b0-155">The following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="de5b0-156">Les extensions s’activent à l’aide de l’objet **MobileAppConfiguration** lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="de5b0-156">You enable extensions during initialization by using the **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="de5b0-157">[Microsoft.Azure.Mobile.Server.Quickstart] prend en charge la configuration de base de Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="de5b0-157">[Microsoft.Azure.Mobile.Server.Quickstart] Supports the basic Mobile Apps setup.</span></span> <span data-ttu-id="de5b0-158">S’ajoute à la configuration en appelant la méthode d’extension **UseDefaultConfiguration** pendant l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="de5b0-158">Added to the configuration by calling the **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="de5b0-159">Cette extension comprend les extensions suivantes : packages Notifications, Authentication, Entity, Tables, Cross-domain et Home.</span><span class="sxs-lookup"><span data-stu-id="de5b0-159">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="de5b0-160">Ce package est utilisé par le didacticiel de démarrage rapide de Mobile Apps disponible sur le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de5b0-160">This package is used by the Mobile Apps Quickstart available on the Azure portal.</span></span>
* <span data-ttu-id="de5b0-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implémente la page par défaut *cette application mobile est opérationnelle* pour la racine du site web.</span><span class="sxs-lookup"><span data-stu-id="de5b0-161">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements the default *this mobile app is up and running page* for the web site root.</span></span> <span data-ttu-id="de5b0-162">S’ajoute à la configuration en appelant la méthode d’extension **AddMobileAppHomeController** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-162">Add to the configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="de5b0-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) Inclut des classes pour l’utilisation des données et configure le pipeline de données.</span><span class="sxs-lookup"><span data-stu-id="de5b0-163">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up the data pipeline.</span></span> <span data-ttu-id="de5b0-164">S’ajoute à la configuration en appelant la méthode d’extension **AddTables** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-164">Add to the configuration by calling the **AddTables** extension method.</span></span>
* <span data-ttu-id="de5b0-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) permet à Entity Framework d’accéder aux données de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="de5b0-165">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables the Entity Framework to access data in the SQL Database.</span></span> <span data-ttu-id="de5b0-166">S’ajoute à la configuration en appelant la méthode d’extension **AddTablesWithEntityFramework** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-166">Add to the configuration by calling the **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="de5b0-167">[Microsoft.Azure.Mobile.Server.Authentication] Active l’authentification et configure l’intergiciel OWIN utilisé pour valider les jetons.</span><span class="sxs-lookup"><span data-stu-id="de5b0-167">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up the OWIN middleware used to validate tokens.</span></span> <span data-ttu-id="de5b0-168">S’ajoute à la configuration en appelant les méthodes d’extension **AddAppServiceAuthentication** et **IAppBuilder**.**UseAppServiceAuthentication**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-168">Add to the configuration by calling the **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="de5b0-169">[Microsoft.Azure.Mobile.Server.Notifications] active les notifications Push et définit un point de terminaison d’inscription Push.</span><span class="sxs-lookup"><span data-stu-id="de5b0-169">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="de5b0-170">S’ajoute à la configuration en appelant la méthode d’extension **AddPushNotifications** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-170">Add to the configuration by calling the **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="de5b0-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) crée un contrôleur qui fournit des données aux navigateurs web hérités à partir de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="de5b0-171">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data to legacy web browsers from your Mobile App.</span></span> <span data-ttu-id="de5b0-172">S’ajoute à la configuration en appelant la méthode d’extension **MapLegacyCrossDomainController** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-172">Add to the configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="de5b0-173">[Microsoft.Azure.Mobile.Server.Login] fournit la méthode AppServiceLoginHandler.CreateToken(), qui est une méthode statique utilisée pendant les scénarios d’authentification personnalisés.</span><span class="sxs-lookup"><span data-stu-id="de5b0-173">[Microsoft.Azure.Mobile.Server.Login] Provides the AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="de5b0-174"><a name="publish-server-project"></a>Publier le projet de serveur</span><span class="sxs-lookup"><span data-stu-id="de5b0-174"><a name="publish-server-project"></a>How to: Publish the server project</span></span>
<span data-ttu-id="de5b0-175">Cette section vous explique comment publier votre projet de backend .NET à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de5b0-175">This section shows you how to publish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="de5b0-176">Vous pouvez également déployer votre projet de backend en utilisant l’une des autres méthodes décrites dans la [Documentation sur le déploiement d’Azure App Service](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="de5b0-176">You can also deploy your backend project using Git or any of the other methods covered in the [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="de5b0-177">Avec Visual Studio, développez le projet pour restaurer des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="de5b0-177">In Visual Studio, rebuild the project to restore NuGet packages.</span></span>
2. <span data-ttu-id="de5b0-178">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-178">In Solution Explorer, right-click the project, click **Publish**.</span></span> <span data-ttu-id="de5b0-179">La première fois que vous publiez un projet, vous devez définir un profil de publication.</span><span class="sxs-lookup"><span data-stu-id="de5b0-179">The first time you publish, you need to define a publishing profile.</span></span> <span data-ttu-id="de5b0-180">Si vous disposez déjà d’un profil, vous pouvez le sélectionner et cliquer sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-180">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="de5b0-181">Si vous êtes invité à sélectionner une cible de publication, cliquez sur **Microsoft Azure App Service** > **Suivant**, puis (si nécessaire) connectez-vous avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="de5b0-181">If asked to select a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="de5b0-182">Visual Studio récupère vos paramètres de publication depuis Azure et les stocke en sécurité.</span><span class="sxs-lookup"><span data-stu-id="de5b0-182">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="de5b0-183">Choisissez votre **Abonnement**, sélectionnez **Type de ressource** dans **Affichage**, développez **Application mobile** et cliquez sur votre backend Mobile App, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-183">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="de5b0-184">Vérifiez les informations de profil de publication, puis cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-184">Verify the publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="de5b0-185">Une fois le backend Mobile App publié, une page vous indique que l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="de5b0-185">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="de5b0-186"><a name="define-table-controller"></a> Définir un contrôleur de table</span><span class="sxs-lookup"><span data-stu-id="de5b0-186"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="de5b0-187">Définissez un contrôleur de table pour exposer une table SQL aux clients mobiles.</span><span class="sxs-lookup"><span data-stu-id="de5b0-187">Define a Table Controller to expose a SQL table to mobile clients.</span></span>  <span data-ttu-id="de5b0-188">La configuration d’un contrôleur de table requiert trois étapes :</span><span class="sxs-lookup"><span data-stu-id="de5b0-188">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="de5b0-189">Créer une classe d’objet de transfert de données (DTO).</span><span class="sxs-lookup"><span data-stu-id="de5b0-189">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="de5b0-190">Configurer une référence de table dans la classe DbContext Mobile.</span><span class="sxs-lookup"><span data-stu-id="de5b0-190">Configure a table reference in the Mobile DbContext class.</span></span>
3. <span data-ttu-id="de5b0-191">Créer un contrôleur de table.</span><span class="sxs-lookup"><span data-stu-id="de5b0-191">Create a table controller.</span></span>

<span data-ttu-id="de5b0-192">Un objet de transfert de données (DTO) est un objet C# simple qui hérite de `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-192">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="de5b0-193">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="de5b0-193">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="de5b0-194">Le DTO est utilisé pour définir la table au sein de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="de5b0-194">The DTO is used to define the table within the SQL database.</span></span>  <span data-ttu-id="de5b0-195">Pour créer l’entrée de base de données, ajoutez une propriété `DbSet<>` à la classe DbContext que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="de5b0-195">To create the database entry, add a `DbSet<>` property to the DbContext you are using.</span></span>  <span data-ttu-id="de5b0-196">Dans le modèle de projet par défaut pour Azure Mobile Apps, la classe DbContext est appelée `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="de5b0-196">In the default project template for Azure Mobile Apps, the DbContext is called `Models\MobileServiceContext.cs`:</span></span>

    public class MobileServiceContext : DbContext
    {
        private const string connectionStringName = "Name=MS_TableConnectionString";

        public MobileServiceContext() : base(connectionStringName)
        {

        }

        public DbSet<TodoItem> TodoItems { get; set; }

        protected override void OnModelCreating(DbModelBuilder modelBuilder)
        {
            modelBuilder.Conventions.Add(
                new AttributeToColumnAnnotationConvention<TableColumnAttribute, string>(
                    "ServiceColumnTable", (property, attributes) => attributes.Single().ColumnType.ToString()));
        }
    }

<span data-ttu-id="de5b0-197">Si vous avez installé le Kit de développement logiciel (SDK) Azure, vous pouvez maintenant créer un modèle de contrôleur de table comme suit :</span><span class="sxs-lookup"><span data-stu-id="de5b0-197">If you have the Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="de5b0-198">Cliquez avec le bouton droit sur le dossier Contrôleurs et sélectionnez **Ajouter** > **Contrôleur...**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-198">Right-click on the Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="de5b0-199">Sélectionnez l’option **Contrôleur de tables dans les applications mobiles Azure**, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-199">Select the **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="de5b0-200">Dans la boîte de dialogue **Ajouter un contrôleur** :</span><span class="sxs-lookup"><span data-stu-id="de5b0-200">In the **Add Controller** dialog:</span></span>
   * <span data-ttu-id="de5b0-201">Dans la liste déroulante **Classe de modèle** , sélectionnez votre nouveau DTO.</span><span class="sxs-lookup"><span data-stu-id="de5b0-201">In the **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="de5b0-202">Dans la liste déroulante **DbContext** , sélectionnez la classe DbContext Mobile Service.</span><span class="sxs-lookup"><span data-stu-id="de5b0-202">In the **DbContext** dropdown, select the Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="de5b0-203">Le nom du contrôleur est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="de5b0-203">The Controller name is created for you.</span></span>
4. <span data-ttu-id="de5b0-204">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-204">Click **Add**.</span></span>

<span data-ttu-id="de5b0-205">Le projet de serveur de démarrage rapide contient un exemple de classe **TodoItemController**simple.</span><span class="sxs-lookup"><span data-stu-id="de5b0-205">The quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="de5b0-206"><a name="adjust-pagesize"></a>Comment ajuster la taille de pagination des tables</span><span class="sxs-lookup"><span data-stu-id="de5b0-206"><a name="adjust-pagesize"></a>How to: Adjust the table paging size</span></span>
<span data-ttu-id="de5b0-207">Par défaut, Azure Mobile Apps retourne 50 enregistrements par demande.</span><span class="sxs-lookup"><span data-stu-id="de5b0-207">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="de5b0-208">La pagination permet de s’assurer que le client n’occupe pas son thread d’interface utilisateur ni le serveur pendant trop longtemps et optimise son expérience utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de5b0-208">Paging ensures that the client does not tie up their UI thread nor the server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="de5b0-209">Pour modifier la taille de pagination des tables, augmentez la « taille de requête autorisée » côté serveur et la taille de page côté client. La « taille de requête autorisée » côté serveur peut être ajustée à l’aide de l’attribut `EnableQuery` :</span><span class="sxs-lookup"><span data-stu-id="de5b0-209">To change the table paging size, increase the server side "allowed query size" and the client-side page size The server side "allowed query size" is adjusted using the `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="de5b0-210">Vérifiez que la valeur de PageSize est supérieure ou égale à la taille demandée par le client.</span><span class="sxs-lookup"><span data-stu-id="de5b0-210">Ensure the PageSize is the same or larger than the size requested by the client.</span></span>  <span data-ttu-id="de5b0-211">Reportez-vous aux procédures de la documentation destinée au client pour savoir comment modifier la taille de pagination pour le client.</span><span class="sxs-lookup"><span data-stu-id="de5b0-211">Refer to the specific client HOWTO documentation for details on changing the client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="de5b0-212">Définir un contrôleur d’API personnalisé</span><span class="sxs-lookup"><span data-stu-id="de5b0-212">How to: Define a custom API controller</span></span>
<span data-ttu-id="de5b0-213">Le contrôleur d’API personnalisé fournit les fonctionnalités de base au serveur principal de votre application mobile en exposant un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="de5b0-213">The custom API controller provides the most basic functionality to your Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="de5b0-214">Vous pouvez enregistrer un contrôleur d’API mobile spécifique à l’aide de l’attribut [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="de5b0-214">You can register a mobile-specific API controller using the [MobileAppController] attribute.</span></span> <span data-ttu-id="de5b0-215">L’attribut `MobileAppController` enregistre l’itinéraire, définit le sérialiseur JSON Mobile Apps et active la [vérification de version du client](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="de5b0-215">The `MobileAppController` attribute registers the route, sets up the Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="de5b0-216">Dans Visual Studio, cliquez avec le bouton droit sur le dossier Contrôleurs, puis cliquez sur **Ajouter** > **Contrôleur**, sélectionnez **Web API 2 Controller&mdash;Empty** et cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-216">In Visual Studio, right-click the Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="de5b0-217">Spécifiez un **nom de contrôleur**, tel que `CustomController`, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-217">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="de5b0-218">Dans le nouveau fichier de classe de contrôleur, ajoutez l’instruction using suivante :</span><span class="sxs-lookup"><span data-stu-id="de5b0-218">In the new controller class file, add the following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="de5b0-219">Appliquez l’attribut **[MobileAppController]** à la définition de classe du contrôleur d’API, comme indiqué dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de5b0-219">Apply the **[MobileAppController]** attribute to the API controller class definition, as in the following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="de5b0-220">Dans le fichier App_Start/Startup.MobileApp.cs, ajoutez un appel à la méthode d’extension **MapApiControllers**, comme dans l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="de5b0-220">In App_Start/Startup.MobileApp.cs file, add a call to the **MapApiControllers** extension method, as in the following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="de5b0-221">Vous pouvez également utiliser la méthode d’extension `UseDefaultConfiguration()` au lieu de `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-221">You can also use the `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="de5b0-222">Tous les contrôleurs auxquels **MobileAppControllerAttribute** n’est pas appliqué restent accessibles aux clients, mais ils peuvent ne pas être utilisés correctement par les clients à l’aide d’un Kit de développement logiciel (SDK) client d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="de5b0-222">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="de5b0-223">Utiliser l’authentification</span><span class="sxs-lookup"><span data-stu-id="de5b0-223">How to: Work with authentication</span></span>
<span data-ttu-id="de5b0-224">Azure Mobile Apps fait appel à l’authentification/autorisation App Service pour sécuriser votre backend mobile.</span><span class="sxs-lookup"><span data-stu-id="de5b0-224">Azure Mobile Apps uses App Service Authentication / Authorization to secure your mobile backend.</span></span>  <span data-ttu-id="de5b0-225">Cette section vous explique comment effectuer les tâches suivantes liées à l’authentification dans votre projet de serveur principal .NET :</span><span class="sxs-lookup"><span data-stu-id="de5b0-225">This section shows you how to perform the following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="de5b0-226">Ajouter l’authentification à un projet de serveur</span><span class="sxs-lookup"><span data-stu-id="de5b0-226">How to: Add authentication to a server project</span></span>](#add-auth)
* [<span data-ttu-id="de5b0-227">Utiliser l’authentification personnalisée pour votre application</span><span class="sxs-lookup"><span data-stu-id="de5b0-227">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="de5b0-228">Récupérer des informations utilisateur authentifiées</span><span class="sxs-lookup"><span data-stu-id="de5b0-228">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="de5b0-229">Limiter l’accès aux données pour les utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="de5b0-229">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="de5b0-230"><a name="add-auth"></a>Ajouter l’authentification à un projet de serveur</span><span class="sxs-lookup"><span data-stu-id="de5b0-230"><a name="add-auth"></a>How to: Add authentication to a server project</span></span>
<span data-ttu-id="de5b0-231">Vous pouvez ajouter l’authentification à votre projet de serveur en étendant l’objet **MobileAppConfiguration** et en configurant l’intergiciel OWIN.</span><span class="sxs-lookup"><span data-stu-id="de5b0-231">You can add authentication to your server project by extending the **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="de5b0-232">Lorsque vous installez le package [Microsoft.Azure.Mobile.Server.Quickstart] et appelez la méthode d’extension **UseDefaultConfiguration** , vous pouvez passer directement à l’étape 3.</span><span class="sxs-lookup"><span data-stu-id="de5b0-232">When you install the [Microsoft.Azure.Mobile.Server.Quickstart] package and call the **UseDefaultConfiguration** extension method, you can skip to step 3.</span></span>

1. <span data-ttu-id="de5b0-233">Dans Visual Studio, installez le package [Microsoft.Azure.Mobile.Server.Authentication] .</span><span class="sxs-lookup"><span data-stu-id="de5b0-233">In Visual Studio, install the [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="de5b0-234">Dans le fichier de projet Startup.cs, ajoutez la ligne de code suivante au début de la méthode **Configuration** :</span><span class="sxs-lookup"><span data-stu-id="de5b0-234">In the Startup.cs project file, add the following line of code at the beginning of the **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="de5b0-235">Ce composant intergiciel (middleware) OWIN valide les jetons émis par la passerelle App Service associée.</span><span class="sxs-lookup"><span data-stu-id="de5b0-235">This OWIN middleware component validates tokens issued by the associated App Service gateway.</span></span>
3. <span data-ttu-id="de5b0-236">Ajoutez l’attribut `[Authorize]` à tous les contrôleurs ou méthodes nécessitant une authentification.</span><span class="sxs-lookup"><span data-stu-id="de5b0-236">Add the `[Authorize]` attribute to any controller or method that requires authentication.</span></span>

<span data-ttu-id="de5b0-237">Pour découvrir comment authentifier les clients auprès de votre serveur principal Mobile Apps, consultez la page [Ajouter une authentification à votre application](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="de5b0-237">To learn about how to authenticate clients to your Mobile Apps backend, see [Add authentication to your app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="de5b0-238"><a name="custom-auth"></a>Utiliser l’authentification personnalisée pour votre application</span><span class="sxs-lookup"><span data-stu-id="de5b0-238"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="de5b0-239">Si vous ne souhaitez pas utiliser l’un des fournisseurs d’authentification/d’autorisation App Service, vous pouvez implémenter votre propre système de connexion.</span><span class="sxs-lookup"><span data-stu-id="de5b0-239">If you do not wish to use one of the App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="de5b0-240">Pour faciliter la génération de jetons d’authentification, installez le package [Microsoft.Azure.Mobile.Server.Login] .</span><span class="sxs-lookup"><span data-stu-id="de5b0-240">Install the [Microsoft.Azure.Mobile.Server.Login] package to assist with authentication token generation.</span></span>  <span data-ttu-id="de5b0-241">Fournissez votre propre code pour valider les informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de5b0-241">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="de5b0-242">Par exemple, vous pouvez définir des mots de passe salés et hachés dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="de5b0-242">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="de5b0-243">Dans l’exemple ci-dessous, la méthode `isValidAssertion()` (définie ailleurs) est chargée de ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="de5b0-243">In the example below, the `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="de5b0-244">L’authentification personnalisée est exposée en créant une classe ApiController et en exposant les actions `register` et `login`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-244">The custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="de5b0-245">Le client doit utiliser une interface utilisateur personnalisée pour collecter les informations auprès de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="de5b0-245">The client should use a custom UI to collect the information from the user.</span></span>  <span data-ttu-id="de5b0-246">Les informations sont ensuite envoyées à l’API avec un appel HTTP POST standard.</span><span class="sxs-lookup"><span data-stu-id="de5b0-246">The information is then submitted to the API with a standard HTTP POST call.</span></span> <span data-ttu-id="de5b0-247">Une fois que le serveur a validé l’assertion, un jeton est émis à l’aide de la méthode `AppServiceLoginHandler.CreateToken()` .</span><span class="sxs-lookup"><span data-stu-id="de5b0-247">Once the server validates the assertion, a token is issued using the `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="de5b0-248">La classe ApiController **ne doit pas** utiliser l’attribut `[MobileAppController]`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-248">The ApiController **should not** use the `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="de5b0-249">Un exemple d’action `login` :</span><span class="sxs-lookup"><span data-stu-id="de5b0-249">An example `login` action:</span></span>

        public IHttpActionResult Post([FromBody] JObject assertion)
        {
            if (isValidAssertion(assertion)) // user-defined function, checks against a database
            {
                JwtSecurityToken token = AppServiceLoginHandler.CreateToken(new Claim[] { new Claim(JwtRegisteredClaimNames.Sub, assertion["username"]) },
                    mySigningKey,
                    myAppURL,
                    myAppURL,
                    TimeSpan.FromHours(24) );
                return Ok(new LoginResult()
                {
                    AuthenticationToken = token.RawData,
                    User = new LoginResultUser() { UserId = userName.ToString() }
                });
            }
            else // user assertion was not valid
            {
                return this.Request.CreateUnauthorizedResponse();
            }
        }

<span data-ttu-id="de5b0-250">Dans l’exemple précédent, LoginResult et LoginResultUser sont des objets sérialisables qui exposent les propriétés requises.</span><span class="sxs-lookup"><span data-stu-id="de5b0-250">In the preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="de5b0-251">Le client attend que les réponses de connexion soient renvoyées en tant qu’objets JSON de la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="de5b0-251">The client expects login responses to be returned as JSON objects of the form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="de5b0-252">La méthode `AppServiceLoginHandler.CreateToken()` inclut un paramètre *audience* et un paramètre *émetteur*.</span><span class="sxs-lookup"><span data-stu-id="de5b0-252">The `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="de5b0-253">Ces deux paramètres sont définis sur l’URL de la racine de votre application à l’aide du schéma HTTPS.</span><span class="sxs-lookup"><span data-stu-id="de5b0-253">Both of these parameters are set to the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="de5b0-254">De la même manière, vous devez définir *secretKey* en tant que clé de signature de votre application.</span><span class="sxs-lookup"><span data-stu-id="de5b0-254">Similarly you should set *secretKey* to be the value of your application's signing key.</span></span> <span data-ttu-id="de5b0-255">Ne distribuez pas la clé de signature dans un client, car elle peut être utilisée pour générer des clés et usurper l’identité d’utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="de5b0-255">Do not distribute the signing key in a client as it can be used to mint keys and impersonate users.</span></span> <span data-ttu-id="de5b0-256">Hébergé dans App Service, vous pouvez obtenir la clé de signature en faisant référence à la variable d’environnement *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="de5b0-256">You can obtain the signing key while hosted in App Service by referencing the *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="de5b0-257">Si vous en avez besoin dans un contexte de débogage local, suivez les instructions de la section [Débogage local avec authentification](#local-debug) afin de récupérer la clé et de la stocker en tant que paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="de5b0-257">If needed in a local debugging context, follow the instructions in the [Local debugging with authentication](#local-debug) section to retrieve the key and store it as an application setting.</span></span>

<span data-ttu-id="de5b0-258">Le jeton émis peut également inclure d’autres revendications et une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="de5b0-258">The issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="de5b0-259">Le jeton émis doit inclure au minimum une revendication d’objet (**sub**).</span><span class="sxs-lookup"><span data-stu-id="de5b0-259">Minimally, the issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="de5b0-260">Vous pouvez prendre en charge la méthode cliente `loginAsync()` standard en surchargeant l’itinéraire d’authentification.</span><span class="sxs-lookup"><span data-stu-id="de5b0-260">You can support the standard client `loginAsync()` method by overloading the authentication route.</span></span>  <span data-ttu-id="de5b0-261">Si le client appelle `client.loginAsync('custom');` pour se connecter, l’itinéraire doit être `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="de5b0-261">If the client calls `client.loginAsync('custom');` to log in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="de5b0-262">Vous pouvez définir l’itinéraire du contrôleur d’authentification personnalisée à l’aide de `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="de5b0-262">You can set the route for the custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="de5b0-263">L’utilisation de l’approche `loginAsync()` permet de s’assurer que le jeton d’authentification est joint à chaque appel supplémentaire au service.</span><span class="sxs-lookup"><span data-stu-id="de5b0-263">Using the `loginAsync()` approach ensures that the authentication token is attached to every subsequent call to the service.</span></span>
>
>

### <span data-ttu-id="de5b0-264"><a name="user-info"></a>Récupérer des informations utilisateur authentifiées</span><span class="sxs-lookup"><span data-stu-id="de5b0-264"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="de5b0-265">Lorsqu’un utilisateur est authentifié par App Service, vous pouvez accéder à l’ID utilisateur affecté et à d’autres informations dans votre code de serveur principal .NET.</span><span class="sxs-lookup"><span data-stu-id="de5b0-265">When a user is authenticated by App Service, you can access the assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="de5b0-266">Les informations utilisateur peuvent être utilisées pour prendre des décisions d’autorisation sur le backend.</span><span class="sxs-lookup"><span data-stu-id="de5b0-266">The user information can be used for making authorization decisions in the backend.</span></span> <span data-ttu-id="de5b0-267">Le code suivant récupère l’ID utilisateur associé à une demande :</span><span class="sxs-lookup"><span data-stu-id="de5b0-267">The following code obtains the user ID associated with a request:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="de5b0-268">Le SID est dérivé de l’ID utilisateur spécifique au fournisseur et est statique pour un utilisateur donné et un fournisseur de connexion.</span><span class="sxs-lookup"><span data-stu-id="de5b0-268">The SID is derived from the provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="de5b0-269">Le SID a la valeur null pour les jetons d’authentification non valides.</span><span class="sxs-lookup"><span data-stu-id="de5b0-269">The SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="de5b0-270">App Service vous permet également de demander des revendications spécifiques à votre fournisseur de connexion.</span><span class="sxs-lookup"><span data-stu-id="de5b0-270">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="de5b0-271">Chaque fournisseur d’identité peut fournir des informations supplémentaires à l’aide du Kit de développement logiciel (SDK) du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="de5b0-271">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="de5b0-272">Par exemple, vous pouvez utiliser l’API Graph Facebook pour les informations relatives aux amis.</span><span class="sxs-lookup"><span data-stu-id="de5b0-272">For example, you can use the Facebook Graph API for friends information.</span></span>  <span data-ttu-id="de5b0-273">Vous pouvez spécifier des revendications qui sont demandées dans le panneau du fournisseur au sein du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="de5b0-273">You can specify claims that are requested in the provider blade in the Azure portal.</span></span> <span data-ttu-id="de5b0-274">Certaines revendications nécessitent la définition de paramètres supplémentaires auprès du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="de5b0-274">Some claims require additional configuration with the identity provider.</span></span>

<span data-ttu-id="de5b0-275">Le code suivant appelle la méthode d’extension **GetAppServiceIdentityAsync** pour obtenir les informations d'identification de connexion, qui incluent l'accès au jeton nécessaire pour effectuer des requêtes par rapport à l’API Graph Facebook :</span><span class="sxs-lookup"><span data-stu-id="de5b0-275">The following code calls the **GetAppServiceIdentityAsync** extension method to get the login credentials, which include the access token needed to make requests against the Facebook Graph API:</span></span>

    // Get the credentials for the logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with the Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request the current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with the Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="de5b0-276">Ajoutez une instruction using pour `System.Security.Principal` afin de fournir la méthode d’extension **GetAppServiceIdentityAsync** .</span><span class="sxs-lookup"><span data-stu-id="de5b0-276">Add a using statement for `System.Security.Principal` to provide the **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="de5b0-277"><a name="authorize"></a>Limiter l’accès aux données pour les utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="de5b0-277"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="de5b0-278">Dans la section précédente, nous vous avons montré comment récupérer l’identificateur d’utilisateur d’un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="de5b0-278">In the previous section, we showed how to retrieve the user ID of an authenticated user.</span></span> <span data-ttu-id="de5b0-279">Vous pouvez restreindre l’accès aux données et à d’autres ressources en fonction de cette valeur.</span><span class="sxs-lookup"><span data-stu-id="de5b0-279">You can restrict access to data and other resources based on this value.</span></span> <span data-ttu-id="de5b0-280">Par exemple, l’ajout d’une colonne userId à des tables et le filtrage des résultats de la requête par l’ID utilisateur constituent un moyen simple de limiter les données renvoyées aux utilisateurs autorisés.</span><span class="sxs-lookup"><span data-stu-id="de5b0-280">For example, adding a userId column to tables and filtering the query results by the user ID is a simple way to limit returned data only to authorized users.</span></span> <span data-ttu-id="de5b0-281">Le code suivant retourne des lignes de données uniquement lorsque le SID correspond à la valeur dans la colonne UserId de la table TodoItem :</span><span class="sxs-lookup"><span data-stu-id="de5b0-281">The following code returns data rows only when the SID matches the value in the UserId column on the TodoItem table:</span></span>

    // Get the SID of the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong to the current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="de5b0-282">La méthode `Query()` renvoie un paramètre `IQueryable` qui peut être manipulé par LINQ pour gérer le filtrage.</span><span class="sxs-lookup"><span data-stu-id="de5b0-282">The `Query()` method returns an `IQueryable` that can be manipulated by LINQ to handle filtering.</span></span>

## <a name="how-to-add-push-notifications-to-a-server-project"></a><span data-ttu-id="de5b0-283">Ajouter des notifications Push à un projet de serveur</span><span class="sxs-lookup"><span data-stu-id="de5b0-283">How to: Add push notifications to a server project</span></span>
<span data-ttu-id="de5b0-284">Ajoutez des notifications Push à votre projet de serveur en étendant l’objet **MobileAppConfiguration** et en créant un client Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="de5b0-284">Add push notifications to your server project by extending the **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="de5b0-285">Dans Visual Studio, cliquez avec le bouton droit sur le projet de serveur, puis cliquez sur **Gérer les packages NuGet**, recherchez `Microsoft.Azure.Mobile.Server.Notifications` et cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-285">In Visual Studio, right-click the server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="de5b0-286">Répétez cette étape pour installer le package `Microsoft.Azure.NotificationHubs` , qui inclut la bibliothèque cliente Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="de5b0-286">Repeat this step to install the `Microsoft.Azure.NotificationHubs` package, which includes the Notification Hubs client library.</span></span>
3. <span data-ttu-id="de5b0-287">Dans le fichier App_Start/Startup.MobileApp.cs, ajoutez un appel de la méthode d’extension **AddPushNotifications()** pendant l’initialisation :</span><span class="sxs-lookup"><span data-stu-id="de5b0-287">In App_Start/Startup.MobileApp.cs, and add a call to the **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="de5b0-288">Ajoutez le code suivant pour créer un client Notification Hubs :</span><span class="sxs-lookup"><span data-stu-id="de5b0-288">Add the following code that creates a Notification Hubs client:</span></span>

        // Get the settings for the server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get the Notification Hubs credentials for the Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="de5b0-289">Vous pouvez maintenant utiliser le client Notification Hubs pour envoyer des notifications Push aux appareils inscrits.</span><span class="sxs-lookup"><span data-stu-id="de5b0-289">You can now use the Notification Hubs client to send push notifications to registered devices.</span></span> <span data-ttu-id="de5b0-290">Pour plus d’informations, consultez [Ajout de notifications Push à votre application](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="de5b0-290">For more information, see [Add push notifications to your app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="de5b0-291">Pour en savoir plus sur Notification Hubs, consultez l’article [Vue d’ensemble de Notification Hubs](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de5b0-291">To learn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="de5b0-292"><a name="tags"></a>Activer les notifications Push ciblées à l’aide de balises</span><span class="sxs-lookup"><span data-stu-id="de5b0-292"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="de5b0-293">Notification Hubs vous permet d’envoyer des notifications ciblées vers des enregistrements spécifiques à l’aide de balises.</span><span class="sxs-lookup"><span data-stu-id="de5b0-293">Notification Hubs lets you send targeted notifications to specific registrations by using tags.</span></span> <span data-ttu-id="de5b0-294">Plusieurs balises sont créées automatiquement :</span><span class="sxs-lookup"><span data-stu-id="de5b0-294">Several tags are created automatically:</span></span>

* <span data-ttu-id="de5b0-295">L’ID d’installation identifie un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="de5b0-295">The Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="de5b0-296">L’ID utilisateur, basé sur le SID authentifié, identifie un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="de5b0-296">The User Id based on the authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="de5b0-297">L’ID d’installation est accessible à partir de la propriété **installationId** sur le **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-297">The installation ID can be accessed from the **installationId** property on the **MobileServiceClient**.</span></span>  <span data-ttu-id="de5b0-298">L’exemple suivant montre comment utiliser un ID d’installation pour ajouter une balise à une installation spécifique dans Notification Hubs :</span><span class="sxs-lookup"><span data-stu-id="de5b0-298">The following example shows how to use an installation ID to add a tag to a specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="de5b0-299">Toutes les balises fournies par le client pendant l’inscription aux notifications Push sont ignorées par le backend pendant la création de l’installation.</span><span class="sxs-lookup"><span data-stu-id="de5b0-299">Any tags supplied by the client during push notification registration are ignored by the backend when creating the installation.</span></span> <span data-ttu-id="de5b0-300">Pour permettre à un client d’ajouter des balises à l’installation, vous devez créer une API personnalisée qui ajoute des balises à l’aide du modèle précédent.</span><span class="sxs-lookup"><span data-stu-id="de5b0-300">To enable a client to add tags to the installation, you must create a custom API that adds tags using the preceding pattern.</span></span>

<span data-ttu-id="de5b0-301">Pour obtenir un exemple, consultez [Client-added push notification tags][5] (Balises de notification Push ajoutées au client) dans l’exemple de démarrage rapide complet d’App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="de5b0-301">See [Client-added push notification tags][5] in the App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="de5b0-302"><a name="push-user"></a>Envoyer des notifications Push à un utilisateur authentifié</span><span class="sxs-lookup"><span data-stu-id="de5b0-302"><a name="push-user"></a>How to: Send push notifications to an authenticated user</span></span>
<span data-ttu-id="de5b0-303">Quand un utilisateur authentifié s’inscrit aux notifications Push, une balise avec l’ID d’utilisateur est automatiquement ajoutée à l’inscription.</span><span class="sxs-lookup"><span data-stu-id="de5b0-303">When an authenticated user registers for push notifications, a user ID tag is automatically added to the registration.</span></span> <span data-ttu-id="de5b0-304">Grâce à cette balise, vous pouvez envoyer des notifications Push à tous les appareils inscrits par cette personne.</span><span class="sxs-lookup"><span data-stu-id="de5b0-304">By using this tag, you can send push notifications to all devices registered by that person.</span></span> <span data-ttu-id="de5b0-305">Le code suivant permet d’obtenir le SID de l’utilisateur qui émet la demande et d’envoyer un modèle de notification Push à chaque inscription d’appareil pour cette personne :</span><span class="sxs-lookup"><span data-stu-id="de5b0-305">The following code gets the SID of user making the request and sends a template push notification to every device registration for that person:</span></span>

    // Get the current user SID and create a tag for the current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for the template with the item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification to the user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="de5b0-306">Quand vous vous inscrivez à des notifications Push à partir d’un client authentifié, assurez-vous au préalable que l’authentification est bien terminée.</span><span class="sxs-lookup"><span data-stu-id="de5b0-306">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="de5b0-307">Pour plus d’informations, consultez [Envoi de notifications Push aux utilisateurs][6] dans l’exemple de démarrage rapide complet d’App Service Mobile Apps pour le serveur principal .NET.</span><span class="sxs-lookup"><span data-stu-id="de5b0-307">For more information, see [Push to users][6] in the App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-the-net-server-sdk"></a><span data-ttu-id="de5b0-308">Déboguer et dépanner le Kit de développement logiciel (SDK) serveur .NET</span><span class="sxs-lookup"><span data-stu-id="de5b0-308">How to: Debug and troubleshoot the .NET Server SDK</span></span>
<span data-ttu-id="de5b0-309">Azure App Service fournit plusieurs techniques de débogage et de résolution des problèmes pour les applications ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="de5b0-309">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="de5b0-310">Surveiller les applications web dans Microsoft Azure App Service</span><span class="sxs-lookup"><span data-stu-id="de5b0-310">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="de5b0-311">Activer la journalisation des diagnostics pour les applications web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="de5b0-311">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="de5b0-312">Dépanner un service Azure App dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="de5b0-312">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="de5b0-313">Journalisation</span><span class="sxs-lookup"><span data-stu-id="de5b0-313">Logging</span></span>
<span data-ttu-id="de5b0-314">Vous pouvez écrire dans les journaux de diagnostics App Service à l’aide du traçage ASP.NET standard.</span><span class="sxs-lookup"><span data-stu-id="de5b0-314">You can write to App Service diagnostic logs by using the standard ASP.NET trace writing.</span></span> <span data-ttu-id="de5b0-315">Avant de pouvoir écrire dans les journaux, vous devez activer les diagnostics de votre serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="de5b0-315">Before you can write to the logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="de5b0-316">Pour activer les diagnostics et écrire dans les journaux :</span><span class="sxs-lookup"><span data-stu-id="de5b0-316">To enable diagnostics and write to the logs:</span></span>

1. <span data-ttu-id="de5b0-317">Suivez les étapes indiquées dans [Activer des diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="de5b0-317">Follow the steps in [How to enable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="de5b0-318">Ajoutez l’instruction using suivante dans votre fichier de code :</span><span class="sxs-lookup"><span data-stu-id="de5b0-318">Add the following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="de5b0-319">Créez un writer de suivi pour écrire à partir du serveur principal .NET dans les journaux de diagnostic, comme ceci :</span><span class="sxs-lookup"><span data-stu-id="de5b0-319">Create a trace writer to write from the .NET backend to the diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="de5b0-320">Publiez à nouveau votre projet de serveur et accédez au serveur principal d’application mobile pour exécuter le chemin d’accès du code avec la journalisation.</span><span class="sxs-lookup"><span data-stu-id="de5b0-320">Republish your server project, and access the Mobile App backend to execute the code path with the logging.</span></span>
5. <span data-ttu-id="de5b0-321">Téléchargez et évaluez les fichiers journaux, comme décrit dans [Télécharger des journaux](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="de5b0-321">Download and evaluate the logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="de5b0-322"><a name="local-debug"></a>Débogage local avec authentification</span><span class="sxs-lookup"><span data-stu-id="de5b0-322"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="de5b0-323">Vous pouvez exécuter localement votre application afin de tester les modifications avant de les publier dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="de5b0-323">You can run your application locally to test changes before publishing them to the cloud.</span></span> <span data-ttu-id="de5b0-324">Pour la plupart des backends Azure Mobile Apps, appuyez sur *F5* lorsque vous êtes dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de5b0-324">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="de5b0-325">Toutefois, certains points spécifiques sont à prendre en compte en lien avec l’authentification.</span><span class="sxs-lookup"><span data-stu-id="de5b0-325">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="de5b0-326">Vous devez disposer d’une application mobile basée sur le cloud avec l’authentification/l’autorisation App Service configurées, et votre client doit posséder le point de terminaison du cloud spécifié en tant qu’hôte secondaire de connexion.</span><span class="sxs-lookup"><span data-stu-id="de5b0-326">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have the cloud endpoint specified as the alternate login host.</span></span> <span data-ttu-id="de5b0-327">Consultez la documentation associée à votre plateforme cliente pour connaître la procédure appropriée.</span><span class="sxs-lookup"><span data-stu-id="de5b0-327">See the documentation for your client platform for the specific steps required.</span></span>

<span data-ttu-id="de5b0-328">Assurez-vous que [Microsoft.Azure.Mobile.Server.Authentication] est installé sur votre backend mobile.</span><span class="sxs-lookup"><span data-stu-id="de5b0-328">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="de5b0-329">Ensuite, dans la classe de démarrage OWIN de votre application, ajoutez les éléments suivants, après que `MobileAppConfiguration` a été appliquée à votre `HttpConfiguration` :</span><span class="sxs-lookup"><span data-stu-id="de5b0-329">Then, in your application's OWIN startup class, add the following, after `MobileAppConfiguration` has been applied to your `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="de5b0-330">Dans l’exemple précédent, vous devez configurer les paramètres d’application *authAudience* et *authIssuer* de votre fichier web.config sur l’URL de la racine de votre application à l’aide du schéma HTTPS.</span><span class="sxs-lookup"><span data-stu-id="de5b0-330">In the preceding example, you should configure the *authAudience* and *authIssuer* application settings within your Web.config file to each be the URL of your application root, using the HTTPS scheme.</span></span> <span data-ttu-id="de5b0-331">De la même manière, vous devez définir *authSigningKey* en tant que valeur de clé de signature de votre application.</span><span class="sxs-lookup"><span data-stu-id="de5b0-331">Similarly you should set *authSigningKey* to be the value of your application's signing key.</span></span>
<span data-ttu-id="de5b0-332">Pour obtenir la clé de signature :</span><span class="sxs-lookup"><span data-stu-id="de5b0-332">To obtain the signing key:</span></span>

1. <span data-ttu-id="de5b0-333">Accédez à votre application dans le [portail Azure]</span><span class="sxs-lookup"><span data-stu-id="de5b0-333">Navigate to your app within the [Azure portal]</span></span>
2. <span data-ttu-id="de5b0-334">Cliquez sur **Outils**, **Kudu**, **Accéder**.</span><span class="sxs-lookup"><span data-stu-id="de5b0-334">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="de5b0-335">Dans le site de gestion Kudu, cliquez sur **Environment**(Environnement).</span><span class="sxs-lookup"><span data-stu-id="de5b0-335">In the Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="de5b0-336">Recherchez la valeur de *WEBSITE\_AUTH\_SIGNING\_KEY*.</span><span class="sxs-lookup"><span data-stu-id="de5b0-336">Find the value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="de5b0-337">Utilisez la clé de signature pour le paramètre *authSigningKey* dans votre configuration d’application locale.</span><span class="sxs-lookup"><span data-stu-id="de5b0-337">Use the signing key for the *authSigningKey* parameter in your local application config.</span></span>  <span data-ttu-id="de5b0-338">Votre backend mobile est désormais équipé de manière appropriée pour valider lors d’une exécution locale les jetons obtenus par le client à partir du point de terminaison basé sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="de5b0-338">Your mobile backend is now equipped to validate tokens when running locally, which the client obtains the token from the cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
<span data-ttu-id="de5b0-339">[portail Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="de5b0-339">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="de5b0-340">[NuGet.org]: http://www.nuget.org/</span><span class="sxs-lookup"><span data-stu-id="de5b0-340">[NuGet.org]: http://www.nuget.org/</span></span>
<span data-ttu-id="de5b0-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span><span class="sxs-lookup"><span data-stu-id="de5b0-341">[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/</span></span>
<span data-ttu-id="de5b0-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span><span class="sxs-lookup"><span data-stu-id="de5b0-342">[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/</span></span>
<span data-ttu-id="de5b0-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span><span class="sxs-lookup"><span data-stu-id="de5b0-343">[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/</span></span>
<span data-ttu-id="de5b0-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span><span class="sxs-lookup"><span data-stu-id="de5b0-344">[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/</span></span>
<span data-ttu-id="de5b0-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span><span class="sxs-lookup"><span data-stu-id="de5b0-345">[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/</span></span>
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
