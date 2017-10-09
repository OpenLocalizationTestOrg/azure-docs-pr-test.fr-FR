---
title: "aaaWindows Universal avancé Reporting avec MobileApps Engagement"
description: Comment tooIntegrate Azure Mobile Engagement avec les applications Windows universelles
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
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a><span data-ttu-id="37000-103">Création de rapports avancée avec hello universel applications Engagement Kit de développement</span><span class="sxs-lookup"><span data-stu-id="37000-103">Advanced Reporting with hello Windows Universal Apps Engagement SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="37000-104">Windows universel</span><span class="sxs-lookup"><span data-stu-id="37000-104">Universal Windows</span></span>](mobile-engagement-windows-store-advanced-reporting.md)
> * [<span data-ttu-id="37000-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="37000-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="37000-106">iOS</span><span class="sxs-lookup"><span data-stu-id="37000-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="37000-107">Android</span><span class="sxs-lookup"><span data-stu-id="37000-107">Android</span></span>](mobile-engagement-android-advanced-reporting.md)
> 
> 

<span data-ttu-id="37000-108">Cette rubrique décrit des scénarios de génération de rapports supplémentaires dans votre application Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="37000-108">This topic describes additional reporting scenarios in your Windows Universal application.</span></span> <span data-ttu-id="37000-109">Ces scénarios incluent les options que vous pouvez choisir d’application toohello tooapply créé Bonjour [mise en route](mobile-engagement-windows-store-dotnet-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="37000-109">These scenarios include options that you can choose tooapply toohello app created in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="37000-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="37000-110">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

<span data-ttu-id="37000-111">Avant de commencer ce didacticiel, vous devez d’abord terminer hello [mise en route](mobile-engagement-windows-store-dotnet-get-started.md) (didacticiel), qui est délibérément simple et directe.</span><span class="sxs-lookup"><span data-stu-id="37000-111">Before starting this tutorial, you must first complete hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) tutorial, which is deliberately direct and simple.</span></span> <span data-ttu-id="37000-112">Ce didacticiel présente les options supplémentaires vous pouvez choisir.</span><span class="sxs-lookup"><span data-stu-id="37000-112">This tutorial covers additional options you can choose from.</span></span>

## <a name="specifying-engagement-configuration-at-runtime"></a><span data-ttu-id="37000-113">Spécification de la configuration d’Engagement lors de l’exécution</span><span class="sxs-lookup"><span data-stu-id="37000-113">Specifying engagement configuration at runtime</span></span>
<span data-ttu-id="37000-114">configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet, c'est-à-dire où il a été spécifié dans hello [mise en route](mobile-engagement-windows-store-dotnet-get-started.md) rubrique.</span><span class="sxs-lookup"><span data-stu-id="37000-114">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project, which is where it was specified in hello [Getting Started](mobile-engagement-windows-store-dotnet-get-started.md) topic.</span></span>

<span data-ttu-id="37000-115">Mais vous pouvez également le spécifier lors de l’exécution : vous pouvez appeler hello méthode avant l’initialisation de l’agent hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="37000-115">But you can also specify it at runtime: you can call hello following method before hello Engagement agent initialization:</span></span>

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a><span data-ttu-id="37000-116">Méthode recommandée : surchargez vos classes `Page`</span><span class="sxs-lookup"><span data-stu-id="37000-116">Recommended method: overload your `Page` classes</span></span>
<span data-ttu-id="37000-117">tooactivate hello reporting de tous les journaux hello requis par Engagement toocompute utilisateurs, Sessions, activités, blocages et statistiques, effectuer tous les votre `Page` sous-classes héritent hello `EngagementPage` classes.</span><span class="sxs-lookup"><span data-stu-id="37000-117">tooactivate hello reporting of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, make all your `Page` sub-classes inherit from hello `EngagementPage` classes.</span></span>

<span data-ttu-id="37000-118">Voici un exemple appliqué à une page de votre application.</span><span class="sxs-lookup"><span data-stu-id="37000-118">Here is an example for a page of your application.</span></span> <span data-ttu-id="37000-119">Vous pouvez effectuer hello identiques pour toutes les pages de votre application.</span><span class="sxs-lookup"><span data-stu-id="37000-119">You can do hello same thing for all pages of your application.</span></span>

### <a name="c-source-file"></a><span data-ttu-id="37000-120">Fichier source C#</span><span class="sxs-lookup"><span data-stu-id="37000-120">C# Source file</span></span>
<span data-ttu-id="37000-121">Modifiez le fichier `.xaml.cs` de votre page :</span><span class="sxs-lookup"><span data-stu-id="37000-121">Modify your page `.xaml.cs` file:</span></span>

* <span data-ttu-id="37000-122">Ajouter tooyour `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="37000-122">Add tooyour `using` statements:</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="37000-123">Remplacez `Page` par `EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="37000-123">Replace `Page` with `EngagementPage`:</span></span>

<span data-ttu-id="37000-124">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="37000-124">**Without Engagement:**</span></span>

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

<span data-ttu-id="37000-125">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="37000-125">**With Engagement:**</span></span>

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage
          {
            [...]
          }
        }

> [!IMPORTANT]
> <span data-ttu-id="37000-126">Si votre page substitue hello `OnNavigatedTo` (méthode), être toocall vraiment `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="37000-126">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="37000-127">Sinon, activité hello n’est pas être signalé (hello `EngagementPage` appelle `StartActivity` à l’intérieur de son `OnNavigatedTo` méthode).</span><span class="sxs-lookup"><span data-stu-id="37000-127">Otherwise, hello activity is not be reported (hello `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span>
> 
> 

### <a name="xaml-file"></a><span data-ttu-id="37000-128">Fichier XAML</span><span class="sxs-lookup"><span data-stu-id="37000-128">XAML file</span></span>
<span data-ttu-id="37000-129">Modifiez le fichier `.xaml` de votre page :</span><span class="sxs-lookup"><span data-stu-id="37000-129">Modify your page `.xaml` file:</span></span>

* <span data-ttu-id="37000-130">Ajoutez les déclarations d’espaces de noms tooyour :</span><span class="sxs-lookup"><span data-stu-id="37000-130">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* <span data-ttu-id="37000-131">Remplacez `Page` par `engagement:EngagementPage` :</span><span class="sxs-lookup"><span data-stu-id="37000-131">Replace `Page` with `engagement:EngagementPage`:</span></span>

<span data-ttu-id="37000-132">**Sans Engagement :**</span><span class="sxs-lookup"><span data-stu-id="37000-132">**Without Engagement:**</span></span>

        <Page>
            <!-- layout -->
            ...
        </Page>

<span data-ttu-id="37000-133">**Avec Engagement :**</span><span class="sxs-lookup"><span data-stu-id="37000-133">**With Engagement:**</span></span>

        <engagement:EngagementPage
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

### <a name="override-hello-default-behaviour"></a><span data-ttu-id="37000-134">Substituer le comportement par défaut de hello</span><span class="sxs-lookup"><span data-stu-id="37000-134">Override hello default behaviour</span></span>
<span data-ttu-id="37000-135">Par défaut, nom de la classe de page de hello hello est signalée comme nom de l’activité hello, avec sans supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="37000-135">By default, hello class name of hello page is reported as hello activity name, with no extra.</span></span> <span data-ttu-id="37000-136">Si la classe hello utilise hello suffixe de « Page », l’Engagement le supprime.</span><span class="sxs-lookup"><span data-stu-id="37000-136">If hello class uses hello "Page" suffix, Engagement removes it.</span></span>

<span data-ttu-id="37000-137">toooverride par défaut hello pour le nom de hello, ajoutez ce code :</span><span class="sxs-lookup"><span data-stu-id="37000-137">toooverride hello default behavior for hello name, add this code:</span></span>

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

<span data-ttu-id="37000-138">tooreport des informations supplémentaires avec votre activité, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="37000-138">tooreport extra information with your activity, add this code:</span></span>

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

<span data-ttu-id="37000-139">Ces méthodes sont appelées dans hello `OnNavigatedTo` méthode de votre page.</span><span class="sxs-lookup"><span data-stu-id="37000-139">These methods are called from within hello `OnNavigatedTo` method of your page.</span></span>

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="37000-140">Autre méthode : appeler `StartActivity()` manuellement</span><span class="sxs-lookup"><span data-stu-id="37000-140">Alternate method: call `StartActivity()` manually</span></span>
<span data-ttu-id="37000-141">Si vous ne pouvez pas ou ne souhaitez pas que toooverload votre `Page` classes, vous pouvez démarrer à la place de vos activités en appelant `EngagementAgent` direct de méthodes.</span><span class="sxs-lookup"><span data-stu-id="37000-141">If you cannot or do not want toooverload your `Page` classes, you can instead start your activities by calling `EngagementAgent` methods directly.</span></span>

<span data-ttu-id="37000-142">Nous vous recommandons d'appeler `StartActivity` à l'intérieur de la méthode `OnNavigatedTo` de votre page.</span><span class="sxs-lookup"><span data-stu-id="37000-142">We recommend calling `StartActivity` inside your `OnNavigatedTo` method of your Page.</span></span>

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> <span data-ttu-id="37000-143">Assurez-vous de terminer votre session correctement.</span><span class="sxs-lookup"><span data-stu-id="37000-143">Ensure you end your session correctly.</span></span>
> 
> <span data-ttu-id="37000-144">Hello SDK Universal Windows appelle automatiquement hello `EndActivity` méthode lors de l’application hello est fermée.</span><span class="sxs-lookup"><span data-stu-id="37000-144">hello Windows Universal SDK automatically calls hello `EndActivity` method when hello application is closed.</span></span> <span data-ttu-id="37000-145">Par conséquent, il est **hautement** recommandé toocall hello `StartActivity` méthode chaque fois que l’activité hello d’utilisateur de hello modifier et trop**jamais** appel hello `EndActivity` (méthode).</span><span class="sxs-lookup"><span data-stu-id="37000-145">Thus, it is **HIGHLY** recommended toocall hello `StartActivity` method whenever hello activity of hello user change, and too**NEVER** call hello `EndActivity` method.</span></span> <span data-ttu-id="37000-146">Cette méthode notifie server d’Engagement hello que l’utilisateur actuel hello a quitté l’application hello, ce qui aura un impact sur tous les journaux d’application.</span><span class="sxs-lookup"><span data-stu-id="37000-146">This method notifies hello Engagement server that hello current user has left hello application, which will impact all application logs.</span></span>
> 
> 

## <a name="advanced-reporting"></a><span data-ttu-id="37000-147">Génération de rapports avancés</span><span class="sxs-lookup"><span data-stu-id="37000-147">Advanced reporting</span></span>
<span data-ttu-id="37000-148">Si vous le souhaitez, vous souhaiterez peut-être tooreport les événements spécifiques à l’application, les erreurs et les travaux, toodo donc, utilisez hello d’autres méthodes trouvés dans hello `EngagementAgent` classe.</span><span class="sxs-lookup"><span data-stu-id="37000-148">Optionally, you may want tooreport application-specific events, errors and jobs, toodo so, use hello others methods found in hello `EngagementAgent` class.</span></span> <span data-ttu-id="37000-149">Hello Engagement API autorise l’utilisation de fonctions avancées de tous les Engagement.</span><span class="sxs-lookup"><span data-stu-id="37000-149">hello Engagement API allows use of all Engagement's advanced capabilities.</span></span>

<span data-ttu-id="37000-150">Pour plus d’informations, consultez [comment toouse hello avancé Mobile Engagement marquage API dans votre application Windows universelle](mobile-engagement-windows-store-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="37000-150">For further information, see [How toouse hello advanced Mobile Engagement tagging API in your Windows Universal app](mobile-engagement-windows-store-use-engagement-api.md).</span></span>

