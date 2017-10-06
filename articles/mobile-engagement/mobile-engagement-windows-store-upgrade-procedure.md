---
title: "aaaWindows procédures de mise à niveau Kit de développement logiciel des applications universelle"
description: "Procédures de mise à niveau du Kit de développement logiciel (SDK) des applications Windows Universal pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="4c834-103">Procédures de mise à niveau du Kit de développement logiciel (SDK) des applications Windows Universal</span><span class="sxs-lookup"><span data-stu-id="4c834-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="4c834-104">Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.</span><span class="sxs-lookup"><span data-stu-id="4c834-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="4c834-105">Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello.</span><span class="sxs-lookup"><span data-stu-id="4c834-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="4c834-106">Par exemple, si vous migrez à partir de 0.10.1 too0.11.0 avoir toofirst suivez hello » à partir de 0.9.0 too0.10.1 « procédure puis hello » à partir de 0.10.1 too0.11.0 « procédure.</span><span class="sxs-lookup"><span data-stu-id="4c834-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="4c834-107">À partir de 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="4c834-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="4c834-108">Journaux des tests</span><span class="sxs-lookup"><span data-stu-id="4c834-108">Test logs</span></span>
<span data-ttu-id="4c834-109">Journaux de la console produits par hello SDK peuvent être activé/désactivé/filtrées.</span><span class="sxs-lookup"><span data-stu-id="4c834-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="4c834-110">toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :</span><span class="sxs-lookup"><span data-stu-id="4c834-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="4c834-111">Ressources</span><span class="sxs-lookup"><span data-stu-id="4c834-111">Resources</span></span>
<span data-ttu-id="4c834-112">segment de recouvrement Hello portée a été améliorée.</span><span class="sxs-lookup"><span data-stu-id="4c834-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="4c834-113">Il fait partie des ressources de package NuGet du Kit de développement logiciel hello.</span><span class="sxs-lookup"><span data-stu-id="4c834-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="4c834-114">Lors de la mise à niveau toohello une nouvelle version du Kit de développement logiciel de hello, vous pouvez choisir que si vous souhaitez tookeep vos fichiers à partir de hello superposition dossier des ressources ou non :</span><span class="sxs-lookup"><span data-stu-id="4c834-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="4c834-115">Si l’utilisation de segment de recouvrement hello précédente pour vous ou vous intégrez hello `WebView` éléments manuellement vos fichiers de sortie, vous pouvez décider tookeep, il continuera de fonctionner.</span><span class="sxs-lookup"><span data-stu-id="4c834-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="4c834-116">Si vous souhaitez tooupdate toohello nouveau segment de recouvrement, hello suffit de remplacer toute `overlay` dossier à partir de vos ressources avec hello nouveau à partir du package SDK de hello (applications UWP : après la mise à niveau de hello, vous pouvez obtenir le nouveau dossier de superposition hello à partir de % USERPROFILE%\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="4c834-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="4c834-117">À l’aide de la superposition de nouveau hello remplace les personnalisations effectuées sur la version précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="4c834-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="4c834-118">À partir de 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="4c834-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="4c834-119">Ressources</span><span class="sxs-lookup"><span data-stu-id="4c834-119">Resources</span></span>
<span data-ttu-id="4c834-120">Cette étape concerne uniquement les ressources personnalisées.</span><span class="sxs-lookup"><span data-stu-id="4c834-120">This step concerns customized resources only.</span></span> <span data-ttu-id="4c834-121">Si vous avez personnalisé les ressources hello fournies par hello SDK (html, images, segment de recouvrement), vous avez toobackup avant la mise à niveau et appliquez à nouveau votre personnalisation sur mis à niveau ressources.</span><span class="sxs-lookup"><span data-stu-id="4c834-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="4c834-122">À partir de 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="4c834-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="4c834-123">Ressources</span><span class="sxs-lookup"><span data-stu-id="4c834-123">Resources</span></span>
<span data-ttu-id="4c834-124">Cette étape concerne uniquement les ressources personnalisées.</span><span class="sxs-lookup"><span data-stu-id="4c834-124">This step concerns customized resources only.</span></span> <span data-ttu-id="4c834-125">Si vous avez personnalisé les ressources hello fournies par hello SDK (html, images, segment de recouvrement), vous avez toobackup avant la mise à niveau et appliquez à nouveau votre personnalisation sur mis à niveau ressources.</span><span class="sxs-lookup"><span data-stu-id="4c834-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="4c834-126">l'intégration de vue web</span><span class="sxs-lookup"><span data-stu-id="4c834-126">Webview integration</span></span>
<span data-ttu-id="4c834-127">Certains facteurs de forme de périphérique différent toomatch améliorations ont été introduites dans cette version.</span><span class="sxs-lookup"><span data-stu-id="4c834-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="4c834-128">Assurez-vous que l’intégration de hello webview correspondent aux suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="4c834-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="4c834-129">Dans votre page XAML () :</span><span class="sxs-lookup"><span data-stu-id="4c834-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="4c834-130">Et dans votre fichier .cs associé :</span><span class="sxs-lookup"><span data-stu-id="4c834-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="4c834-131">À partir de 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="4c834-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="4c834-132">Ressources</span><span class="sxs-lookup"><span data-stu-id="4c834-132">Resources</span></span>
<span data-ttu-id="4c834-133">Cette étape concerne uniquement les ressources personnalisées.</span><span class="sxs-lookup"><span data-stu-id="4c834-133">This step concerns customized resources only.</span></span> <span data-ttu-id="4c834-134">Si vous avez personnalisé les ressources hello fournies par hello SDK (html, images, segment de recouvrement), vous avez toobackup avant la mise à niveau et appliquez à nouveau votre personnalisation sur mis à niveau ressources.</span><span class="sxs-lookup"><span data-stu-id="4c834-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="4c834-135">À partir de 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="4c834-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="4c834-136">Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4c834-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4c834-137">Capptain et Mobile Engagement sont hello pas les mêmes services et procédure hello fourni ci-dessous uniquement met en évidence comment toomigrate hello application cliente.</span><span class="sxs-lookup"><span data-stu-id="4c834-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="4c834-138">Migration hello SDK dans l’application hello ne fait pas migrer vos données des hello Capptain toohello Mobile Engagement serveurs</span><span class="sxs-lookup"><span data-stu-id="4c834-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="4c834-139">Si vous effectuez une migration à partir d’une version antérieure, veuillez consultez hello Capptain site web toomigrate too1.1.1 tout d’abord, appliquez hello procédure</span><span class="sxs-lookup"><span data-stu-id="4c834-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="4c834-140">Package NuGet</span><span class="sxs-lookup"><span data-stu-id="4c834-140">Nuget package</span></span>
<span data-ttu-id="4c834-141">Remplacez **Capptain.WindowsPhone** par le package NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="4c834-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="4c834-142">Application d'Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="4c834-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="4c834-143">Hello SDK utilise le terme de hello `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="4c834-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="4c834-144">Vous devez tooupdate toomatch de votre projet cette modification.</span><span class="sxs-lookup"><span data-stu-id="4c834-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="4c834-145">Vous devez toouninstall votre package nuget Capptain.</span><span class="sxs-lookup"><span data-stu-id="4c834-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="4c834-146">Considérez que toutes vos modifications dans le dossier de ressources Capptain seront supprimées.</span><span class="sxs-lookup"><span data-stu-id="4c834-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="4c834-147">Si vous souhaitez tookeep ces fichiers, faites une copie d’eux.</span><span class="sxs-lookup"><span data-stu-id="4c834-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="4c834-148">Après cela, installer le nouveau package de nuget Microsoft Azure Engagement hello sur votre projet.</span><span class="sxs-lookup"><span data-stu-id="4c834-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="4c834-149">Vous le trouverez directement sur le [site web NuGet].</span><span class="sxs-lookup"><span data-stu-id="4c834-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="4c834-150">ou ici.</span><span class="sxs-lookup"><span data-stu-id="4c834-150">or here index.</span></span> <span data-ttu-id="4c834-151">Ce remplace action tous les fichiers de ressources utilisées par l’Engagement et ajoute hello nouvelle DLL d’Engagement tooyour les références de projet.</span><span class="sxs-lookup"><span data-stu-id="4c834-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="4c834-152">Vous avez tooclean à vos références de projet et en supprimant les références Capptain DLL.</span><span class="sxs-lookup"><span data-stu-id="4c834-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="4c834-153">Si vous n’apportez pas cette option, version hello de Capptain est en conflit et erreur se produira.</span><span class="sxs-lookup"><span data-stu-id="4c834-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="4c834-154">Si vous avez personnalisé les ressources Capptain, copiez votre ancien contenu de fichiers et les coller dans des fichiers de Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="4c834-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="4c834-155">Notez que les fichiers xaml et cs ont toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4c834-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="4c834-156">Une fois ces étapes terminées il vous suffit tooreplace les anciennes références Capptain par nouvelles références d’Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="4c834-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="4c834-157">Tous les espaces de noms Capptain ont toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="4c834-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="4c834-158">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="4c834-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="4c834-159">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="4c834-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="4c834-160">Toutes les classes Capptain qui contiennent « Capptain » doivent contenir « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="4c834-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="4c834-161">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="4c834-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="4c834-162">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="4c834-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="4c834-163">Pour les fichiers xaml, les attributs et les espaces de noms Capptain changent également.</span><span class="sxs-lookup"><span data-stu-id="4c834-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="4c834-164">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="4c834-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="4c834-165">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="4c834-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="4c834-166">Modifications des pages de superposition</span><span class="sxs-lookup"><span data-stu-id="4c834-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="4c834-167">La superposition change également.</span><span class="sxs-lookup"><span data-stu-id="4c834-167">Overlay also changes.</span></span> <span data-ttu-id="4c834-168">Son nouvel espace de noms est `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="4c834-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="4c834-169">Il a toobe utilisé dans les fichiers xaml et cs.</span><span class="sxs-lookup"><span data-stu-id="4c834-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="4c834-170">En outre `CapptainGrid` toobe nommé `EngagementGrid`, `capptain_notification_content` et `capptain_announcement_content` sont nommés `engagement_notification_content` et `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="4c834-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="4c834-171">Pour la superposition :</span><span class="sxs-lookup"><span data-stu-id="4c834-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="4c834-172">Cela devient :</span><span class="sxs-lookup"><span data-stu-id="4c834-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="4c834-173">Pourquoi autres ressources telles que Capptain images et des fichiers HTML, notez qu’ils ont également été renommé toouse « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="4c834-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="4c834-174">Déclaration de projet</span><span class="sxs-lookup"><span data-stu-id="4c834-174">Project declaration</span></span>
<span data-ttu-id="4c834-175">Sur Package.appxmanifest, `File Type Associations` a été mis à jour à partir de :</span><span class="sxs-lookup"><span data-stu-id="4c834-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="4c834-176">capptain\_atteindre\_tooengagement contenu\_atteindre\_contenu</span><span class="sxs-lookup"><span data-stu-id="4c834-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="4c834-177">capptain\_journal\_tooengagement de fichiers\_journal\_fichier</span><span class="sxs-lookup"><span data-stu-id="4c834-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="4c834-178">ID de l'application / clé SDK</span><span class="sxs-lookup"><span data-stu-id="4c834-178">Application ID / SDK Key</span></span>
<span data-ttu-id="4c834-179">Engagement utilise une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="4c834-179">Engagement uses a connection string.</span></span> <span data-ttu-id="4c834-180">Vous n’avez pas toospecify un ID d’application et une clé de kit de développement logiciel avec Mobile Engagement, vous devez uniquement toospecify une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="4c834-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="4c834-181">Vous pouvez la configurer dans votre fichier EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="4c834-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="4c834-182">configuration d’Engagement Hello peut être définie dans votre `Resources\EngagementConfiguration.xml` le fichier de votre projet.</span><span class="sxs-lookup"><span data-stu-id="4c834-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="4c834-183">Modifiez cette toospecify de fichier :</span><span class="sxs-lookup"><span data-stu-id="4c834-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="4c834-184">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="4c834-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="4c834-185">Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :</span><span class="sxs-lookup"><span data-stu-id="4c834-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="4c834-186">chaîne de connexion Hello pour votre application s’affiche sur hello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="4c834-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="4c834-187">Changement de noms d'éléments</span><span class="sxs-lookup"><span data-stu-id="4c834-187">Items name change</span></span>
<span data-ttu-id="4c834-188">Tous les éléments nommés *capptain* ont été renommés *engagement*.</span><span class="sxs-lookup"><span data-stu-id="4c834-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="4c834-189">De même pour *Capptain* trop*Engagement*.</span><span class="sxs-lookup"><span data-stu-id="4c834-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="4c834-190">Exemples d'éléments Capptain couramment utilisés :</span><span class="sxs-lookup"><span data-stu-id="4c834-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="4c834-191">CapptainConfiguration se nomme maintenant EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="4c834-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="4c834-192">CapptainAgent se nomme maintenant EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="4c834-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="4c834-193">CapptainReach se nomme maintenant EngagementReach</span><span class="sxs-lookup"><span data-stu-id="4c834-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="4c834-194">CapptainHttpConfig se nomme maintenant EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="4c834-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="4c834-195">GetCapptainPageName se nomme maintenant GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="4c834-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="4c834-196">Notez que ce changement affecte également les méthodes substituées.</span><span class="sxs-lookup"><span data-stu-id="4c834-196">Note that rename also affects overridden methods.</span></span>

