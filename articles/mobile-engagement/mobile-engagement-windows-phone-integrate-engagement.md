---
title: "Intégration du Kit de développement logiciel (SDK) d’Engagement Windows Phone Silverlight"
description: "Intégration du module Azure Mobile Engagement avec des applications Windows Phone Silverlight"
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
ms.openlocfilehash: 29b18aecff783cebf617995e2a19f16f0b68b51b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a><span data-ttu-id="15124-103">Intégration du Kit de développement logiciel (SDK) d’Engagement Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="15124-103">Windows Phone Silverlight Engagement SDK Integration</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="15124-104">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="15124-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md) 
> * [<span data-ttu-id="15124-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="15124-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [<span data-ttu-id="15124-106">iOS</span><span class="sxs-lookup"><span data-stu-id="15124-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md) 
> * [<span data-ttu-id="15124-107">Android</span><span class="sxs-lookup"><span data-stu-id="15124-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md) 
> 
> 

<span data-ttu-id="15124-108">Cette procédure décrit la méthode la plus simple pour activer les fonctions d’analyse et de surveillance d’Azure Mobile Engagement dans votre application Windows Phone Silverlight.</span><span class="sxs-lookup"><span data-stu-id="15124-108">This procedure describes the simplest way to activate Azure Mobile Engagement's Analytics and Monitoring functions in your Windows Phone Silverlight application.</span></span>

<span data-ttu-id="15124-109">Les étapes suivantes permettent d'activer la génération des journaux nécessaires pour calculer toutes les statistiques concernant les utilisateurs, les sessions, les activités, les incidents et les informations techniques.</span><span class="sxs-lookup"><span data-stu-id="15124-109">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="15124-110">La génération des journaux nécessaires au calcul d’autres statistiques, telles que les événements, les erreurs et les travaux, doit être effectuée manuellement à l’aide de l’API Engagement (consultez [Utilisation avancée de l’API de marquage Mobile Engagement dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md) ci-dessous), dans la mesure où ces statistiques dépendent de l’application.</span><span class="sxs-lookup"><span data-stu-id="15124-110">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API (see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md) below) since these statistics are application-dependent.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="15124-111">Versions prises en charge</span><span class="sxs-lookup"><span data-stu-id="15124-111">Supported versions</span></span>
<span data-ttu-id="15124-112">Le Kit de développement logiciel Mobile Engagement pour Windows Silverlight peut uniquement être intégré dans les applications ciblant :</span><span class="sxs-lookup"><span data-stu-id="15124-112">The Mobile Engagement SDK for Windows Silverlight can only be integrated into applications targeting :</span></span>

* <span data-ttu-id="15124-113">Windows Phone 8.0</span><span class="sxs-lookup"><span data-stu-id="15124-113">Windows Phone 8.0</span></span>
* <span data-ttu-id="15124-114">Windows Phone 8.1 Silverlight</span><span class="sxs-lookup"><span data-stu-id="15124-114">Windows Phone 8.1 Silverlight</span></span>

> [!NOTE]
> <span data-ttu-id="15124-115">Si vous ciblez Windows Phone 8.1 (non-Silverlight), consultez la rubrique [Procédure d’intégration de Windows Universal](mobile-engagement-windows-store-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="15124-115">If you are targeting Windows Phone 8.1 (non-Silverlight) then refer to the [Windows Universal integration procedure](mobile-engagement-windows-store-integrate-engagement.md).</span></span>
> 
> 

## <a name="install-the-mobile-engagement-silverlight-sdk"></a><span data-ttu-id="15124-116">Installer le Kit de développement logiciel Mobile Engagement Silverlight</span><span class="sxs-lookup"><span data-stu-id="15124-116">Install the Mobile Engagement Silverlight SDK</span></span>
<span data-ttu-id="15124-117">Le Kit de développement Mobile Engagement pour Windows Silverlight est disponible comme package Nuget appelé *MicrosoftAzure.MobileEngagement*.</span><span class="sxs-lookup"><span data-stu-id="15124-117">The Mobile Engagement SDK for Windows Silverlight is available as a Nuget package called *MicrosoftAzure.MobileEngagement*.</span></span> <span data-ttu-id="15124-118">Vous pouvez l'installer à partir du gestionnaire de package Nuget Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="15124-118">You can install it from the Visual Studio Nuget Package Manager.</span></span> 

## <a name="add-the-capabilities"></a><span data-ttu-id="15124-119">Ajouter les fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="15124-119">Add the capabilities</span></span>
<span data-ttu-id="15124-120">Le SDK Engagement a besoin de certaines fonctionnalités du SDK Windows Phone Silverlight pour pouvoir fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="15124-120">The Engagement SDK needs some capabilities of the Windows Phone Silverlight SDK in order to work properly.</span></span>

<span data-ttu-id="15124-121">Ouvrez votre fichier `WMAppManifest.xml` et assurez-vous que les fonctionnalités suivantes sont indiquées dans le volet `Capabilities` :</span><span class="sxs-lookup"><span data-stu-id="15124-121">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared in the `Capabilities` panel:</span></span>

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="15124-122">Initialiser le SDK Engagement</span><span class="sxs-lookup"><span data-stu-id="15124-122">Initialize the Engagement SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="15124-123">Configuration d'Engagement</span><span class="sxs-lookup"><span data-stu-id="15124-123">Engagement configuration</span></span>
<span data-ttu-id="15124-124">La configuration d'Engagement est centralisée dans le fichier `Resources\EngagementConfiguration.xml` de votre projet.</span><span class="sxs-lookup"><span data-stu-id="15124-124">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="15124-125">Modifiez ce fichier pour spécifier :</span><span class="sxs-lookup"><span data-stu-id="15124-125">Edit this file to specify :</span></span>

* <span data-ttu-id="15124-126">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="15124-126">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="15124-127">Si vous souhaitez plutôt la spécifier au moment de l'exécution, vous pouvez appeler la méthode suivante avant l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="15124-127">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

<span data-ttu-id="15124-128">La chaîne de connexion de votre application est affichée sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="15124-128">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="engagement-initialization"></a><span data-ttu-id="15124-129">Initialisation d'Engagement</span><span class="sxs-lookup"><span data-stu-id="15124-129">Engagement initialization</span></span>
<span data-ttu-id="15124-130">Quand vous créez un projet, un fichier `App.xaml.cs` est généré.</span><span class="sxs-lookup"><span data-stu-id="15124-130">When you create a new project, a `App.xaml.cs` file is generated.</span></span> <span data-ttu-id="15124-131">Cette classe hérite de `Application` et contient de nombreuses méthodes importantes.</span><span class="sxs-lookup"><span data-stu-id="15124-131">This class inherits from `Application` and contains many important methods.</span></span> <span data-ttu-id="15124-132">Son rôle consiste également à initialiser le SDK Engagement.</span><span class="sxs-lookup"><span data-stu-id="15124-132">It will also be used to initialize the Engagement SDK.</span></span>

<span data-ttu-id="15124-133">Modifiez le fichier `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="15124-133">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="15124-134">Ajoutez à vos instructions `using` :</span><span class="sxs-lookup"><span data-stu-id="15124-134">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="15124-135">Insérez `EngagementAgent.Instance.Init` dans la méthode `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="15124-135">Insert `EngagementAgent.Instance.Init` in the `Application_Launching` method :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* <span data-ttu-id="15124-136">Insérez `EngagementAgent.Instance.OnActivated` dans la méthode `Application_Activated` :</span><span class="sxs-lookup"><span data-stu-id="15124-136">Insert `EngagementAgent.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> <span data-ttu-id="15124-137">Nous vous déconseillons fortement d'ajouter l'initialisation d'Engagement à un autre endroit de votre application.</span><span class="sxs-lookup"><span data-stu-id="15124-137">We strongly discourage you to add the Engagement initialization in another place of your application.</span></span> <span data-ttu-id="15124-138">Toutefois, sachez que la méthode `EngagementAgent.Instance.Init` s'exécute sur un thread dédié et non sur le thread d'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="15124-138">However, be aware that the `EngagementAgent.Instance.Init` method runs on a dedicated thread, and not on the UI thread.</span></span>
> 
> 

## <a name="basic-reporting"></a><span data-ttu-id="15124-139">Génération de rapports de base</span><span class="sxs-lookup"><span data-stu-id="15124-139">Basic reporting</span></span>
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a><span data-ttu-id="15124-140">Méthode recommandée : surchargez vos classes `PhoneApplicationPage`</span><span class="sxs-lookup"><span data-stu-id="15124-140">Recommended method : overload your `PhoneApplicationPage` classes</span></span>
<span data-ttu-id="15124-141">Pour activer la génération de tous les journaux requis par Engagement pour calculer les statistiques concernant les utilisateurs, les sessions, les activités, les incidents et les informations techniques, vous pouvez simplement configurer toutes vos sous-classes `PhoneApplicationPage` de manière à ce qu'elles héritent des classes `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="15124-141">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `PhoneApplicationPage` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="15124-142">Voici un exemple qui montre comment procéder pour une page de votre application.</span><span class="sxs-lookup"><span data-stu-id="15124-142">Here is an example of how to do this for a page of your application.</span></span> <span data-ttu-id="15124-143">Vous pouvez faire la même chose pour toutes les pages de votre application.</span><span class="sxs-lookup"><span data-stu-id="15124-143">You can do the same thing for all pages of your application.</span></span>

#### <a name="c-source-file"></a><span data-ttu-id="15124-144">Fichier source C#</span><span class="sxs-lookup"><span data-stu-id="15124-144">C# Source file</span></span>
<span data-ttu-id="15124-145">Modifiez le fichier `.xaml.cs` de votre page :</span><span class="sxs-lookup"><span data-stu-id="15124-145">Modify your page `.xaml.cs` file :</span></span>

* <span data-ttu-id="15124-146">Ajoutez à vos instructions `using` :</span><span class="sxs-lookup"><span data-stu-id="15124-146">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="15124-147">Remplacez `PhoneApplicationPage` par `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="15124-147">Replace `PhoneApplicationPage` with `EngagementPage` :</span></span>

<span data-ttu-id="15124-148">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="15124-148">**Without Engagement:**</span></span>

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

<span data-ttu-id="15124-149">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="15124-149">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> <span data-ttu-id="15124-150">Si votre page hérite de la méthode `OnNavigatedTo`, veillez à laisser l'appel `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="15124-150">If your page inherits from the `OnNavigatedTo` method, be careful to let the `base.OnNavigatedTo(e)` call.</span></span> <span data-ttu-id="15124-151">Sinon, l'activité ne sera pas signalée.</span><span class="sxs-lookup"><span data-stu-id="15124-151">Otherwise, the activity will not be reported.</span></span> <span data-ttu-id="15124-152">En effet, l'appel `EngagementPage` invoque `StartActivity` à l'intérieur de la méthode `OnNavigatedTo`.</span><span class="sxs-lookup"><span data-stu-id="15124-152">Indeed, the `EngagementPage` is calling `StartActivity` inside the `OnNavigatedTo` method.</span></span>
> 
> 

#### <a name="xaml-file"></a><span data-ttu-id="15124-153">Fichier XAML</span><span class="sxs-lookup"><span data-stu-id="15124-153">XAML file</span></span>
<span data-ttu-id="15124-154">Modifiez le fichier `.xaml` de votre page :</span><span class="sxs-lookup"><span data-stu-id="15124-154">Modify your page `.xaml` file :</span></span>

* <span data-ttu-id="15124-155">Ajoutez à vos déclarations d'espaces de noms :</span><span class="sxs-lookup"><span data-stu-id="15124-155">Add to your namespaces declarations :</span></span>
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* <span data-ttu-id="15124-156">Remplacez `phone:PhoneApplicationPage` par `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="15124-156">Replace `phone:PhoneApplicationPage` with `engagement:EngagementPage` :</span></span>

<span data-ttu-id="15124-157">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="15124-157">**Without Engagement:**</span></span>

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

<span data-ttu-id="15124-158">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="15124-158">**With Engagement:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-the-default-behavior"></a><span data-ttu-id="15124-159">Remplacement du comportement par défaut</span><span class="sxs-lookup"><span data-stu-id="15124-159">Override the default behavior</span></span>
<span data-ttu-id="15124-160">Par défaut, le nom de classe de la page est signalé comme le nom de l'activité, sans informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="15124-160">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="15124-161">Si la classe utilise le suffixe « Page », Engagement le supprime également.</span><span class="sxs-lookup"><span data-stu-id="15124-161">If the class uses the "Page" suffix, Engagement will also remove it.</span></span>

<span data-ttu-id="15124-162">Si vous souhaitez remplacer le comportement par défaut pour le nom, ajoutez simplement ceci à votre code :</span><span class="sxs-lookup"><span data-stu-id="15124-162">If you want to override the default behavior for the name, simply add this to your code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

<span data-ttu-id="15124-163">Si vous souhaitez signaler des informations supplémentaires avec votre activité, vous pouvez ajouter ceci à votre code :</span><span class="sxs-lookup"><span data-stu-id="15124-163">If you want to report some extra information with your activity, you can add this to your code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

<span data-ttu-id="15124-164">Ces méthodes sont appelées depuis la méthode `OnNavigatedTo` de votre page.</span><span class="sxs-lookup"><span data-stu-id="15124-164">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="15124-165">Autre méthode : appeler `StartActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="15124-165">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="15124-166">Si vous ne pouvez pas ou ne souhaitez pas surcharger vos classes `PhoneApplicationPage`, vous pouvez démarrer vos activités en appelant directement les méthodes `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="15124-166">If you cannot or do not want to overload your `PhoneApplicationPage` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="15124-167">Nous vous recommandons d’appeler `StartActivity` à l’intérieur de la méthode `OnNavigatedTo` de votre PhoneApplicationPage.</span><span class="sxs-lookup"><span data-stu-id="15124-167">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your PhoneApplicationPage.</span></span>

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> <span data-ttu-id="15124-168">Assurez-vous de terminer votre session correctement.</span><span class="sxs-lookup"><span data-stu-id="15124-168">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="15124-169">Le Kit de développement logiciel (SDK) appelle automatiquement la méthode `EndActivity` à la fermeture de l'application.</span><span class="sxs-lookup"><span data-stu-id="15124-169">The SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="15124-170">Par conséquent, il est **FORTEMENT** recommandé d’appeler la méthode `StartActivity` chaque fois que l’activité de l’utilisateur change et de ne **JAMAIS** appeler la méthode `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="15124-170">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="15124-171">Cette méthode envoie un message au serveur Engagement indiquant que l'utilisateur actuel a quitté l'application et cela affecte tous les journaux d'application.</span><span class="sxs-lookup"><span data-stu-id="15124-171">This method sends a message to the Engagement server that the current user has left the application and this impacts all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="15124-172">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="15124-172">Advanced reporting</span></span>
<span data-ttu-id="15124-173">Vous pouvez éventuellement signaler les événements, erreurs et tâches spécifiques à l'application. Pour cela, utilisez les autres méthodes disponibles dans la classe `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="15124-173">Optionally, you may want to report application specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="15124-174">L'API Engagement permet d'utiliser toutes les fonctionnalités avancées d'Engagement.</span><span class="sxs-lookup"><span data-stu-id="15124-174">The Engagement API allows to use all of Engagement's advanced capabilities.</span></span>

<span data-ttu-id="15124-175">Pour plus d'informations, consultez la rubrique [Utilisation de l'API de marquage avancée Mobile Engagement dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="15124-175">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Phone Silverlight app](mobile-engagement-windows-phone-use-engagement-api.md).</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="15124-176">Configuration avancée</span><span class="sxs-lookup"><span data-stu-id="15124-176">Advanced configuration</span></span>
### <a name="disable-automatic-crash-reporting"></a><span data-ttu-id="15124-177">Désactiver le signalement automatique des incidents</span><span class="sxs-lookup"><span data-stu-id="15124-177">Disable automatic crash reporting</span></span>
<span data-ttu-id="15124-178">Vous pouvez désactiver la fonctionnalité de signalement automatique des incidents d'Engagement.</span><span class="sxs-lookup"><span data-stu-id="15124-178">You can disable the automatic crash reporting feature of Engagement.</span></span> <span data-ttu-id="15124-179">Dans ce cas, si une exception non gérée se produit, Engagement ne fait rien.</span><span class="sxs-lookup"><span data-stu-id="15124-179">Then, when an unhandled exception will occur, Engagement won't do anything.</span></span>

> [!WARNING]
> <span data-ttu-id="15124-180">Si vous envisagez de désactiver cette fonctionnalité, sachez que si un incident non pris en charge se produit dans votre application, Engagement n'enverra pas l'incident **ET** ne fermera ni la session ni les tâches.</span><span class="sxs-lookup"><span data-stu-id="15124-180">If you plan to disable this feature, be aware that when a unhandled crash will occur in your app, Engagement will not send the crash **AND** it will not close the session and jobs.</span></span>
> 
> 

<span data-ttu-id="15124-181">Pour désactiver le signalement automatique d'incident, il suffit de personnaliser votre configuration en fonction de la façon dont vous l'avez déclaré :</span><span class="sxs-lookup"><span data-stu-id="15124-181">To disable automatic crash reporting, just customize your configuration depending on the way you declared it :</span></span>

#### <a name="from-engagementconfigurationxml-file"></a><span data-ttu-id="15124-182">Dans le fichier `EngagementConfiguration.xml`</span><span class="sxs-lookup"><span data-stu-id="15124-182">From `EngagementConfiguration.xml` file</span></span>
<span data-ttu-id="15124-183">Affectez au signalement des incidents la valeur `false` entre les balises `<reportCrash>` et `</reportCrash>`.</span><span class="sxs-lookup"><span data-stu-id="15124-183">Set report crash to `false` between `<reportCrash>` and `</reportCrash>` tags.</span></span>

#### <a name="from-engagementconfiguration-object-at-run-time"></a><span data-ttu-id="15124-184">Dans l'objet `EngagementConfiguration` au moment l'exécution</span><span class="sxs-lookup"><span data-stu-id="15124-184">From `EngagementConfiguration` object at run time</span></span>
<span data-ttu-id="15124-185">Affectez au signalement des incidents la valeur false à l'aide de votre objet EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="15124-185">Set report crash to false using your EngagementConfiguration object.</span></span>

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a><span data-ttu-id="15124-186">Mode rafale</span><span class="sxs-lookup"><span data-stu-id="15124-186">Burst mode</span></span>
<span data-ttu-id="15124-187">Par défaut, le service Engagement génère des journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="15124-187">By default, the Engagement service reports logs in real time.</span></span> <span data-ttu-id="15124-188">Si votre application génère très fréquemment des journaux, il est préférable de les mettre en mémoire tampon et de les générer tous en même temps à intervalles réguliers (« mode rafale »).</span><span class="sxs-lookup"><span data-stu-id="15124-188">If your application reports logs very frequently, it is better to buffer the logs and to report them all at once on a regular time base (this is called the “burst mode”).</span></span>

<span data-ttu-id="15124-189">Pour cela, appelez la méthode :</span><span class="sxs-lookup"><span data-stu-id="15124-189">To do so, call the method:</span></span>

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

<span data-ttu-id="15124-190">L'argument est une valeur en **millisecondes**.</span><span class="sxs-lookup"><span data-stu-id="15124-190">The argument is a value in **milliseconds**.</span></span> <span data-ttu-id="15124-191">Si vous souhaitez réactiver la génération de journaux en temps réel, vous pouvez appeler à tout moment la méthode sans aucun paramètre ou avec la valeur 0.</span><span class="sxs-lookup"><span data-stu-id="15124-191">At any time, if you want to reactivate the real-time logging, just call the method without any parameter, or with the 0 value.</span></span>

<span data-ttu-id="15124-192">Le mode rafale accroît légèrement l'autonomie de la batterie, mais il affecte aussi Engagement Monitor. En effet, la durée des sessions et des tâches est arrondie au seuil de rafale (les sessions et les tâches plus courtes que le seuil de rafale ne sont donc pas visibles).</span><span class="sxs-lookup"><span data-stu-id="15124-192">The burst mode slightly increase the battery life but has an impact on the Engagement Monitor: all sessions and jobs duration will be rounded to the burst threshold (thus, sessions and jobs shorter than the burst threshold may not be visible).</span></span> <span data-ttu-id="15124-193">Il est recommandé d'utiliser un seuil de rafale inférieur à 30 000 (30 s).</span><span class="sxs-lookup"><span data-stu-id="15124-193">It is recommended to use a burst threshold no longer than 30000 (30s).</span></span> <span data-ttu-id="15124-194">Vous devez savoir que les journaux enregistrés sont limités à 300 entrées.</span><span class="sxs-lookup"><span data-stu-id="15124-194">You have to be aware that saved logs are limited to 300 items.</span></span> <span data-ttu-id="15124-195">Si l'envoi est trop long, vous risquez de perdre certains journaux.</span><span class="sxs-lookup"><span data-stu-id="15124-195">If sending is too long you can lose some logs.</span></span>

> [!WARNING]
> <span data-ttu-id="15124-196">Il n'est pas possible de configurer un seuil de rafale inférieur à une seconde.</span><span class="sxs-lookup"><span data-stu-id="15124-196">The burst threshold cannot be configured to a period lesser than one second.</span></span> <span data-ttu-id="15124-197">Si vous essayez de le faire, le SDK affichera une erreur et réinitialisera automatiquement la valeur par défaut, c'est-à-dire zéro seconde.</span><span class="sxs-lookup"><span data-stu-id="15124-197">If you try to do so, the SDK will show a trace with the error and will automatically reset to the default value, that is, zero seconds.</span></span> <span data-ttu-id="15124-198">Le SDK génère alors les journaux en temps réel.</span><span class="sxs-lookup"><span data-stu-id="15124-198">This will trigger the SDK to report the logs in real-time.</span></span>
> 
> 

