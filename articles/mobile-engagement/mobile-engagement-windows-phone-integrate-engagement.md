---
title: "aaaWindows l’intégration de kit de développement logiciel Silverlight Engagement téléphonique"
description: Comment tooIntegrate Azure Mobile Engagement avec les applications Silverlight Windows Phone
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="a767f-103">Intégration du Kit de développement logiciel (SDK) d’Engagement Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a767f-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a767f-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="a767f-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="a767f-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="a767f-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="a767f-106">iOS</span><span class="sxs-lookup"><span data-stu-id="a767f-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="a767f-107">Android</span><span class="sxs-lookup"><span data-stu-id="a767f-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="a767f-108">Cette procédure décrit Analytique hello la plus simple façon tooactivate Azure Mobile Engagement et l’analyse des fonctions dans votre application Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="a767f-108">This procedure describes hello simplest way tooactivate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="a767f-109">Hello suit est que suffisamment rapport hello tooactivate journaux nécessaires toocompute toutes les statistiques concernant les utilisateurs, Sessions, activités, blocages et Technicals.</span><span class="sxs-lookup"><span data-stu-id="a767f-109">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="a767f-110">rapport Hello de journaux nécessaires toocompute autres statistiques telles que les événements, les erreurs et les tâches doivent être effectués manuellement à l’aide des API de l’Engagement de hello (consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) ci-dessous) dans la mesure où ces statistiques sont dépend de l’application.</span><span class="sxs-lookup"><span data-stu-id="a767f-110">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API (see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="a767f-111">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="a767f-111">Supported versions</span></span>
<span data-ttu-id="a767f-112">Hello le Kit de développement logiciel Mobile Engagement pour Windows Silverlight peut uniquement être intégré dans des applications qui ciblent :</span><span class="sxs-lookup"><span data-stu-id="a767f-112">hello Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="a767f-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="a767f-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="a767f-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="a767f-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="a767f-115">Si vous ciblez Windows Phone 8.1 (non Silverlight), consultez toohello [procédure d’intégration Windows universel](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="a767f-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer toohello [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="a767f-116">Installer hello Mobile Engagement Silverlight SDK</span><span class="sxs-lookup"><span data-stu-id="a767f-116">Install hello Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="a767f-117">Hello Mobile Engagement Kit de développement logiciel de Silverlight pour Windows est disponible comme package Nuget appelé *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="a767f-117">hello Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="a767f-118">Vous pouvez l’installer à partir de hello Gestionnaire de Package Nuget de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a767f-118">You can install it from hello Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="a767f-119">Ajouter des fonctionnalités hello</span><span class="sxs-lookup"><span data-stu-id="a767f-119">Add hello capabilities</span></span>
<span data-ttu-id="a767f-120">Hello SDK de l’Engagement a besoin de certaines fonctionnalités de hello Kit de développement logiciel Windows Phone Silverlight dans l’ordre toowork correctement.</span><span class="sxs-lookup"><span data-stu-id="a767f-120">hello Engagement SDK needs some capabilities of hello Windows Phone Silverlight SDK in order toowork properly.</span></span>

<span data-ttu-id="a767f-121">Ouvrez votre `WMAppManifest.xml` de fichiers et assurez-vous que hello suivant des fonctions sont déclarés dans hello `Capabilities` Panneau de configuration :</span><span class="sxs-lookup"><span data-stu-id="a767f-121">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared in hello `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="a767f-122">Initialiser hello Engagement SDK</span><span class="sxs-lookup"><span data-stu-id="a767f-122">Initialize hello Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="a767f-123">Configuration d'Engagement</span><span class="sxs-lookup"><span data-stu-id="a767f-123">Engagement configuration</span></span>
<span data-ttu-id="a767f-124">configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="a767f-124">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="a767f-125">Modifiez cette toospecify de fichier :</span><span class="sxs-lookup"><span data-stu-id="a767f-125">Edit this file toospecify :</span></span>

* <span data-ttu-id="a767f-126">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="a767f-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="a767f-127">Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="a767f-127">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="a767f-128">chaîne de connexion Hello pour votre application s’affiche sur hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="a767f-128">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="a767f-129">Initialisation d'Engagement</span><span class="sxs-lookup"><span data-stu-id="a767f-129">Engagement initialization</span></span>
<span data-ttu-id="a767f-130">Quand vous créez un projet, un fichier `App.xaml.cs` est généré.</span><span class="sxs-lookup"><span data-stu-id="a767f-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="a767f-131">Cette classe hérite de `Application` et contient de nombreuses méthodes importantes.</span><span class="sxs-lookup"><span data-stu-id="a767f-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="a767f-132">Il sera également utilisé tooinitialize hello Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="a767f-132">It will also be used tooinitialize hello Engagement SDK.</span></span>

<span data-ttu-id="a767f-133">Modifier hello `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="a767f-133">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="a767f-134">Ajouter tooyour `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="a767f-134">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="a767f-135">Insérer `EngagementAgent.Instance.Init` Bonjour `Application_Launching` méthode :</span><span class="sxs-lookup"><span data-stu-id="a767f-135">Insert `EngagementAgent.Instance.Init` in hello `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="a767f-136">Insérer `EngagementAgent.Instance.OnActivated` Bonjour `Application_Activated` méthode :</span><span class="sxs-lookup"><span data-stu-id="a767f-136">Insert `EngagementAgent.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="a767f-137">Nous vous déconseillons de vous tooadd hello Engagement d’initialisation à un autre endroit de votre application.</span><span class="sxs-lookup"><span data-stu-id="a767f-137">We strongly discourage you tooadd hello Engagement initialization in another place of your application.</span></span> <span data-ttu-id="a767f-138">Toutefois, n’oubliez pas que hello `EngagementAgent.Instance.Init` méthode s’exécute sur un thread dédié et non sur hello thread d’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a767f-138">However, be aware that hello `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on hello UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="a767f-139">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="a767f-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="a767f-140">Méthode recommandée : surchargez vos classes `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="a767f-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="a767f-141">Dans le rapport de hello order tooactivate de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, vous pouvez simplement mettre toutes vos `PhoneApplicationPage` sous-classes héritent hello `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="a767f-141">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="a767f-142">Voici un exemple de procédure toodo pour une page de votre application.</span><span class="sxs-lookup"><span data-stu-id="a767f-142">Here is an example of how toodo this for a page of your application.</span></span> <span data-ttu-id="a767f-143">Vous pouvez effectuer hello identiques pour toutes les pages de votre application.</span><span class="sxs-lookup"><span data-stu-id="a767f-143">You can do hello same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="a767f-144">Fichier source C#</span><span class="sxs-lookup"><span data-stu-id="a767f-144">C# Source file</span></span>
<span data-ttu-id="a767f-145">Modifiez le fichier `.xaml.cs` de votre page :</span><span class="sxs-lookup"><span data-stu-id="a767f-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="a767f-146">Ajouter tooyour `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="a767f-146">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="a767f-147">Remplacez `PhoneApplicationPage` par `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="a767f-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="a767f-148">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="a767f-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="a767f-149">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="a767f-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="a767f-150">Si votre page hérite de hello `OnNavigatedTo` (méthode), être prudent toolet hello `base.OnNavigatedTo(e)` appeler.</span><span class="sxs-lookup"><span data-stu-id="a767f-150">If your page inherits from hello `OnNavigatedTo` method, be careful toolet hello `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="a767f-151">Dans le cas contraire, activité hello n’est pas signalée.</span><span class="sxs-lookup"><span data-stu-id="a767f-151">Otherwise, hello activity will not be reported.</span></span> <span data-ttu-id="a767f-152">En effet, hello `EngagementPage` appelle `StartActivity` à l’intérieur de hello `OnNavigatedTo` (méthode).</span><span class="sxs-lookup"><span data-stu-id="a767f-152">Indeed, hello `EngagementPage` is calling `StartActivity` inside hello `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="a767f-153">Fichier XAML</span><span class="sxs-lookup"><span data-stu-id="a767f-153">XAML file</span></span>
<span data-ttu-id="a767f-154">Modifiez le fichier `.xaml` de votre page :</span><span class="sxs-lookup"><span data-stu-id="a767f-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="a767f-155">Ajoutez les déclarations d’espaces de noms tooyour :</span><span class="sxs-lookup"><span data-stu-id="a767f-155">Add tooyour namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="a767f-156">Remplacez `phone:PhoneApplicationPage` par `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="a767f-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="a767f-157">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="a767f-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="a767f-158">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="a767f-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a><span data-ttu-id="a767f-159">Substituer le comportement par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="a767f-159">Override hello default behavior</span></span>
<span data-ttu-id="a767f-160">Par défaut, nom de la classe de page de hello hello est signalée comme nom de l’activité hello, avec sans supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="a767f-160">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="a767f-161">Si la classe hello utilise hello suffixe de « Page », Engagement entraîne également sa suppression.</span><span class="sxs-lookup"><span data-stu-id="a767f-161">If hello class uses hello "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="a767f-162">Si vous souhaitez le comportement par défaut de hello toooverride pour le nom de hello, ajoutez simplement ce code tooyour :</span><span class="sxs-lookup"><span data-stu-id="a767f-162">If you want toooverride hello default behavior for hello name, simply add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="a767f-163">Si vous souhaitez tooreport des informations supplémentaires avec votre activité, vous pouvez ajouter ce code tooyour :</span><span class="sxs-lookup"><span data-stu-id="a767f-163">If you want tooreport some extra information with your activity, you can add this tooyour code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="a767f-164">Ces méthodes sont appelées dans hello `OnNavigatedTo` méthode de votre page.</span><span class="sxs-lookup"><span data-stu-id="a767f-164">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="a767f-165">Autre méthode : appeler `StartActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="a767f-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="a767f-166">Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `PhoneApplicationPage` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent` direct de méthodes.</span><span class="sxs-lookup"><span data-stu-id="a767f-166">If you cannot or do not want toooverload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="a767f-167">Nous vous recommandons d’appeler `StartActivity` à l’intérieur de la méthode `OnNavigatedTo` de votre PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="a767f-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="a767f-168">Assurez-vous de terminer votre session correctement.</span><span class="sxs-lookup"><span data-stu-id="a767f-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="a767f-169">Kit de développement logiciel de Hello appelle automatiquement hello `EndActivity` méthode lors de l’application hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="a767f-169">hello SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="a767f-170">Par conséquent, il est **hautement** recommandé toocall hello `StartActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop**jamais** appel hello `EndActivity` (méthode).</span><span class="sxs-lookup"><span data-stu-id="a767f-170">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="a767f-171">Cette méthode envoie un message toohello Engagement serveur que l’utilisateur actuel hello a quitté l’application hello et que cela affecte tous les journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="a767f-171">This method sends a message toohello Engagement server that hello current user has left hello application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="a767f-172">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="a767f-172">Advanced reporting</span></span>
<span data-ttu-id="a767f-173">Si vous le souhaitez, vous souhaiterez peut-être tooreport les événements d’application spécifique, les erreurs et les travaux, toodo donc, utilisez hello d’autres méthodes trouvés dans hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="a767f-173">Optionally, you may want tooreport application specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="a767f-174">Hello Engagement API permet toouse toutes les fonctionnalités avancées d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="a767f-174">hello Engagement API allows toouse all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="a767f-175">Pour plus d’informations, consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="a767f-175">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="a767f-176">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="a767f-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="a767f-177">Désactiver le signalement automatique des incidents</span><span class="sxs-lookup"><span data-stu-id="a767f-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="a767f-178">Vous pouvez désactiver hello automatique de rapport d’incident fonctionnalité d’Engagement.</span><span class="sxs-lookup"><span data-stu-id="a767f-178">You can disable hello automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="a767f-179">Dans ce cas, si une exception non gérée se produit, Engagement ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="a767f-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="a767f-180">Si vous envisagez de toodisable cette fonctionnalité, gardez à l’esprit que, lorsqu’un incident non géré se produit dans votre application, Engagement n’envoie pas de blocage de hello **AND** il ne ferme pas la session de hello et les travaux.</span><span class="sxs-lookup"><span data-stu-id="a767f-180">If you plan toodisable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send hello crash **AND** it will not close hello session and jobs.</span></span>
> 
> 

<span data-ttu-id="a767f-181">toodisable automatique sur incident reporting, simplement personnaliser votre configuration en fonction de méthode hello vous l’avez déclarée :</span><span class="sxs-lookup"><span data-stu-id="a767f-181">toodisable automatic crash reporting, just customize your configuration depending on hello way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="a767f-182">Dans le fichier `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="a767f-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="a767f-183">Définir le rapport incident trop`false` entre `<reportCrash>` et `</reportCrash>` balises.</span><span class="sxs-lookup"><span data-stu-id="a767f-183">Set report crash too`false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="a767f-184">Dans l'objet `EngagementConfiguration` au moment l'exécution</span><span class="sxs-lookup"><span data-stu-id="a767f-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="a767f-185">Définissez toofalse de panne de rapport à l’aide de votre objet EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="a767f-185">Set report crash toofalse using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="a767f-186">Mode rafale</span><span class="sxs-lookup"><span data-stu-id="a767f-186">Burst mode</span></span>
<span data-ttu-id="a767f-187">Par défaut, les rapports de service d’Engagement hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="a767f-187">By default, hello Engagement service reports logs in real time.</span></span> <span data-ttu-id="a767f-188">Si votre application rapports journaux très fréquemment, il est mieux toobuffer hello journaux et tooreport à la fois à une base de temps réguliers (appelée hello « mode de croissance »).</span><span class="sxs-lookup"><span data-stu-id="a767f-188">If your application reports logs very frequently, it is better toobuffer hello logs and tooreport them all at once on a regular time base (this is called hello “burst mode”).</span></span>

<span data-ttu-id="a767f-189">toodo appeler par conséquent, la méthode hello :</span><span class="sxs-lookup"><span data-stu-id="a767f-189">toodo so, call hello method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="a767f-190">l’argument Hello est une valeur dans **millisecondes**.</span><span class="sxs-lookup"><span data-stu-id="a767f-190">hello argument is a value in **milliseconds**.</span></span> <span data-ttu-id="a767f-191">À tout moment, si vous souhaitez que la journalisation en temps réel tooreactivate hello, appelez uniquement méthode hello sans paramètres ou avec la valeur de hello 0.</span><span class="sxs-lookup"><span data-stu-id="a767f-191">At any time, if you want tooreactivate hello real-time logging, just call hello method without any parameter, or with hello 0 value.</span></span>

<span data-ttu-id="a767f-192">Hello mode rafale légèrement augmenter la batterie de hello vie mais n’a un impact sur hello Engagement moniteur : toutes les sessions et les travaux seront arrondies toohello rafale seuil (par conséquent, les sessions et les travaux plus court que le seuil de croissance hello n’est pas forcément visible).</span><span class="sxs-lookup"><span data-stu-id="a767f-192">hello burst mode slightly increase hello battery life but has an impact on hello Engagement Monitor: all sessions and jobs duration will be rounded toohello burst threshold (thus, sessions and jobs shorter than hello burst threshold may not be visible).</span></span> <span data-ttu-id="a767f-193">Il est recommandé de toouse un seuil de croissance n’est plus à 30000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="a767f-193">It is recommended toouse a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="a767f-194">Vous avez toobe souvenez-vous des journaux enregistrés too300 limité des éléments.</span><span class="sxs-lookup"><span data-stu-id="a767f-194">You have toobe aware that saved logs are limited too300 items.</span></span> <span data-ttu-id="a767f-195">Si l'envoi est trop long, vous risquez de perdre certains journaux.</span><span class="sxs-lookup"><span data-stu-id="a767f-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="a767f-196">Hello rafale seuil ne peut pas être configuré période tooa inférieure à une seconde.</span><span class="sxs-lookup"><span data-stu-id="a767f-196">hello burst threshold cannot be configured tooa period lesser than one second.</span></span> <span data-ttu-id="a767f-197">Si vous essayez donc toodo, hello SDK affiche une trace avec l’erreur de hello et sera automatiquement réinitialise toohello par défaut, c'est-à-dire que zéro seconde.</span><span class="sxs-lookup"><span data-stu-id="a767f-197">If you try toodo so, hello SDK will show a trace with hello error and will automatically reset toohello default value, that is, zero seconds.</span></span> <span data-ttu-id="a767f-198">Cette opération déclenche hello SDK tooreport hello journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="a767f-198">This will trigger hello SDK tooreport hello logs in real-time.</span></span>
> 
> 

