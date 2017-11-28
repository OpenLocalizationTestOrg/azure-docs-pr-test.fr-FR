---
title: "Génération de rapports avancés pour des applications Windows Universal avec Mobile Apps Engagement"
description: "Intégration du module Azure Mobile Engagement avec des applications universelles Windows"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: feac309db1ffce0945012e293bfc1df417aed876
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-reporting-with-the-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="5c936-103">Génération de rapports avancés avec le Kit de développement logiciel (SDK) des applications Windows Universal Engagement</span><span class="sxs-lookup"><span data-stu-id="5c936-103">Advanced Reporting with the Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5c936-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="5c936-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="5c936-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5c936-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="5c936-106">iOS</span><span class="sxs-lookup"><span data-stu-id="5c936-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="5c936-107">Android</span><span class="sxs-lookup"><span data-stu-id="5c936-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="5c936-108">Cette rubrique décrit des scénarios de génération de rapports supplémentaires dans votre application Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="5c936-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="5c936-109">Ces scénarios incluent des options que vous pouvez choisir d’intégrer à l’application créée dans le didacticiel [Prise en main](mobile-engagement-windows-store-dotnet-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="5c936-109">These scenarios include options that you can choose to apply to the app created in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c936-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="5c936-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="5c936-111">Avant de commencer ce didacticiel, vous devez suivre le didacticiel [Prise en main](mobile-engagement-windows-store-dotnet-get-started.md) , qui est délibérément direct et simple.</span><span class="sxs-lookup"><span data-stu-id="5c936-111">Before starting this tutorial, you must first complete the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="5c936-112">Ce didacticiel présente les options supplémentaires vous pouvez choisir.</span><span class="sxs-lookup"><span data-stu-id="5c936-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="5c936-113">Spécification de la configuration d’Engagement lors de l’exécution</span><span class="sxs-lookup"><span data-stu-id="5c936-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="5c936-114">La configuration d’Engagement est centralisée dans le fichier `Resources\EngagementConfiguration.xml` de votre projet, c’est-à-dire l’endroit où il a été spécifié dans la rubrique [Mise en route](mobile-engagement-windows-store-dotnet-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="5c936-114">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in the [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="5c936-115">Mais vous pouvez également le spécifier lors de l'exécution en appelant la méthode suivante avant l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="5c936-115">But you can also specify it at runtime: you can call the following method before the Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set the Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="5c936-116">Méthode recommandée : surchargez vos classes `Page`</span><span class="sxs-lookup"><span data-stu-id="5c936-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="5c936-117">Pour activer la génération de tous les journaux requis par Engagement pour calculer les statistiques concernant les utilisateurs, les sessions, les activités, les incidents et les informations techniques, configurez toutes vos sous-classes `Page` de manière à ce qu'elles héritent des classes `EngagementPage`.</span><span class="sxs-lookup"><span data-stu-id="5c936-117">To activate the reporting of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from the `EngagementPage` classes.</span></span>

<span data-ttu-id="5c936-118">Voici un exemple appliqué à une page de votre application.</span><span class="sxs-lookup"><span data-stu-id="5c936-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="5c936-119">Vous pouvez faire la même chose pour toutes les pages de votre application.</span><span class="sxs-lookup"><span data-stu-id="5c936-119">You can do the same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="5c936-120">Fichier source C#</span><span class="sxs-lookup"><span data-stu-id="5c936-120">C# Source file</span></span>
<span data-ttu-id="5c936-121">Modifiez le fichier `.xaml.cs` de votre page :</span><span class="sxs-lookup"><span data-stu-id="5c936-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="5c936-122">Ajoutez à vos instructions `using` :</span><span class="sxs-lookup"><span data-stu-id="5c936-122">Add to your `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="5c936-123">Remplacez `Page` par `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="5c936-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="5c936-124">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="5c936-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="5c936-125">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="5c936-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="5c936-126">Si votre page remplace la méthode `OnNavigatedTo`, veillez à appeler `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="5c936-126">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="5c936-127">Sinon, l'activité ne sera pas signalée (la `EngagementPage` appelle `StartActivity` à l'intérieur de sa méthode `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="5c936-127">Otherwise, the activity is not be reported (the `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="5c936-128">Fichier XAML</span><span class="sxs-lookup"><span data-stu-id="5c936-128">XAML file</span></span>
<span data-ttu-id="5c936-129">Modifiez le fichier `.xaml` de votre page :</span><span class="sxs-lookup"><span data-stu-id="5c936-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="5c936-130">Ajoutez une déclaration d'espace de noms :</span><span class="sxs-lookup"><span data-stu-id="5c936-130">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="5c936-131">Remplacez `Page` par `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="5c936-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="5c936-132">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="5c936-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="5c936-133">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="5c936-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-the-default-behaviour"></a><span data-ttu-id="5c936-134">Remplacer le comportement par défaut</span><span class="sxs-lookup"><span data-stu-id="5c936-134">Override the default behaviour</span></span>
<span data-ttu-id="5c936-135">Par défaut, le nom de classe de la page est signalé comme le nom de l'activité, sans informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="5c936-135">By default, the class name of the page is reported as the activity name, with no extra.</span></span> <span data-ttu-id="5c936-136">Si la classe utilise le suffixe « Page », Engagement le supprime également.</span><span class="sxs-lookup"><span data-stu-id="5c936-136">If the class uses the "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="5c936-137">Pour remplacer le comportement par défaut pour le nom, ajoutez ce code :</span><span class="sxs-lookup"><span data-stu-id="5c936-137">To override the default behavior for the name, add this code:</span></span>

        // in the .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="5c936-138">Pour signaler des informations supplémentaires avec votre activité, ajoutez ce code :</span><span class="sxs-lookup"><span data-stu-id="5c936-138">To report extra information with your activity, add this code:</span></span>

        // in the .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="5c936-139">Ces méthodes sont appelées depuis la méthode `OnNavigatedTo` de votre page.</span><span class="sxs-lookup"><span data-stu-id="5c936-139">These methods are called from within the `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="5c936-140">Autre méthode : appeler `StartActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="5c936-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="5c936-141">Si vous ne pouvez pas ou ne souhaitez pas surcharger vos classes `Page`, vous pouvez démarrer vos activités en appelant directement les méthodes `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="5c936-141">If you cannot or do not want to overload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="5c936-142">Nous vous recommandons d'appeler `StartActivity` à l'intérieur de la méthode `OnNavigatedTo` de votre page.</span><span class="sxs-lookup"><span data-stu-id="5c936-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="5c936-143">Assurez-vous de terminer votre session correctement.</span><span class="sxs-lookup"><span data-stu-id="5c936-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="5c936-144">Le Kit de développement logiciel Windows Universal appelle automatiquement la méthode `EndActivity` quand l'application est fermée.</span><span class="sxs-lookup"><span data-stu-id="5c936-144">The Windows Universal SDK automatically calls the `EndActivity` method when the application is closed.</span></span> <span data-ttu-id="5c936-145">Par conséquent, il est **FORTEMENT** recommandé d’appeler la méthode `StartActivity` chaque fois que l’activité de l’utilisateur change et de ne **JAMAIS** appeler la méthode `EndActivity`.</span><span class="sxs-lookup"><span data-stu-id="5c936-145">Thus, it is **HIGHLY** recommended to call the `StartActivity` method whenever the activity of the user change, and to **NEVER** call the `EndActivity` method.</span></span> <span data-ttu-id="5c936-146">Cette méthode informe le serveur Engagement que l'utilisateur actuel a quitté l'application, ce qui affectera tous les journaux d'application.</span><span class="sxs-lookup"><span data-stu-id="5c936-146">This method notifies the Engagement server that the current user has left the application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="5c936-147">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="5c936-147">Advanced reporting</span></span>
<span data-ttu-id="5c936-148">Vous pouvez éventuellement signaler les événements, erreurs et tâches spécifiques à l'application. Pour cela, utilisez les autres méthodes disponibles dans la classe `EngagementAgent`.</span><span class="sxs-lookup"><span data-stu-id="5c936-148">Optionally, you may want to report application-specific events, errors and jobs, to do so, use the others methods found in the `EngagementAgent` class.</span></span> <span data-ttu-id="5c936-149">L'API Engagement permet d'utiliser toutes les fonctionnalités avancées d'Engagement.</span><span class="sxs-lookup"><span data-stu-id="5c936-149">The Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="5c936-150">Pour plus d'informations, consultez [Utilisation de l'API de marquage avancée Mobile Engagement dans votre application Windows Phone](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="5c936-150">For further information, see [How to use the advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

