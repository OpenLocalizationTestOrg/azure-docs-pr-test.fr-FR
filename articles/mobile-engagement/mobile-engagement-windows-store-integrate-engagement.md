---
title: "aaaWindows intégration de kit de développement logiciel Engagement applications universel"
description: Comment tooIntegrate Azure Mobile Engagement avec les applications Windows universelles
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a><span data-ttu-id="bd471-103">Intégration du Kit de développement logiciel du module Engagement des applications universelles Windows</span><span class="sxs-lookup"><span data-stu-id="bd471-103">Windows Universal Apps Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bd471-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="bd471-104">Universal Windows</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="bd471-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="bd471-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="bd471-106">iOS</span><span class="sxs-lookup"><span data-stu-id="bd471-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="bd471-107">Android</span><span class="sxs-lookup"><span data-stu-id="bd471-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="bd471-108">Cette procédure décrit Analytique hello la plus simple façon tooactivate Engagement et l’analyse des fonctions dans votre application Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="bd471-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your Windows Universal application.</span></span>

<span data-ttu-id="bd471-109">Hello suit est que suffisamment rapport hello tooactivate journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals.</span><span class="sxs-lookup"><span data-stu-id="bd471-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="bd471-110">rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md) depuis Ces statistiques sont dépend de l’application.</span><span class="sxs-lookup"><span data-stu-id="bd471-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="bd471-111">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="bd471-111">Supported versions</span></span>
<span data-ttu-id="bd471-112">Hello Mobile Engagement SDK pour applications Windows universelles peut uniquement être intégré dans Windows Runtime et les applications de plateforme Windows universelle qui ciblent :</span><span class="sxs-lookup"><span data-stu-id="bd471-112">hello Mobile Engagement SDK for Windows Universal Apps can only be integrated into Windows Runtime and Universal Windows Platform applications targeting :</span></span>

* <span data-ttu-id="bd471-113">Windows 8</span><span class="sxs-lookup"><span data-stu-id="bd471-113">Windows 8</span></span>
* <span data-ttu-id="bd471-114">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="bd471-114">Windows 8.1</span></span>
* <span data-ttu-id="bd471-115">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="bd471-115">Windows Phone 8.1</span></span>
* <span data-ttu-id="bd471-116">Windows 10 (gammes mobiles et de bureau)</span><span class="sxs-lookup"><span data-stu-id="bd471-116">Windows 10 (desktop and mobile families)</span></span>

> [!NOTE]
> <span data-ttu-id="bd471-117">Si vous ciblez Windows Phone Silverlight, consultez toohello [procédure d’intégration de Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="bd471-117">If you are targeting Windows Phone Silverlight then refer toohello [Windows Phone Silverlight integration procedure](mobile-engagement-windows-phone-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a><span data-ttu-id="bd471-118">Installer hello SDK des applications Universal Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="bd471-118">Install hello Mobile Engagement Universal Apps SDK</span></span>
### <a name="all-platforms"></a><span data-ttu-id="bd471-119">Toutes les plateformes</span><span class="sxs-lookup"><span data-stu-id="bd471-119">All platforms</span></span>
<span data-ttu-id="bd471-120">Hello Mobile Engagement SDK pour Windows application universelle est disponible comme package Nuget appelé *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="bd471-120">hello Mobile Engagement SDK for Windows Universal App is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="bd471-121">Vous pouvez l’installer à partir de hello Gestionnaire de Package Nuget de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd471-121">You can install it from hello Visual Studio Nuget Package Manager.</span></span>

### <a name="windows-8x-and-windows-phone-81"></a><span data-ttu-id="bd471-122">Windows 8.x et Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="bd471-122">Windows 8.x and Windows Phone 8.1</span></span>
<span data-ttu-id="bd471-123">NuGet déploie automatiquement les ressources du Kit de développement logiciel hello Bonjour `Resources` dossier à votre projet d’application hello racine.</span><span class="sxs-lookup"><span data-stu-id="bd471-123">NuGet automatically deploys hello SDK resources in hello `Resources` folder at hello root of your application project.</span></span>

### <a name="windows-10-universal-windows-platform-applications"></a><span data-ttu-id="bd471-124">Applications de la plateforme Windows universelle Windows 10</span><span class="sxs-lookup"><span data-stu-id="bd471-124">Windows 10 Universal Windows Platform applications</span></span>
<span data-ttu-id="bd471-125">NuGet ne déploie pas automatiquement les ressources du Kit de développement logiciel hello dans votre application UWP encore.</span><span class="sxs-lookup"><span data-stu-id="bd471-125">NuGet does not automatically deploy hello SDK resources in your UWP application yet.</span></span> <span data-ttu-id="bd471-126">Vous avez toodo manuellement avant le déploiement de ressources est réintroduit dans NuGet :</span><span class="sxs-lookup"><span data-stu-id="bd471-126">You have toodo it manually until resources deployment is reintroduced in NuGet:</span></span>

1. <span data-ttu-id="bd471-127">Ouvrez votre Explorateur de fichiers.</span><span class="sxs-lookup"><span data-stu-id="bd471-127">Open your File Explorer.</span></span>
2. <span data-ttu-id="bd471-128">Accédez toohello l’emplacement suivant (**x.x.x** est la version hello d’Engagement que vous installez) : *% USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\*  *x.x.x**\\content\win81*</span><span class="sxs-lookup"><span data-stu-id="bd471-128">Navigate toohello following location (**x.x.x** is hello version of Engagement you are installing): *%USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\\**x.x.x**\\content\win81*</span></span>
3. <span data-ttu-id="bd471-129">Glisser- déposer hello **ressources** dossier hello fichier explorer toohello de racine de votre projet dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bd471-129">Drag and drop hello **Resources** folder from hello file explorer toohello root of your project in Visual Studio.</span></span>
4. <span data-ttu-id="bd471-130">Dans Visual Studio, sélectionnez votre projet et activer hello **afficher tous les fichiers** icône au-dessus hello **l’Explorateur de solutions**.</span><span class="sxs-lookup"><span data-stu-id="bd471-130">In Visual Studio select your project and activate hello **Show All files** icon on top of hello **Solution Explorer**.</span></span>
5. <span data-ttu-id="bd471-131">Certains fichiers ne sont pas inclus dans le projet de hello.</span><span class="sxs-lookup"><span data-stu-id="bd471-131">Some files are not included in hello project.</span></span> <span data-ttu-id="bd471-132">tooimport à la fois avec le bouton droit à cliquer sur hello **ressources** dossier, **exclure du projet** puis un autre avec le bouton droit sur hello **ressources** dossier **Include dans le projet** toore-inclure la totalité du dossier hello.</span><span class="sxs-lookup"><span data-stu-id="bd471-132">tooimport them at once right click on hello **Resources** folder, **Exclude from project** then another right click on hello **Resources** folder, **Include in project** toore-include hello whole folder.</span></span> <span data-ttu-id="bd471-133">Tous les fichiers à partir de hello **ressources** dossier sont désormais incluses dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="bd471-133">All files from hello **Resources** folder are now included in your project.</span></span>

## <a name="add-hello-capabilities"></a><span data-ttu-id="bd471-134">Ajouter des fonctionnalités hello</span><span class="sxs-lookup"><span data-stu-id="bd471-134">Add hello capabilities</span></span>
<span data-ttu-id="bd471-135">Hello SDK de l’Engagement a besoin de certaines fonctionnalités de hello Kit de développement dans l’ordre toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="bd471-135">hello Engagement SDK needs some capabilities of hello Windows SDK in order toowork properly.</span></span>

<span data-ttu-id="bd471-136">Ouvrez votre `Package.appxmanifest` de fichiers et assurez-vous que hello suivant des fonctions sont déclarés :</span><span class="sxs-lookup"><span data-stu-id="bd471-136">Open your `Package.appxmanifest` file and be sure that hello following capabilities are declared:</span></span>

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="bd471-137">Initialiser hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="bd471-137">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="bd471-138">Configuration d'Engagement</span><span class="sxs-lookup"><span data-stu-id="bd471-138">Engagement configuration</span></span>
<span data-ttu-id="bd471-139">configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="bd471-139">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="bd471-140">Modifiez cette toospecify de fichier :</span><span class="sxs-lookup"><span data-stu-id="bd471-140">Edit this file toospecify:</span></span>

* <span data-ttu-id="bd471-141">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="bd471-141">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="bd471-142">Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="bd471-142">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

<span data-ttu-id="bd471-143">chaîne de connexion Hello pour votre application s’affiche sur hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="bd471-143">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="bd471-144">Initialisation d'Engagement</span><span class="sxs-lookup"><span data-stu-id="bd471-144">Engagement initialization</span></span>
<span data-ttu-id="bd471-145">Quand vous créez un projet, un fichier `App.xaml.cs` est généré.</span><span class="sxs-lookup"><span data-stu-id="bd471-145">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="bd471-146">Cette classe hérite de `Application` et contient de nombreuses méthodes importantes.</span><span class="sxs-lookup"><span data-stu-id="bd471-146">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="bd471-147">Il sera également utilisé tooinitialize hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="bd471-147">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="bd471-148">Modifier hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="bd471-148">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="bd471-149">Ajouter tooyour `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="bd471-149">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="bd471-150">Définissez une initialisation d’Engagement méthode tooshare hello qu’une seule fois pour tous les appels :</span><span class="sxs-lookup"><span data-stu-id="bd471-150">Define a method tooshare hello Engagement initialization once for all calls:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* <span data-ttu-id="bd471-151">Appelez `InitEngagement` Bonjour `OnLaunched` méthode :</span><span class="sxs-lookup"><span data-stu-id="bd471-151">Call `InitEngagement` in hello `OnLaunched` method:</span></span>
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* <span data-ttu-id="bd471-152">Lorsque votre application est lancée à l’aide d’un schéma personnalisé, une autre ligne de commande de l’application ou hello hello puis `OnActivated` méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="bd471-152">When your application is launched using a custom scheme, another application or hello command line then hello `OnActivated` method is called.</span></span> <span data-ttu-id="bd471-153">Vous devez également tooinitiate hello Engagement SDK quand votre application est activée.</span><span class="sxs-lookup"><span data-stu-id="bd471-153">You also need tooinitiate hello Engagement SDK when your app is activated.</span></span> <span data-ttu-id="bd471-154">toodo donc remplacer `OnActivated` méthode :</span><span class="sxs-lookup"><span data-stu-id="bd471-154">toodo so, override `OnActivated` method:</span></span>
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> <span data-ttu-id="bd471-155">Nous vous déconseillons de vous tooadd hello Engagement d’initialisation à un autre endroit de votre application.</span><span class="sxs-lookup"><span data-stu-id="bd471-155">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="bd471-156">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="bd471-156">Basic reporting</span></span>
### <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="bd471-157">Méthode recommandée : surchargez vos classes `Page`</span><span class="sxs-lookup"><span data-stu-id="bd471-157">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="bd471-158">Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, vous pouvez simplement mettre toutes vos `Page` sous-classes héritent hello `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="bd471-158">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="bd471-159">Voici un exemple de procédure toodo pour une page de votre application.</span><span class="sxs-lookup"><span data-stu-id="bd471-159">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="bd471-160">Vous pouvez effectuer hello identiques pour toutes les pages de votre application.</span><span class="sxs-lookup"><span data-stu-id="bd471-160">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="bd471-161">Fichier source C#</span><span class="sxs-lookup"><span data-stu-id="bd471-161">C# Source file</span></span>
<span data-ttu-id="bd471-162">Modifiez le fichier `.xaml.cs` de votre page :</span><span class="sxs-lookup"><span data-stu-id="bd471-162">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="bd471-163">Ajouter tooyour `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="bd471-163">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="bd471-164">Remplacez `Page` par `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="bd471-164">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="bd471-165">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="bd471-165">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="bd471-166">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="bd471-166">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="bd471-167">Si votre page substitue hello `OnNavigatedTo` (méthode), être toocall vraiment `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="bd471-167">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="bd471-168">Dans le cas contraire, activité hello n’est pas signalée (hello `EngagementPage` appelle `StartActivity` à l’intérieur de son `OnNavigatedTo` méthode).</span><span class="sxs-lookup"><span data-stu-id="bd471-168">Otherwise,  hello activity will not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="bd471-169">Fichier XAML</span><span class="sxs-lookup"><span data-stu-id="bd471-169">XAML file</span></span>
<span data-ttu-id="bd471-170">Modifiez le fichier `.xaml` de votre page :</span><span class="sxs-lookup"><span data-stu-id="bd471-170">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="bd471-171">Ajoutez les déclarations d’espaces de noms tooyour :</span><span class="sxs-lookup"><span data-stu-id="bd471-171">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="bd471-172">Remplacez `Page` par `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="bd471-172">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="bd471-173">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="bd471-173">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="bd471-174">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="bd471-174">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a><span data-ttu-id="bd471-175">Substituer le comportement par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="bd471-175">Override hello default behaviour</span></span>
<span data-ttu-id="bd471-176">Par défaut, nom de la classe de page de hello hello est signalée comme nom de l’activité hello, avec sans supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="bd471-176">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="bd471-177">Si la classe hello utilise hello suffixe de « Page », Engagement entraîne également sa suppression.</span><span class="sxs-lookup"><span data-stu-id="bd471-177">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="bd471-178">Si vous souhaitez le comportement par défaut de hello toooverride pour le nom de hello, ajoutez simplement ce code tooyour :</span><span class="sxs-lookup"><span data-stu-id="bd471-178">If you want toooverride hello default behaviour for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="bd471-179">Si vous souhaitez tooreport certaines informations supplémentaires avec votre activité, vous pouvez ajouter ce code tooyour :</span><span class="sxs-lookup"><span data-stu-id="bd471-179">If you want tooreport some extra informations with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="bd471-180">Ces méthodes sont appelées dans hello `OnNavigatedTo` méthode de votre page.</span><span class="sxs-lookup"><span data-stu-id="bd471-180">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="bd471-181">Autre méthode : appeler `StartActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="bd471-181">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="bd471-182">Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Page` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent` direct de méthodes.</span><span class="sxs-lookup"><span data-stu-id="bd471-182">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="bd471-183">Nous vous recommandons de toocall `StartActivity` à l’intérieur de votre `OnNavigatedTo` méthode de votre Page.</span><span class="sxs-lookup"><span data-stu-id="bd471-183">We recommend toocall `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="bd471-184">Assurez-vous de terminer votre session correctement.</span><span class="sxs-lookup"><span data-stu-id="bd471-184">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="bd471-185">Hello SDK Universal Windows appelle automatiquement hello `EndActivity` méthode lors de l’application hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="bd471-185">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="bd471-186">Par conséquent, il est **hautement** recommandé toocall hello `StartActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop**jamais** appel hello `EndActivity` (méthode), cette méthode envoie tooEngagement serveur que l’utilisateur actuel a laissez hello application, ce sera a un impact sur tous les journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="bd471-186">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method, this method sends tooEngagement server that current user has leave hello application, this will impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="bd471-187">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="bd471-187">Advanced reporting</span></span>
<span data-ttu-id="bd471-188">Si vous le souhaitez, vous souhaiterez peut-être tooreport les événements d’application spécifique, les erreurs et les travaux, toodo donc, utilisez hello d’autres méthodes trouvés dans hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="bd471-188">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="bd471-189">Hello Engagement API permet toouse toutes les fonctionnalités avancées d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="bd471-189">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="bd471-190">Pour plus d’informations, consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="bd471-190">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="bd471-191">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="bd471-191">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="bd471-192">Désactiver le signalement automatique des incidents</span><span class="sxs-lookup"><span data-stu-id="bd471-192">Disable automatic crash reporting</span></span>
<span data-ttu-id="bd471-193">Vous pouvez désactiver hello automatique de rapport d’incident fonctionnalité d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="bd471-193">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="bd471-194">Dans ce cas, si une exception non gérée se produit, Engagement ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="bd471-194">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="bd471-195">Si vous envisagez de toodisable cette fonctionnalité, gardez à l’esprit que, lorsqu’un incident non géré se produit dans votre application, Engagement n’envoie pas de blocage de hello **et** ne ferme pas la session de hello et les travaux.</span><span class="sxs-lookup"><span data-stu-id="bd471-195">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="bd471-196">toodisable automatique sur incident reporting, simplement personnaliser votre configuration en fonction de méthode hello vous l’avez déclarée :</span><span class="sxs-lookup"><span data-stu-id="bd471-196">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it:</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="bd471-197">Dans le fichier `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="bd471-197">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="bd471-198">Définir le rapport incident trop`false` entre `<reportCrash>` et `</reportCrash>` balises.</span><span class="sxs-lookup"><span data-stu-id="bd471-198">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="bd471-199">Dans l'objet `EngagementConfiguration` au moment l'exécution</span><span class="sxs-lookup"><span data-stu-id="bd471-199">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="bd471-200">Définissez toofalse de panne de rapport à l’aide de votre objet EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="bd471-200">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="bd471-201">Mode rafale</span><span class="sxs-lookup"><span data-stu-id="bd471-201">Burst mode</span></span>
<span data-ttu-id="bd471-202">Par défaut, les rapports de service d’Engagement hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="bd471-202">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="bd471-203">Si votre application rapports journaux très fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée hello « mode de croissance »).</span><span class="sxs-lookup"><span data-stu-id="bd471-203">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="bd471-204">toodo appeler par conséquent, la méthode hello :</span><span class="sxs-lookup"><span data-stu-id="bd471-204">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="bd471-205">l’argument Hello est une valeur dans **millisecondes**.</span><span class="sxs-lookup"><span data-stu-id="bd471-205">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="bd471-206">À tout moment, si vous souhaitez que la journalisation en temps réel tooreactivate hello, appelez uniquement méthode hello sans paramètres ou avec la valeur de hello 0.</span><span class="sxs-lookup"><span data-stu-id="bd471-206">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="bd471-207">Hello mode rafale légèrement augmenter la batterie de hello vie mais n’a un impact sur hello Engagement moniteur : toutes les sessions et les travaux seront arrondies toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible).</span><span class="sxs-lookup"><span data-stu-id="bd471-207">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="bd471-208">Il est recommandé de toouse un seuil de croissance n’est plus à 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="bd471-208">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="bd471-209">Vous avez toobe souvenez-vous des journaux enregistrés too300 limité des éléments.</span><span class="sxs-lookup"><span data-stu-id="bd471-209">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="bd471-210">Si l'envoi est trop long, vous risquez de perdre certains journaux.</span><span class="sxs-lookup"><span data-stu-id="bd471-210">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="bd471-211">seuil de croissance Hello ne peut pas être configurée période tooa inférieur à 1 s.</span><span class="sxs-lookup"><span data-stu-id="bd471-211">hello burst threshold cannot be configured tooa period lesser than 1s.</span></span> <span data-ttu-id="bd471-212">Si vous essayez donc toodo, hello SDK affiche une trace avec l’erreur de hello et sera automatiquement réinitialisé toohello par défaut, c'est-à-dire 0.</span><span class="sxs-lookup"><span data-stu-id="bd471-212">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, i.e., 0s.</span></span> <span data-ttu-id="bd471-213">Cette opération déclenche hello SDK tooreport hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="bd471-213">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

