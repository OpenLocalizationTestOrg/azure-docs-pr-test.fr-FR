---
title: toowork aaaHow avec serveur principal de .NET hello SDK pour applications mobiles | Documents Microsoft
description: "Découvrez comment toowork avec hello serveur principal de .NET SDK pour applications de Azure App Service Mobile."
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
ms.openlocfilehash: 2946c5ba4424565ac764e2ce5597bf42362fcedf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-hello-net-backend-server-sdk-for-azure-mobile-apps"></a><span data-ttu-id="6fd2e-104">Travailler avec serveur principal de .NET hello Kit de développement logiciel pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="6fd2e-104">Work with hello .NET backend server SDK for Azure Mobile Apps</span></span>
[!INCLUDE [app-service-mobile-selector-server-sdk](../../includes/app-service-mobile-selector-server-sdk.md)]

<span data-ttu-id="6fd2e-105">Cette rubrique vous montre comment toouse hello .NET back-end server SDK dans les scénarios de clés Azure App Service Mobile Apps.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-105">This topic shows you how toouse hello .NET backend server SDK in key Azure App Service Mobile Apps scenarios.</span></span> <span data-ttu-id="6fd2e-106">Bonjour Azure Mobile Apps SDK vous permet de travailler avec des clients mobiles à partir de votre application ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-106">hello Azure Mobile Apps SDK helps you work with mobile clients from your ASP.NET application.</span></span>

> [!TIP]
> <span data-ttu-id="6fd2e-107">Hello [.NET server SDK pour les applications mobiles Azure] [ 2] est open source sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-107">hello [.NET server SDK for Azure Mobile Apps][2] is open source on GitHub.</span></span> <span data-ttu-id="6fd2e-108">référentiel de Hello contient tout le code source, y compris la suite de tests unitaires hello ensemble du serveur SDK et des exemples de projets.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-108">hello repository contains all source code including hello entire server SDK unit test suite and some sample projects.</span></span>
>
>

## <a name="reference-documentation"></a><span data-ttu-id="6fd2e-109">Documentation de référence</span><span class="sxs-lookup"><span data-stu-id="6fd2e-109">Reference documentation</span></span>
<span data-ttu-id="6fd2e-110">documentation de référence Hello pour le serveur hello SDK se trouve ici : [référence .NET de Azure Mobile Apps][1].</span><span class="sxs-lookup"><span data-stu-id="6fd2e-110">hello reference documentation for hello server SDK is located here: [Azure Mobile Apps .NET Reference][1].</span></span>

## <span data-ttu-id="6fd2e-111"><a name="create-app"></a>Comment : créer un serveur principal d’une application Mobile .NET</span><span class="sxs-lookup"><span data-stu-id="6fd2e-111"><a name="create-app"></a>How to: Create a .NET Mobile App backend</span></span>
<span data-ttu-id="6fd2e-112">Si vous démarrez un nouveau projet, vous pouvez créer une application de Service d’applications à l’aide soit hello [portail Azure] ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-112">If you are starting a new project, you can create an App Service application using either hello [Azure portal] or Visual Studio.</span></span> <span data-ttu-id="6fd2e-113">Vous pouvez exécuter hello application de Service de l’application localement ou publier le projet tooyour en nuage du Service d’applications mobile application hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-113">You can run hello App Service application locally or publish hello project tooyour cloud-based App Service mobile app.</span></span>

<span data-ttu-id="6fd2e-114">Si vous ajoutez un projet existant tooan fonctionnalités mobiles, consultez hello [télécharger et initialiser hello SDK](#install-sdk) section.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-114">If you are adding mobile capabilities tooan existing project, see hello [Download and initialize hello SDK](#install-sdk) section.</span></span>

### <a name="create-a-net-backend-using-hello-azure-portal"></a><span data-ttu-id="6fd2e-115">Créer un service principal de .NET à l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="6fd2e-115">Create a .NET backend using hello Azure portal</span></span>
<span data-ttu-id="6fd2e-116">toocreate un serveur principal de Service d’applications mobile, soit suivre hello [didacticiel de démarrage rapide] [ 3] ou procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-116">toocreate an App Service mobile backend, either follow hello [Quickstart tutorial][3] or follow these steps:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service-classic](../../includes/app-service-mobile-dotnet-backend-create-new-service-classic.md)]

<span data-ttu-id="6fd2e-117">Dans hello *prise en main* panneau, sous **créer une table API**, choisissez **c#** en tant que votre **principal langage**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-117">Back in hello *Get started* blade, under **Create a table API**, choose **C#** as your **Backend language**.</span></span> <span data-ttu-id="6fd2e-118">Cliquez sur **télécharger**, extraire l’ordinateur local de tooyour de fichiers de projet compressée et ouvrez la solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-118">Click **Download**, extract the compressed project files tooyour local computer, and open hello solution in Visual Studio.</span></span>

### <a name="create-a-net-backend-using-visual-studio-2013-and-visual-studio-2015"></a><span data-ttu-id="6fd2e-119">Créer un backend .NET à l’aide de Visual Studio 2013 et de Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="6fd2e-119">Create a .NET backend using Visual Studio 2013 and Visual Studio 2015</span></span>
<span data-ttu-id="6fd2e-120">Installer hello [Azure SDK pour .NET] [ 4] (version 2.9.0 ou version ultérieure) toocreate un projet Azure Mobile Apps dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-120">Install hello [Azure SDK for .NET][4] (version 2.9.0 or later) toocreate an Azure Mobile Apps project in Visual Studio.</span></span> <span data-ttu-id="6fd2e-121">Une fois que vous avez installé hello SDK, créez une application ASP.NET à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-121">Once you have installed hello SDK, create an ASP.NET application using hello following steps:</span></span>

1. <span data-ttu-id="6fd2e-122">Ouvrez hello **nouveau projet** boîte de dialogue (à partir de *fichier* > **nouveau** > **projet...** ).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-122">Open hello **New Project** dialog (from *File* > **New** > **Project...**).</span></span>
2. <span data-ttu-id="6fd2e-123">Développez **Modèles** > **Visual C#**, puis sélectionnez **Web**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-123">Expand **Templates** > **Visual C#**, and select **Web**.</span></span>
3. <span data-ttu-id="6fd2e-124">Sélectionnez **Application web ASP.NET**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-124">Select **ASP.NET Web Application**.</span></span>
4. <span data-ttu-id="6fd2e-125">Renseignez le nom du projet hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-125">Fill in hello project name.</span></span> <span data-ttu-id="6fd2e-126">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-126">Then click **OK**.</span></span>
5. <span data-ttu-id="6fd2e-127">Sous *Modèles ASP.NET 4.5.2*, sélectionnez **Application mobile Azure**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-127">Under *ASP.NET 4.5.2 Templates*, select **Azure Mobile App**.</span></span> <span data-ttu-id="6fd2e-128">Vérifiez **hôte hello cloud** toocreate un backend mobile Bonjour cloud toowhich, vous pouvez publier ce projet.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-128">Check **Host in hello cloud** toocreate a mobile backend in hello cloud toowhich you can publish this project.</span></span>
6. <span data-ttu-id="6fd2e-129">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-129">Click **OK**.</span></span>

## <span data-ttu-id="6fd2e-130"><a name="install-sdk"></a>Comment : télécharger et initialiser hello SDK</span><span class="sxs-lookup"><span data-stu-id="6fd2e-130"><a name="install-sdk"></a>How to: Download and initialize hello SDK</span></span>
<span data-ttu-id="6fd2e-131">Hello SDK est disponible sur [NuGet.org]. Ce package comprend tooget de fonctionnalités de base requises hello démarré à l’aide du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-131">hello SDK is available on [NuGet.org]. This package includes hello base functionality required tooget started using hello SDK.</span></span> <span data-ttu-id="6fd2e-132">tooinitialize hello SDK, vous devez les actions tooperform sur hello **HttpConfiguration** objet.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-132">tooinitialize hello SDK, you need tooperform actions on hello **HttpConfiguration** object.</span></span>

### <a name="install-hello-sdk"></a><span data-ttu-id="6fd2e-133">Installer hello SDK</span><span class="sxs-lookup"><span data-stu-id="6fd2e-133">Install hello SDK</span></span>
<span data-ttu-id="6fd2e-134">tooinstall hello SDK, avec le bouton droit sur le projet de serveur hello dans Visual Studio, sélectionnez **gérer les Packages NuGet**, recherchez hello [Microsoft.Azure.Mobile.Server] du package, puis cliquez sur  **Installer**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-134">tooinstall hello SDK, right-click on hello server project in Visual Studio, select **Manage NuGet Packages**, search for hello [Microsoft.Azure.Mobile.Server] package, then click **Install**.</span></span>

### <span data-ttu-id="6fd2e-135"><a name="server-project-setup"></a>Initialiser le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="6fd2e-135"><a name="server-project-setup"></a> Initialize hello server project</span></span>
<span data-ttu-id="6fd2e-136">Un projet de serveur principal .NET est initialisé similaire tooother les projets ASP.NET, en incluant une classe de démarrage OWIN.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-136">A .NET backend server project is initialized similar tooother ASP.NET projects, by including an OWIN startup class.</span></span> <span data-ttu-id="6fd2e-137">Assurez-vous que vous avez référencé package NuGet de hello `Microsoft.Owin.Host.SystemWeb`.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-137">Ensure that you have referenced hello NuGet package `Microsoft.Owin.Host.SystemWeb`.</span></span> <span data-ttu-id="6fd2e-138">tooadd cette classe dans Visual Studio, avec le bouton droit sur votre projet de serveur, puis sélectionnez **ajouter** >
**un nouvel élément**, puis **Web**  >  ** Général** > **classe de démarrage OWIN**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-138">tooadd this class in Visual Studio, right-click on your server project and select **Add** >
**New Item**, then **Web** > **General** > **OWIN Startup class**.</span></span>  <span data-ttu-id="6fd2e-139">Une classe est générée avec hello suivant attribut :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-139">A class is generated with hello following attribute:</span></span>

    [assembly: OwinStartup(typeof(YourServiceName.YourStartupClassName))]

<span data-ttu-id="6fd2e-140">Bonjour `Configuration()` méthode de votre classe de démarrage OWIN, utilisez un **HttpConfiguration** environnement d’applications mobiles Azure objet tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-140">In hello `Configuration()` method of your OWIN startup class, use an **HttpConfiguration** object tooconfigure hello Azure Mobile Apps environment.</span></span>
<span data-ttu-id="6fd2e-141">Hello, l’exemple suivant initialise le projet de serveur hello sans fonctionnalités non ajoutés :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-141">hello following example initializes hello server project with no added features:</span></span>

    // in OWIN startup class
    public void Configuration(IAppBuilder app)
    {
        HttpConfiguration config = new HttpConfiguration();

        new MobileAppConfiguration()
            // no added features
            .ApplyTo(config);

        app.UseWebApi(config);
    }

<span data-ttu-id="6fd2e-142">tooenable des fonctionnalités individuelles, vous devez appeler les méthodes d’extension sur hello **MobileAppConfiguration** objet avant d’appeler **ApplyTo**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-142">tooenable individual features, you must call extension methods on hello **MobileAppConfiguration** object before calling **ApplyTo**.</span></span> <span data-ttu-id="6fd2e-143">Par exemple, hello suivant code ajoute par défaut de hello achemine les contrôleurs tooall API qui ont l’attribut de hello `[MobileAppController]` lors de l’initialisation :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-143">For example, hello following code adds hello default routes tooall API controllers that have hello attribute `[MobileAppController]` during initialization:</span></span>

    new MobileAppConfiguration()
        .MapApiControllers()
        .ApplyTo(config);

<span data-ttu-id="6fd2e-144">démarrage rapide de serveur Hello de hello appels portails Azure **UseDefaultConfiguration()**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-144">hello server quickstart from hello Azure portal calls **UseDefaultConfiguration()**.</span></span> <span data-ttu-id="6fd2e-145">Cette toohello équivalente après l’installation :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-145">This equivalent toohello following setup:</span></span>

        new MobileAppConfiguration()
            .AddMobileAppHomeController()             // from hello Home package
            .MapApiControllers()
            .AddTables(                               // from hello Tables package
                new MobileAppTableConfiguration()
                    .MapTableControllers()
                    .AddEntityFramework()             // from hello Entity package
                )
            .AddPushNotifications()                   // from hello Notifications package
            .MapLegacyCrossDomainController()         // from hello CrossDomain package
            .ApplyTo(config);

<span data-ttu-id="6fd2e-146">méthodes d’extension Hello utilisées sont :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-146">hello extension methods used are:</span></span>

* <span data-ttu-id="6fd2e-147">`AddMobileAppHomeController()`Fournit la page d’accueil Azure Mobile Apps hello par défaut.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-147">`AddMobileAppHomeController()` provides hello default Azure Mobile Apps home page.</span></span>
* <span data-ttu-id="6fd2e-148">`MapApiControllers()`Fournit des fonctions personnalisées de l’API pour les contrôleurs WebAPI décorées avec hello `[MobileAppController]` attribut.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-148">`MapApiControllers()` provides custom API capabilities for WebAPI controllers decorated with hello `[MobileAppController]` attribute.</span></span>
* <span data-ttu-id="6fd2e-149">`AddTables()`fournit un mappage de hello `/tables` contrôleurs tootable de points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-149">`AddTables()` provides a mapping of hello `/tables` endpoints tootable controllers.</span></span>
* <span data-ttu-id="6fd2e-150">`AddTablesWithEntityFramework()`est un abrégé pour hello de mappage `/tables` contrôleurs basés sur des points de terminaison à l’aide d’Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-150">`AddTablesWithEntityFramework()` is a short-hand for mapping hello `/tables` endpoints using Entity Framework based controllers.</span></span>
* <span data-ttu-id="6fd2e-151">`AddPushNotifications()` fournit une méthode simple pour l’inscription d’appareils au service Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-151">`AddPushNotifications()` provides a simple method of registering devices for Notification Hubs.</span></span>
* <span data-ttu-id="6fd2e-152">`MapLegacyCrossDomainController()` fournit des en-têtes CORS standard pour le développement local.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-152">`MapLegacyCrossDomainController()` provides standard CORS headers for local development.</span></span>

### <a name="sdk-extensions"></a><span data-ttu-id="6fd2e-153">Extensions de Kit de développement logiciel (SDK)</span><span class="sxs-lookup"><span data-stu-id="6fd2e-153">SDK extensions</span></span>
<span data-ttu-id="6fd2e-154">Hello suivant les packages NuGet d’extension fourniture diverses fonctionnalités mobiles qui peuvent être utilisées par votre application.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-154">hello following NuGet-based extension packages provide various mobile features that can be used by your application.</span></span> <span data-ttu-id="6fd2e-155">Vous activez les extensions lors de l’initialisation à l’aide de hello **MobileAppConfiguration** objet.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-155">You enable extensions during initialization by using hello **MobileAppConfiguration** object.</span></span>

* <span data-ttu-id="6fd2e-156">[Microsoft.Azure.Mobile.Server.Quickstart] prend en charge hello le programme d’installation de base applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-156">[Microsoft.Azure.Mobile.Server.Quickstart] Supports hello basic Mobile Apps setup.</span></span> <span data-ttu-id="6fd2e-157">Configuration toohello ajouté par l’appelant hello **UseDefaultConfiguration** méthode d’extension lors de l’initialisation.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-157">Added toohello configuration by calling hello **UseDefaultConfiguration** extension method during initialization.</span></span> <span data-ttu-id="6fd2e-158">Cette extension comprend les extensions suivantes : packages Notifications, Authentication, Entity, Tables, Cross-domain et Home.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-158">This extension includes following extensions: Notifications, Authentication, Entity, Tables, Cross-domain, and Home packages.</span></span> <span data-ttu-id="6fd2e-159">Ce package est utilisé par hello démarrage rapide pour des applications mobiles disponible sur hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-159">This package is used by hello Mobile Apps Quickstart available on hello Azure portal.</span></span>
* <span data-ttu-id="6fd2e-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) implémente par défaut de hello *cette application mobile est en cours d’exécution page* pour la racine du site web hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-160">[Microsoft.Azure.Mobile.Server.Home](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Home/) Implements hello default *this mobile app is up and running page* for hello web site root.</span></span> <span data-ttu-id="6fd2e-161">Ajouter la configuration de toohello en appelant le **AddMobileAppHomeController** méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-161">Add toohello configuration by calling the **AddMobileAppHomeController** extension method.</span></span>
* <span data-ttu-id="6fd2e-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) comprend des classes pour l’utilisation des données et configuration du pipeline de données hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-162">[Microsoft.Azure.Mobile.Server.Tables](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Tables/) includes classes for working with data and sets-up hello data pipeline.</span></span> <span data-ttu-id="6fd2e-163">Ajouter des toohello configuration en appelant hello **AddTables** méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-163">Add toohello configuration by calling hello **AddTables** extension method.</span></span>
* <span data-ttu-id="6fd2e-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Active hello Entity Framework tooaccess données Bonjour de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-164">[Microsoft.Azure.Mobile.Server.Entity](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Entity/) Enables hello Entity Framework tooaccess data in hello SQL Database.</span></span> <span data-ttu-id="6fd2e-165">Ajouter des toohello configuration en appelant hello **AddTablesWithEntityFramework** méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-165">Add toohello configuration by calling hello **AddTablesWithEntityFramework** extension method.</span></span>
* <span data-ttu-id="6fd2e-166">[Microsoft.Azure.Mobile.Server.Authentication] permet l’authentification et configuration hello OWIN intergiciel (middleware) utilisé toovalidate jetons.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-166">[Microsoft.Azure.Mobile.Server.Authentication] Enables authentication and sets-up hello OWIN middleware used toovalidate tokens.</span></span> <span data-ttu-id="6fd2e-167">Ajouter des toohello configuration en appelant hello **AddAppServiceAuthentication** et **IAppBuilder**. **UseAppServiceAuthentication** les méthodes d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-167">Add toohello configuration by calling hello **AddAppServiceAuthentication** and **IAppBuilder**.**UseAppServiceAuthentication** extension methods.</span></span>
* <span data-ttu-id="6fd2e-168">[Microsoft.Azure.Mobile.Server.Notifications] active les notifications Push et définit un point de terminaison d’inscription Push.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-168">[Microsoft.Azure.Mobile.Server.Notifications] Enables push notifications and defines a push registration endpoint.</span></span> <span data-ttu-id="6fd2e-169">Ajouter des toohello configuration en appelant hello **AddPushNotifications** méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-169">Add toohello configuration by calling hello **AddPushNotifications** extension method.</span></span>
* <span data-ttu-id="6fd2e-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) crée un contrôleur qui fait Office de données toolegacy navigateurs web à partir de votre application Mobile.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-170">[Microsoft.Azure.Mobile.Server.CrossDomain](http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.CrossDomain/) Creates a controller that serves data toolegacy web browsers from your Mobile App.</span></span> <span data-ttu-id="6fd2e-171">Ajouter la configuration de toohello en appelant le **MapLegacyCrossDomainController** méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-171">Add toohello configuration by calling the **MapLegacyCrossDomainController** extension method.</span></span>
* <span data-ttu-id="6fd2e-172">[Microsoft.Azure.Mobile.Server.Login] fournit une méthode AppServiceLoginHandler.CreateToken() hello, qui est une méthode statique utilisée durant les scénarios d’authentification personnalisée.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-172">[Microsoft.Azure.Mobile.Server.Login] Provides hello AppServiceLoginHandler.CreateToken() method, which is a static method used during custom authentication scenarios.</span></span>

## <span data-ttu-id="6fd2e-173"><a name="publish-server-project"></a>Comment : publier le projet de serveur hello</span><span class="sxs-lookup"><span data-stu-id="6fd2e-173"><a name="publish-server-project"></a>How to: Publish hello server project</span></span>
<span data-ttu-id="6fd2e-174">Cette section vous montre comment toopublish votre serveur principal .NET project à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-174">This section shows you how toopublish your .NET backend project from Visual Studio.</span></span> <span data-ttu-id="6fd2e-175">Vous pouvez également déployer votre projet de service principal à l’aide de Git ou des hello autres méthodes présentées dans hello [documentation sur le déploiement du Service d’applications Azure](../app-service-web/web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-175">You can also deploy your backend project using Git or any of hello other methods covered in hello [Azure App Service deployment documentation](../app-service-web/web-sites-deploy.md).</span></span>

1. <span data-ttu-id="6fd2e-176">Dans Visual Studio, régénérez les packages NuGet de hello projet toorestore.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-176">In Visual Studio, rebuild hello project toorestore NuGet packages.</span></span>
2. <span data-ttu-id="6fd2e-177">Dans l’Explorateur de solutions, projets de hello avec le bouton droit, cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-177">In Solution Explorer, right-click hello project, click **Publish**.</span></span> <span data-ttu-id="6fd2e-178">Hello première fois que vous publiez, vous devez toodefine un profil de publication.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-178">hello first time you publish, you need toodefine a publishing profile.</span></span> <span data-ttu-id="6fd2e-179">Si vous disposez déjà d’un profil, vous pouvez le sélectionner et cliquer sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-179">When you already have a profile defined, you can select it and click **Publish**.</span></span>
3. <span data-ttu-id="6fd2e-180">Si vous êtes invité tooselect une cible de publication, cliquez sur **Microsoft Azure App Service** > **suivant**, puis (si nécessaire) connectez-vous avec vos informations d’identification Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-180">If asked tooselect a publish target, click **Microsoft Azure App Service** > **Next**, then (if needed) sign-in with your Azure credentials.</span></span>
   <span data-ttu-id="6fd2e-181">Visual Studio récupère vos paramètres de publication depuis Azure et les stocke en sécurité.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-181">Visual Studio downloads and securely stores your publish settings directly from Azure.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-1.png)
4. <span data-ttu-id="6fd2e-182">Choisissez votre **Abonnement**, sélectionnez **Type de ressource** dans **Affichage**, développez **Application mobile** et cliquez sur votre backend Mobile App, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-182">Choose your **Subscription**, select **Resource Type** from **View**, expand **Mobile App**, and click your Mobile App backend, then click **OK**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-2.png)
5. <span data-ttu-id="6fd2e-183">Vérifiez que hello publier des informations de profil et cliquez sur **publier**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-183">Verify hello publish profile information and click **Publish**.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-wizard-3.png)

    <span data-ttu-id="6fd2e-184">Une fois le backend Mobile App publié, une page vous indique que l’opération a réussi.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-184">When your Mobile App backend has published successfully, you see a landing page indicating success.</span></span>

    ![](./media/app-service-mobile-dotnet-backend-how-to-use-server-sdk/publish-success.png)

## <span data-ttu-id="6fd2e-185"><a name="define-table-controller"></a> Définir un contrôleur de table</span><span class="sxs-lookup"><span data-stu-id="6fd2e-185"><a name="define-table-controller"></a> How to: Define a table controller</span></span>
<span data-ttu-id="6fd2e-186">Définir un tooexpose de contrôleur de la Table des clients de toomobile une table SQL.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-186">Define a Table Controller tooexpose a SQL table toomobile clients.</span></span>  <span data-ttu-id="6fd2e-187">La configuration d’un contrôleur de table requiert trois étapes :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-187">Configuring a Table Controller requires three steps:</span></span>

1. <span data-ttu-id="6fd2e-188">Créer une classe d’objet de transfert de données (DTO).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-188">Create a Data Transfer Object (DTO) class.</span></span>
2. <span data-ttu-id="6fd2e-189">Configurez une référence de table Bonjour classe Mobile DbContext.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-189">Configure a table reference in hello Mobile DbContext class.</span></span>
3. <span data-ttu-id="6fd2e-190">Créer un contrôleur de table.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-190">Create a table controller.</span></span>

<span data-ttu-id="6fd2e-191">Un objet de transfert de données (DTO) est un objet C# simple qui hérite de `EntityData`.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-191">A Data Transfer Object (DTO) is a plain C# object that inherits from `EntityData`.</span></span>  <span data-ttu-id="6fd2e-192">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-192">For example:</span></span>

    public class TodoItem : EntityData
    {
        public string Text { get; set; }
        public bool Complete {get; set;}
    }

<span data-ttu-id="6fd2e-193">Hello DTO est la table de hello toodefine utilisés au sein de la base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-193">hello DTO is used toodefine hello table within hello SQL database.</span></span>  <span data-ttu-id="6fd2e-194">toocreate hello de base de données d’entrée, ajoutez un `DbSet<>` propriété Hello DbContext que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-194">toocreate hello database entry, add a `DbSet<>` property to hello DbContext you are using.</span></span>  <span data-ttu-id="6fd2e-195">Dans le modèle de projet hello par défaut pour les applications mobiles Azure, hello DbContext est appelée `Models\MobileServiceContext.cs`:</span><span class="sxs-lookup"><span data-stu-id="6fd2e-195">In hello default project template for Azure Mobile Apps, hello DbContext is called `Models\MobileServiceContext.cs`:</span></span>

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

<span data-ttu-id="6fd2e-196">Si vous avez hello Qu'azure SDK est installé, vous pouvez maintenant créer un contrôleur de table de modèle comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-196">If you have hello Azure SDK installed, you can now create a template table controller as follows:</span></span>

1. <span data-ttu-id="6fd2e-197">Avec le bouton droit sur le dossier de contrôleurs hello et sélectionnez **ajouter** > **contrôleur...** .</span><span class="sxs-lookup"><span data-stu-id="6fd2e-197">Right-click on hello Controllers folder and select **Add** > **Controller...**.</span></span>
2. <span data-ttu-id="6fd2e-198">Sélectionnez hello **contrôleur de Table Azure Mobile Apps** option, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-198">Select hello **Azure Mobile Apps Table Controller** option, then click **Add**.</span></span>
3. <span data-ttu-id="6fd2e-199">Bonjour **ajouter un contrôleur** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-199">In hello **Add Controller** dialog:</span></span>
   * <span data-ttu-id="6fd2e-200">Bonjour **classe de modèle** liste déroulante, sélectionnez votre nouvelle DTO.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-200">In hello **Model class** dropdown, select your new DTO.</span></span>
   * <span data-ttu-id="6fd2e-201">Bonjour **DbContext** liste déroulante, la classe DbContext du Service Mobile de hello select.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-201">In hello **DbContext** dropdown, select hello Mobile Service DbContext class.</span></span>
   * <span data-ttu-id="6fd2e-202">nom du contrôleur Hello est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-202">hello Controller name is created for you.</span></span>
4. <span data-ttu-id="6fd2e-203">Cliquez sur **Add**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-203">Click **Add**.</span></span>

<span data-ttu-id="6fd2e-204">projet de serveur Hello quickstart contient un exemple d’un simple **TodoItemController**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-204">hello quickstart server project contains an example for a simple **TodoItemController**.</span></span>

### <span data-ttu-id="6fd2e-205"><a name="adjust-pagesize"></a>Comment : redimensionner la pagination hello table</span><span class="sxs-lookup"><span data-stu-id="6fd2e-205"><a name="adjust-pagesize"></a>How to: Adjust hello table paging size</span></span>
<span data-ttu-id="6fd2e-206">Par défaut, Azure Mobile Apps retourne 50 enregistrements par demande.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-206">By default, Azure Mobile Apps returns 50 records per request.</span></span>  <span data-ttu-id="6fd2e-207">La pagination garantit que le client hello n’occupe pas leur serveur de l’interface utilisateur thread ni hello trop longtemps, garantissant une expérience utilisateur optimale.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-207">Paging ensures that hello client does not tie up their UI thread nor hello server for too long, ensuring a good user experience.</span></span> <span data-ttu-id="6fd2e-208">taille de la pagination du tableau toochange hello, augmentation hello SSI « taille de la requête autorisé » et hello SSI de page côté client de hello de taille « taille de la requête d’autorisé » est ajustée à l’aide de hello `EnableQuery` attribut :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-208">toochange hello table paging size, increase hello server side "allowed query size" and hello client-side page size hello server side "allowed query size" is adjusted using hello `EnableQuery` attribute:</span></span>

    [EnableQuery(PageSize = 500)]

<span data-ttu-id="6fd2e-209">Vérifiez que hello PageSize est hello égale ou supérieure à la taille de hello demandée par le client de hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-209">Ensure hello PageSize is hello same or larger than hello size requested by hello client.</span></span>  <span data-ttu-id="6fd2e-210">Pour plus d’informations sur la modification de taille de page hello client, consultez la documentation de faire du client spécifique toohello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-210">Refer toohello specific client HOWTO documentation for details on changing hello client page size.</span></span>

## <a name="how-to-define-a-custom-api-controller"></a><span data-ttu-id="6fd2e-211">Définir un contrôleur d’API personnalisé</span><span class="sxs-lookup"><span data-stu-id="6fd2e-211">How to: Define a custom API controller</span></span>
<span data-ttu-id="6fd2e-212">contrôleur d’API personnalisée Hello fournit le principal de l’application Mobile hello plus simple fonctionnalité tooyour en exposant un point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-212">hello custom API controller provides hello most basic functionality tooyour Mobile App backend by exposing an endpoint.</span></span> <span data-ttu-id="6fd2e-213">Vous pouvez enregistrer un contrôleur d’API mobile spécifique à l’aide des attributs de hello [MobileAppController].</span><span class="sxs-lookup"><span data-stu-id="6fd2e-213">You can register a mobile-specific API controller using hello [MobileAppController] attribute.</span></span> <span data-ttu-id="6fd2e-214">Hello `MobileAppController` attribut enregistre hello itinéraire, configure le sérialiseur JSON des applications mobiles de hello et Active [la vérification de la version client](app-service-mobile-client-and-server-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-214">hello `MobileAppController` attribute registers hello route, sets up hello Mobile Apps JSON serializer, and turns on [client version checking](app-service-mobile-client-and-server-versioning.md).</span></span>

1. <span data-ttu-id="6fd2e-215">Dans Visual Studio, le dossier de contrôleurs hello avec le bouton droit, puis cliquez sur **ajouter** > **contrôleur**, sélectionnez **Web API 2 contrôleur&mdash;vide** et Cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-215">In Visual Studio, right-click hello Controllers folder, then click **Add** > **Controller**, select **Web API 2 Controller&mdash;Empty** and click **Add**.</span></span>
2. <span data-ttu-id="6fd2e-216">Spécifiez un **nom de contrôleur**, tel que `CustomController`, puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-216">Supply a **Controller name**, such as `CustomController`, and click **Add**.</span></span>
3. <span data-ttu-id="6fd2e-217">Dans le nouveau fichier de classe de contrôleur hello, ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-217">In hello new controller class file, add hello following using statement:</span></span>

        using Microsoft.Azure.Mobile.Server.Config;
4. <span data-ttu-id="6fd2e-218">Appliquer hello **[MobileAppController]** attribut de définition de classe de contrôleur toohello API, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-218">Apply hello **[MobileAppController]** attribute toohello API controller class definition, as in hello following example:</span></span>

        [MobileAppController]
        public class CustomController : ApiController
        {
              //...
        }
5. <span data-ttu-id="6fd2e-219">Dans le fichier de App_Start/Startup.MobileApp.cs, ajouter un appel toohello **MapApiControllers** méthode d’extension, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-219">In App_Start/Startup.MobileApp.cs file, add a call toohello **MapApiControllers** extension method, as in hello following example:</span></span>

        new MobileAppConfiguration()
            .MapApiControllers()
            .ApplyTo(config);

<span data-ttu-id="6fd2e-220">Vous pouvez également utiliser hello `UseDefaultConfiguration()` méthode d’extension à la place de `MapApiControllers()`.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-220">You can also use hello `UseDefaultConfiguration()` extension method instead of `MapApiControllers()`.</span></span> <span data-ttu-id="6fd2e-221">Tous les contrôleurs auxquels **MobileAppControllerAttribute** n’est pas appliqué restent accessibles aux clients, mais ils peuvent ne pas être utilisés correctement par les clients à l’aide d’un Kit de développement logiciel (SDK) client d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-221">Any controller that does not have **MobileAppControllerAttribute** applied can still be accessed by clients, but it may not be correctly consumed by clients using any Mobile App client SDK.</span></span>

## <a name="how-to-work-with-authentication"></a><span data-ttu-id="6fd2e-222">Utiliser l’authentification</span><span class="sxs-lookup"><span data-stu-id="6fd2e-222">How to: Work with authentication</span></span>
<span data-ttu-id="6fd2e-223">Les applications mobiles Azure utilise l’authentification du Service application / d’autorisation toosecure votre serveur principal mobile.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-223">Azure Mobile Apps uses App Service Authentication / Authorization toosecure your mobile backend.</span></span>  <span data-ttu-id="6fd2e-224">Cette section vous montre comment hello tooperform liés à l’authentification des tâches dans votre projet de serveur principal .NET suivantes :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-224">This section shows you how tooperform hello following authentication-related tasks in your .NET backend server project:</span></span>

* [<span data-ttu-id="6fd2e-225">Comment : ajouter un projet de serveur d’authentification tooa</span><span class="sxs-lookup"><span data-stu-id="6fd2e-225">How to: Add authentication tooa server project</span></span>](#add-auth)
* [<span data-ttu-id="6fd2e-226">Utiliser l’authentification personnalisée pour votre application</span><span class="sxs-lookup"><span data-stu-id="6fd2e-226">How to: Use custom authentication for your application</span></span>](#custom-auth)
* [<span data-ttu-id="6fd2e-227">Récupérer des informations utilisateur authentifiées</span><span class="sxs-lookup"><span data-stu-id="6fd2e-227">How to: Retrieve authenticated user information</span></span>](#user-info)
* [<span data-ttu-id="6fd2e-228">Limiter l’accès aux données pour les utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="6fd2e-228">How to: Restrict data access for authorized users</span></span>](#authorize)

### <span data-ttu-id="6fd2e-229"><a name="add-auth"></a>Comment : ajouter un projet de serveur d’authentification tooa</span><span class="sxs-lookup"><span data-stu-id="6fd2e-229"><a name="add-auth"></a>How to: Add authentication tooa server project</span></span>
<span data-ttu-id="6fd2e-230">Vous pouvez ajouter le projet de serveur d’authentification tooyour en étendant hello **MobileAppConfiguration** objet et la configuration d’intergiciel (middleware) OWIN.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-230">You can add authentication tooyour server project by extending hello **MobileAppConfiguration** object and configuring OWIN middleware.</span></span> <span data-ttu-id="6fd2e-231">Lorsque vous installez hello [Microsoft.Azure.Mobile.Server.Quickstart] hello package et appelez **UseDefaultConfiguration** méthode d’extension, vous pouvez ignorer toostep 3.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-231">When you install hello [Microsoft.Azure.Mobile.Server.Quickstart] package and call hello **UseDefaultConfiguration** extension method, you can skip toostep 3.</span></span>

1. <span data-ttu-id="6fd2e-232">Dans Visual Studio, installez hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-232">In Visual Studio, install hello [Microsoft.Azure.Mobile.Server.Authentication] package.</span></span>
2. <span data-ttu-id="6fd2e-233">Dans le fichier de projet Startup.cs hello, ajouter hello suivant la ligne de code au début de hello Hello **Configuration** méthode :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-233">In hello Startup.cs project file, add hello following line of code at hello beginning of hello **Configuration** method:</span></span>

        app.UseAppServiceAuthentication(config);

    <span data-ttu-id="6fd2e-234">Ce composant d’intergiciel (middleware) OWIN valide les jetons émis par la passerelle de Service de l’application hello associé.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-234">This OWIN middleware component validates tokens issued by hello associated App Service gateway.</span></span>
3. <span data-ttu-id="6fd2e-235">Ajouter hello `[Authorize]` contrôleur de tooany d’attribut ou une méthode qui requiert une authentification.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-235">Add hello `[Authorize]` attribute tooany controller or method that requires authentication.</span></span>

<span data-ttu-id="6fd2e-236">toolearn comment tooauthenticate clients tooyour principal des applications mobiles, consultez [ajouter l’authentification tooyour application](app-service-mobile-ios-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-236">toolearn about how tooauthenticate clients tooyour Mobile Apps backend, see [Add authentication tooyour app](app-service-mobile-ios-get-started-users.md).</span></span>

### <span data-ttu-id="6fd2e-237"><a name="custom-auth"></a>Utiliser l’authentification personnalisée pour votre application</span><span class="sxs-lookup"><span data-stu-id="6fd2e-237"><a name="custom-auth"></a>How to: Use custom authentication for your application</span></span>
<span data-ttu-id="6fd2e-238">Si vous ne souhaitez pas toouse un des fournisseurs d’authentification/autorisation du Service application hello, vous pouvez implémenter votre propre système de connexion.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-238">If you do not wish toouse one of hello App Service Authentication/Authorization providers, you can implement your own login system.</span></span> <span data-ttu-id="6fd2e-239">Installer hello [Microsoft.Azure.Mobile.Server.Login] tooassist de génération de jetons d’authentification du package.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-239">Install hello [Microsoft.Azure.Mobile.Server.Login] package tooassist with authentication token generation.</span></span>  <span data-ttu-id="6fd2e-240">Fournissez votre propre code pour valider les informations d’identification utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-240">Provide your own code for validating user credentials.</span></span> <span data-ttu-id="6fd2e-241">Par exemple, vous pouvez définir des mots de passe salés et hachés dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-241">For example, you might check against salted and hashed passwords in a database.</span></span> <span data-ttu-id="6fd2e-242">Dans l’exemple hello ci-dessous, hello `isValidAssertion()` (méthode) (définie ailleurs) est chargé de ces vérifications.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-242">In hello example below, hello `isValidAssertion()` method (defined elsewhere) is responsible for these checks.</span></span>

<span data-ttu-id="6fd2e-243">authentification personnalisée de Hello est exposée par un ApiController de créer et d’exposer `register` et `login` actions.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-243">hello custom authentication is exposed by creating an ApiController and exposing `register` and `login` actions.</span></span> <span data-ttu-id="6fd2e-244">client de Hello doit utiliser une interface utilisateur toocollect hello des informations personnalisées à partir de l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-244">hello client should use a custom UI toocollect hello information from hello user.</span></span>  <span data-ttu-id="6fd2e-245">informations de Hello sont soumis toohello API avec un HTTP POST standard l’appeler.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-245">hello information is then submitted toohello API with a standard HTTP POST call.</span></span> <span data-ttu-id="6fd2e-246">Une fois que le serveur de hello valide l’assertion de hello, un jeton est émis à l’aide de hello `AppServiceLoginHandler.CreateToken()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-246">Once hello server validates hello assertion, a token is issued using hello `AppServiceLoginHandler.CreateToken()` method.</span></span>  <span data-ttu-id="6fd2e-247">Hello ApiController **ne doivent pas** utiliser hello `[MobileAppController]` attribut.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-247">hello ApiController **should not** use hello `[MobileAppController]` attribute.</span></span>

<span data-ttu-id="6fd2e-248">Un exemple d’action `login` :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-248">An example `login` action:</span></span>

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

<span data-ttu-id="6fd2e-249">Bonjour précédent exemple, LoginResult et LoginResultUser sont des objets sérialisables qui exposent des propriétés requises.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-249">In hello preceding example, LoginResult and LoginResultUser are serializable objects exposing required properties.</span></span> <span data-ttu-id="6fd2e-250">client de Hello attend toobe de réponses de connexion en tant qu’objets JSON sous forme de hello :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-250">hello client expects login responses toobe returned as JSON objects of hello form:</span></span>

        {
            "authenticationToken": "<token>",
            "user": {
                "userId": "<userId>"
            }
        }

<span data-ttu-id="6fd2e-251">Hello `AppServiceLoginHandler.CreateToken()` méthode inclut un *public* et un *émetteur* paramètre.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-251">hello `AppServiceLoginHandler.CreateToken()` method includes an *audience* and an *issuer* parameter.</span></span> <span data-ttu-id="6fd2e-252">Ces deux paramètres sont définies toohello des URL de la racine de votre application, à l’aide du schéma HTTPS de hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-252">Both of these parameters are set toohello URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="6fd2e-253">De même, vous devez définir *secretKey* clé de signature de la valeur de hello toobe de votre application.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-253">Similarly you should set *secretKey* toobe hello value of your application's signing key.</span></span> <span data-ttu-id="6fd2e-254">Ne distribuez pas hello signer la clé dans un client peut être utilisé toomint clés et emprunter l’identité des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-254">Do not distribute hello signing key in a client as it can be used toomint keys and impersonate users.</span></span> <span data-ttu-id="6fd2e-255">Vous pouvez obtenir hello tandis que hébergée dans le Service d’applications en référençant hello de clé de signature *site Web\_AUTH\_signature\_clé* variable d’environnement.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-255">You can obtain hello signing key while hosted in App Service by referencing hello *WEBSITE\_AUTH\_SIGNING\_KEY* environment variable.</span></span> <span data-ttu-id="6fd2e-256">Si nécessaire dans un contexte de débogage local, suivez les instructions de hello Bonjour [débogage Local avec l’authentification](#local-debug) section clé de hello tooretrieve et stocker en tant que paramètre d’application.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-256">If needed in a local debugging context, follow hello instructions in hello [Local debugging with authentication](#local-debug) section tooretrieve hello key and store it as an application setting.</span></span>

<span data-ttu-id="6fd2e-257">jeton de Hello émis peut-être également inclure les autres revendications et une date d’expiration.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-257">hello issued token may also include other claims and an expiry date.</span></span>  <span data-ttu-id="6fd2e-258">Au minimum, jeton de hello émis doit inclure un sujet (**sub**) de revendication.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-258">Minimally, hello issued token must include a subject (**sub**) claim.</span></span>

<span data-ttu-id="6fd2e-259">Vous pouvez prendre en charge client standard de hello `loginAsync()` méthode en surchargeant l’itinéraire d’authentification hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-259">You can support hello standard client `loginAsync()` method by overloading hello authentication route.</span></span>  <span data-ttu-id="6fd2e-260">Si hello client appelle `client.loginAsync('custom');` toolog dans, l’itinéraire doit être `/.auth/login/custom`.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-260">If hello client calls `client.loginAsync('custom');` toolog in, your route must be `/.auth/login/custom`.</span></span>  <span data-ttu-id="6fd2e-261">Vous pouvez définir des itinéraires hello pour hello de contrôleur d’authentification personnalisée à l’aide `MapHttpRoute()`:</span><span class="sxs-lookup"><span data-stu-id="6fd2e-261">You can set hello route for hello custom authentication controller using `MapHttpRoute()`:</span></span>

    config.Routes.MapHttpRoute("custom", ".auth/login/custom", new { controller = "CustomAuth" });

> [!TIP]
> <span data-ttu-id="6fd2e-262">À l’aide de hello `loginAsync()` approche garantit que ce jeton d’authentification hello est attaché tooevery appeler toohello service.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-262">Using hello `loginAsync()` approach ensures that hello authentication token is attached tooevery subsequent call toohello service.</span></span>
>
>

### <span data-ttu-id="6fd2e-263"><a name="user-info"></a>Récupérer des informations utilisateur authentifiées</span><span class="sxs-lookup"><span data-stu-id="6fd2e-263"><a name="user-info"></a>How to: Retrieve authenticated user information</span></span>
<span data-ttu-id="6fd2e-264">Lorsqu’un utilisateur est authentifié par le Service d’applications, vous pouvez accéder à hello affecté des ID d’utilisateur et d’autres informations dans votre code de serveur principal .NET.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-264">When a user is authenticated by App Service, you can access hello assigned user ID and other information in your .NET backend code.</span></span> <span data-ttu-id="6fd2e-265">informations d’utilisateur de Hello peuvent être utilisées pour prendre des décisions d’autorisation dans le service principal hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-265">hello user information can be used for making authorization decisions in hello backend.</span></span> <span data-ttu-id="6fd2e-266">Hello de code suivant obtient hello ID d’utilisateur associé à une demande :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-266">hello following code obtains hello user ID associated with a request:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

<span data-ttu-id="6fd2e-267">Hello SID est dérivé de l’ID d’utilisateur spécifique au fournisseur hello et est statique pour un utilisateur donné et le fournisseur de connexion.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-267">hello SID is derived from hello provider-specific user ID and is static for a given user and login provider.</span></span>  <span data-ttu-id="6fd2e-268">Hello SID est null pour les jetons d’authentification non valide.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-268">hello SID is null for invalid authentication tokens.</span></span>

<span data-ttu-id="6fd2e-269">App Service vous permet également de demander des revendications spécifiques à votre fournisseur de connexion.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-269">App Service also lets you request specific claims from your login provider.</span></span> <span data-ttu-id="6fd2e-270">Chaque fournisseur d’identité peut fournir des informations supplémentaires à l’aide du Kit de développement logiciel (SDK) du fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-270">Each identity provider can provide more information using the identity provider SDK.</span></span>  <span data-ttu-id="6fd2e-271">Par exemple, vous pouvez utiliser hello API Graph Facebook pour les informations de vos amis.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-271">For example, you can use hello Facebook Graph API for friends information.</span></span>  <span data-ttu-id="6fd2e-272">Vous pouvez spécifier les revendications qui sont demandées dans le panneau de fournisseur hello Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-272">You can specify claims that are requested in hello provider blade in hello Azure portal.</span></span> <span data-ttu-id="6fd2e-273">Certaines demandes nécessitent une configuration supplémentaire avec un fournisseur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-273">Some claims require additional configuration with hello identity provider.</span></span>

<span data-ttu-id="6fd2e-274">hello d’appels de code suivant de Hello **GetAppServiceIdentityAsync** extension méthode tooget hello informations d’identification, notamment les demandes de jeton toomake nécessaires d’accès hello contre hello API Graph Facebook :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-274">hello following code calls hello **GetAppServiceIdentityAsync** extension method tooget hello login credentials, which include hello access token needed toomake requests against hello Facebook Graph API:</span></span>

    // Get hello credentials for hello logged-in user.
    var credentials =
        await this.User
        .GetAppServiceIdentityAsync<FacebookCredentials>(this.Request);

    if (credentials.Provider == "Facebook")
    {
        // Create a query string with hello Facebook access token.
        var fbRequestUrl = "https://graph.facebook.com/me/feed?access_token="
            + credentials.AccessToken;

        // Create an HttpClient request.
        var client = new System.Net.Http.HttpClient();

        // Request hello current user info from Facebook.
        var resp = await client.GetAsync(fbRequestUrl);
        resp.EnsureSuccessStatusCode();

        // Do something here with hello Facebook user information.
        var fbInfo = await resp.Content.ReadAsStringAsync();
    }

<span data-ttu-id="6fd2e-275">Ajouter un à l’aide de l’instruction pour `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** méthode d’extension.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-275">Add a using statement for `System.Security.Principal` tooprovide hello **GetAppServiceIdentityAsync** extension method.</span></span>

### <span data-ttu-id="6fd2e-276"><a name="authorize"></a>Limiter l’accès aux données pour les utilisateurs autorisés</span><span class="sxs-lookup"><span data-stu-id="6fd2e-276"><a name="authorize"></a>How to: Restrict data access for authorized users</span></span>
<span data-ttu-id="6fd2e-277">Dans la section précédente de hello, nous vous avons montré comment tooretrieve hello ID d’utilisateur d’un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-277">In hello previous section, we showed how tooretrieve hello user ID of an authenticated user.</span></span> <span data-ttu-id="6fd2e-278">Vous pouvez restreindre l’accès toodata et autres ressources en fonction de cette valeur.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-278">You can restrict access toodata and other resources based on this value.</span></span> <span data-ttu-id="6fd2e-279">Par exemple, ajout d’un tootables de la colonne ID d’utilisateur et le filtrage des résultats de la requête par ID d’utilisateur hello hello sont un toolimit de façon simple retourné utilisateurs tooauthorized uniquement des données.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-279">For example, adding a userId column tootables and filtering hello query results by hello user ID is a simple way toolimit returned data only tooauthorized users.</span></span> <span data-ttu-id="6fd2e-280">Hello de code suivant retourne les lignes de données uniquement lorsque hello SID correspond à la valeur de colonne de UserId hello sur la table TodoItem de hello :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-280">hello following code returns data rows only when hello SID matches the value in hello UserId column on hello TodoItem table:</span></span>

    // Get hello SID of hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;

    // Only return data rows that belong toohello current user.
    return Query().Where(t => t.UserId == sid);

<span data-ttu-id="6fd2e-281">Hello `Query()` méthode retourne un `IQueryable` qui peuvent être manipulées par filtrage de toohandle LINQ.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-281">hello `Query()` method returns an `IQueryable` that can be manipulated by LINQ toohandle filtering.</span></span>

## <a name="how-to-add-push-notifications-tooa-server-project"></a><span data-ttu-id="6fd2e-282">Comment : ajouter un projet de serveur de tooa de notifications push</span><span class="sxs-lookup"><span data-stu-id="6fd2e-282">How to: Add push notifications tooa server project</span></span>
<span data-ttu-id="6fd2e-283">Ajouter un projet de serveur push notifications tooyour en étendant hello **MobileAppConfiguration** objet et la création d’un client de concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-283">Add push notifications tooyour server project by extending hello **MobileAppConfiguration** object and creating a Notification Hubs client.</span></span>

1. <span data-ttu-id="6fd2e-284">Dans Visual Studio, cliquez sur le projet de serveur hello et cliquez sur **gérer les Packages NuGet**, recherchez `Microsoft.Azure.Mobile.Server.Notifications`, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-284">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for `Microsoft.Azure.Mobile.Server.Notifications`, then click **Install**.</span></span>
2. <span data-ttu-id="6fd2e-285">Répétez cette hello de tooinstall étape `Microsoft.Azure.NotificationHubs` package, qui inclut la bibliothèque cliente de concentrateurs de Notification hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-285">Repeat this step tooinstall hello `Microsoft.Azure.NotificationHubs` package, which includes hello Notification Hubs client library.</span></span>
3. <span data-ttu-id="6fd2e-286">Dans App_Start/Startup.MobileApp.cs et ajoutez un appel toohello **AddPushNotifications()** méthode d’extension lors de l’initialisation :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-286">In App_Start/Startup.MobileApp.cs, and add a call toohello **AddPushNotifications()** extension method during initialization:</span></span>

        new MobileAppConfiguration()
            // other features...
            .AddPushNotifications()
            .ApplyTo(config);
4. <span data-ttu-id="6fd2e-287">Ajoutez hello suivant le code qui crée un client de concentrateurs de Notification :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-287">Add hello following code that creates a Notification Hubs client:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            config.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create a new Notification Hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

<span data-ttu-id="6fd2e-288">Vous pouvez maintenant utiliser hello concentrateurs de Notification toosend push notifications tooregistered les périphériques clients.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-288">You can now use hello Notification Hubs client toosend push notifications tooregistered devices.</span></span> <span data-ttu-id="6fd2e-289">Pour plus d’informations, consultez [ajouter push notifications tooyour application](app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-289">For more information, see [Add push notifications tooyour app](app-service-mobile-ios-get-started-push.md).</span></span> <span data-ttu-id="6fd2e-290">toolearn en savoir plus sur les concentrateurs de Notification, consultez [vue d’ensemble des concentrateurs de Notification](../notification-hubs/notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-290">toolearn more about Notification Hubs, see [Notification Hubs Overview](../notification-hubs/notification-hubs-push-notification-overview.md).</span></span>

## <span data-ttu-id="6fd2e-291"><a name="tags"></a>Activer les notifications Push ciblées à l’aide de balises</span><span class="sxs-lookup"><span data-stu-id="6fd2e-291"><a name="tags"></a>How to: Enable targeted push using Tags</span></span>
<span data-ttu-id="6fd2e-292">Concentrateurs de notification vous permet d’envoyer des notifications ciblées toospecific inscriptions à l’aide de balises.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-292">Notification Hubs lets you send targeted notifications toospecific registrations by using tags.</span></span> <span data-ttu-id="6fd2e-293">Plusieurs balises sont créées automatiquement :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-293">Several tags are created automatically:</span></span>

* <span data-ttu-id="6fd2e-294">Hello ID d’Installation identifie un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-294">hello Installation ID identifies a specific device.</span></span>
* <span data-ttu-id="6fd2e-295">Hello Id d’utilisateur en fonction de hello authentifié SID identifie un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-295">hello User Id based on hello authenticated SID identifies a specific user.</span></span>

<span data-ttu-id="6fd2e-296">Hello installation ID est accessible à partir de hello **installationId** propriété hello **MobileServiceClient**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-296">hello installation ID can be accessed from hello **installationId** property on hello **MobileServiceClient**.</span></span>  <span data-ttu-id="6fd2e-297">Hello exemple suivant montre comment utiliser un tooadd de ID d’installation une installation spécifique de balise tooa dans des concentrateurs de Notification :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-297">hello following example shows how to use an installation ID tooadd a tag tooa specific installation in Notification Hubs:</span></span>

    hub.PatchInstallation("my-installation-id", new[]
    {
        new PartialUpdateOperation
        {
            Operation = UpdateOperationType.Add,
            Path = "/tags",
            Value = "{my-tag}"
        }
    });

<span data-ttu-id="6fd2e-298">Toutes les balises fournies par le client de hello lors de l’enregistrement des notifications push sont ignorés par hello principal lors de la création d’une installation de hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-298">Any tags supplied by hello client during push notification registration are ignored by hello backend when creating hello installation.</span></span> <span data-ttu-id="6fd2e-299">tooenable un tooadd client balises toohello installation, vous devez créer une API personnalisée qui ajoute des balises à l’aide de hello précédant le modèle.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-299">tooenable a client tooadd tags toohello installation, you must create a custom API that adds tags using hello preceding pattern.</span></span>

<span data-ttu-id="6fd2e-300">Consultez [balises de notification push de Client ajouté] [ 5] dans l’exemple de démarrage rapide terminée hello App Service Mobile Apps pour obtenir un exemple.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-300">See [Client-added push notification tags][5] in hello App Service Mobile Apps completed quickstart sample for an example.</span></span>

## <span data-ttu-id="6fd2e-301"><a name="push-user"></a>Comment : envoyer push notifications tooan de l’utilisateur authentifié</span><span class="sxs-lookup"><span data-stu-id="6fd2e-301"><a name="push-user"></a>How to: Send push notifications tooan authenticated user</span></span>
<span data-ttu-id="6fd2e-302">Lorsqu’un utilisateur authentifié s’inscrit pour les notifications push, une balise d’ID utilisateur est automatiquement ajoutée l’enregistrement de toohello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-302">When an authenticated user registers for push notifications, a user ID tag is automatically added toohello registration.</span></span> <span data-ttu-id="6fd2e-303">À l’aide de cette balise, vous pouvez envoyer par émission de données des appareils tooall notifications inscrits par cette personne.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-303">By using this tag, you can send push notifications tooall devices registered by that person.</span></span> <span data-ttu-id="6fd2e-304">Hello de code suivant obtient hello SID de l’utilisateur qui effectue la requête et envoie une inscription de périphérique modèle push notification tooevery pour cette personne :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-304">hello following code gets hello SID of user making the request and sends a template push notification tooevery device registration for that person:</span></span>

    // Get hello current user SID and create a tag for hello current user.
    var claimsPrincipal = this.User as ClaimsPrincipal;
    string sid = claimsPrincipal.FindFirst(ClaimTypes.NameIdentifier).Value;
    string userTag = "_UserId:" + sid;

    // Build a dictionary for hello template with hello item message text.
    var notification = new Dictionary<string, string> { { "message", item.Text } };

    // Send a template notification toohello user ID.
    await hub.SendTemplateNotificationAsync(notification, userTag);

<span data-ttu-id="6fd2e-305">Quand vous vous inscrivez à des notifications Push à partir d’un client authentifié, assurez-vous au préalable que l’authentification est bien terminée.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-305">When registering for push notifications from an authenticated client, make sure that authentication is complete before attempting registration.</span></span> <span data-ttu-id="6fd2e-306">Pour plus d’informations, consultez [Push toousers] [ 6] dans exemple de démarrage rapide terminée App Service Mobile Apps hello pour le service principal .NET.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-306">For more information, see [Push toousers][6] in hello App Service Mobile Apps completed quickstart sample for .NET backend.</span></span>

## <a name="how-to-debug-and-troubleshoot-hello-net-server-sdk"></a><span data-ttu-id="6fd2e-307">Comment : déboguer et résoudre les problèmes de hello .NET Server SDK</span><span class="sxs-lookup"><span data-stu-id="6fd2e-307">How to: Debug and troubleshoot hello .NET Server SDK</span></span>
<span data-ttu-id="6fd2e-308">Azure App Service fournit plusieurs techniques de débogage et de résolution des problèmes pour les applications ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-308">Azure App Service provides several debugging and troubleshooting techniques for ASP.NET applications:</span></span>

* [<span data-ttu-id="6fd2e-309">Surveiller les applications web dans Microsoft Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6fd2e-309">Monitoring an Azure App Service</span></span>](../app-service-web/web-sites-monitor.md)
* [<span data-ttu-id="6fd2e-310">Activer la journalisation des diagnostics pour les applications web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="6fd2e-310">Enable Diagnostic Logging in Azure App Service</span></span>](../app-service-web/web-sites-enable-diagnostic-log.md)
* [<span data-ttu-id="6fd2e-311">Dépanner un service Azure App dans Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6fd2e-311">Troubleshoot an Azure App Service in Visual Studio</span></span>](../app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md)

### <a name="logging"></a><span data-ttu-id="6fd2e-312">Journalisation</span><span class="sxs-lookup"><span data-stu-id="6fd2e-312">Logging</span></span>
<span data-ttu-id="6fd2e-313">Vous pouvez écrire des journaux de diagnostic Service tooApp à l’aide d’écriture de trace ASP.NET standard hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-313">You can write tooApp Service diagnostic logs by using hello standard ASP.NET trace writing.</span></span> <span data-ttu-id="6fd2e-314">Avant de pouvoir écrire des journaux de toohello, vous devez activer les diagnostics de votre serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-314">Before you can write toohello logs, you must enable diagnostics in your Mobile App backend.</span></span>

<span data-ttu-id="6fd2e-315">tooenable diagnostics et écriture toohello des journaux :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-315">tooenable diagnostics and write toohello logs:</span></span>

1. <span data-ttu-id="6fd2e-316">Suivez les étapes de hello dans [comment tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-316">Follow hello steps in [How tooenable diagnostics](../app-service-web/web-sites-enable-diagnostic-log.md#enablediag).</span></span>
2. <span data-ttu-id="6fd2e-317">Ajoutez hello qui suit à l’aide d’instruction dans votre fichier de code :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-317">Add hello following using statement in your code file:</span></span>

        using System.Web.Http.Tracing;
3. <span data-ttu-id="6fd2e-318">Créez un toowrite d’enregistreur de trace à partir de hello .NET principal toohello journaux de diagnostic, comme suit :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-318">Create a trace writer toowrite from hello .NET backend toohello diagnostic logs, as follows:</span></span>

        ITraceWriter traceWriter = this.Configuration.Services.GetTraceWriter();
        traceWriter.Info("Hello, World");
4. <span data-ttu-id="6fd2e-319">Publier à nouveau votre projet de serveur et accéder hello application Mobile back-end tooexecute hello code au chemin avec une journalisation hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-319">Republish your server project, and access hello Mobile App backend tooexecute hello code path with hello logging.</span></span>
5. <span data-ttu-id="6fd2e-320">Téléchargez et évaluez les journaux de hello, comme décrit dans [Comment : télécharger les journaux](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span><span class="sxs-lookup"><span data-stu-id="6fd2e-320">Download and evaluate hello logs, as described in [How to: Download logs](../app-service-web/web-sites-enable-diagnostic-log.md#download).</span></span>

### <span data-ttu-id="6fd2e-321"><a name="local-debug"></a>Débogage local avec authentification</span><span class="sxs-lookup"><span data-stu-id="6fd2e-321"><a name="local-debug"></a>Local debugging with authentication</span></span>
<span data-ttu-id="6fd2e-322">Vous pouvez exécuter votre application localement tootest change avant leur publication toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-322">You can run your application locally tootest changes before publishing them toohello cloud.</span></span> <span data-ttu-id="6fd2e-323">Pour la plupart des backends Azure Mobile Apps, appuyez sur *F5* lorsque vous êtes dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-323">For most Azure Mobile Apps backends, press *F5* while in Visual Studio.</span></span> <span data-ttu-id="6fd2e-324">Toutefois, certains points spécifiques sont à prendre en compte en lien avec l’authentification.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-324">However, there are some additional considerations when using authentication.</span></span>

<span data-ttu-id="6fd2e-325">Vous devez disposer d’une application mobile sur le cloud avec application d’authentification/autorisation du Service configurée, et que votre client doit avoir hello cloud point de terminaison spécifié en tant qu’hôte de connexion de substitution hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-325">You must have a cloud-based mobile app with App Service Authentication/Authorization configured, and your client must have hello cloud endpoint specified as hello alternate login host.</span></span> <span data-ttu-id="6fd2e-326">Consultez la documentation hello pour votre plateforme de client pour connaître la procédure hello requis.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-326">See hello documentation for your client platform for hello specific steps required.</span></span>

<span data-ttu-id="6fd2e-327">Assurez-vous que [Microsoft.Azure.Mobile.Server.Authentication] est installé sur votre backend mobile.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-327">Ensure that your mobile backend has [Microsoft.Azure.Mobile.Server.Authentication] installed.</span></span> <span data-ttu-id="6fd2e-328">Puis, dans la classe de démarrage de votre application OWIN, ajoutez après suivantes de hello, `MobileAppConfiguration` a été appliqué tooyour `HttpConfiguration`:</span><span class="sxs-lookup"><span data-stu-id="6fd2e-328">Then, in your application's OWIN startup class, add hello following, after `MobileAppConfiguration` has been applied tooyour `HttpConfiguration`:</span></span>

        app.UseAppServiceAuthentication(new AppServiceAuthenticationOptions()
        {
            SigningKey = ConfigurationManager.AppSettings["authSigningKey"],
            ValidAudiences = new[] { ConfigurationManager.AppSettings["authAudience"] },
            ValidIssuers = new[] { ConfigurationManager.AppSettings["authIssuer"] },
            TokenHandler = config.GetAppServiceTokenHandler()
        });

<span data-ttu-id="6fd2e-329">Bonjour précédent exemple, vous devez configurer hello *authAudience* et *authIssuer* paramètres d’application dans votre fichier Web.config du fichier tooeach l’URL de la racine de votre application, à l’aide de hello HTTPS schéma.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-329">In hello preceding example, you should configure hello *authAudience* and *authIssuer* application settings within your Web.config file tooeach be the URL of your application root, using hello HTTPS scheme.</span></span> <span data-ttu-id="6fd2e-330">De même, vous devez définir *authSigningKey* clé de signature de la valeur de hello toobe de votre application.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-330">Similarly you should set *authSigningKey* toobe hello value of your application's signing key.</span></span>
<span data-ttu-id="6fd2e-331">clé de signature hello tooobtain :</span><span class="sxs-lookup"><span data-stu-id="6fd2e-331">tooobtain hello signing key:</span></span>

1. <span data-ttu-id="6fd2e-332">Accédez application tooyour dans hello [portail Azure]</span><span class="sxs-lookup"><span data-stu-id="6fd2e-332">Navigate tooyour app within hello [Azure portal]</span></span>
2. <span data-ttu-id="6fd2e-333">Cliquez sur **Outils**, **Kudu**, **Accéder**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-333">Click **Tools**, **Kudu**, **Go**.</span></span>
3. <span data-ttu-id="6fd2e-334">Dans le site d’administration de Kudu hello, cliquez sur **environnement**.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-334">In hello Kudu Management site, click **Environment**.</span></span>
4. <span data-ttu-id="6fd2e-335">Rechercher la valeur hello pour *site Web\_AUTH\_signature\_clé*.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-335">Find hello value for *WEBSITE\_AUTH\_SIGNING\_KEY*.</span></span>

<span data-ttu-id="6fd2e-336">Hello utilisez la signature de clé pour hello *authSigningKey* paramètre dans votre configuration de l’application locale.  Votre serveur principal mobile est maintenant toovalidate équipés jetons lors de l’exécution localement, quel client hello Obtient un jeton de hello du point de terminaison sur le cloud hello.</span><span class="sxs-lookup"><span data-stu-id="6fd2e-336">Use hello signing key for hello *authSigningKey* parameter in your local application config.  Your mobile backend is now equipped toovalidate tokens when running locally, which hello client obtains hello token from hello cloud-based endpoint.</span></span>

[1]: https://msdn.microsoft.com/library/azure/dn961176.aspx
[2]: https://github.com/Azure/azure-mobile-apps-net-server
[3]: app-service-mobile-ios-get-started.md
[4]: https://azure.microsoft.com/downloads/
[5]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#client-added-push-notification-tags
[6]: https://github.com/Azure-Samples/app-service-mobile-dotnet-backend-quickstart/blob/master/README.md#push-to-users
[portail Azure]: https://portal.azure.com
[NuGet.org]: http://www.nuget.org/
[Microsoft.Azure.Mobile.Server]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/
[Microsoft.Azure.Mobile.Server.Quickstart]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Quickstart/
[Microsoft.Azure.Mobile.Server.Authentication]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Authentication/
[Microsoft.Azure.Mobile.Server.Login]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Login/
[Microsoft.Azure.Mobile.Server.Notifications]: http://www.nuget.org/packages/Microsoft.Azure.Mobile.Server.Notifications/
[MapHttpAttributeRoutes]: https://msdn.microsoft.com/library/dn479134(v=vs.118).aspx
