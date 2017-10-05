---
title: "Procédures de mise à niveau du Kit de développement logiciel (SDK) des applications Windows Universal"
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
ms.openlocfilehash: fe85a99a92fb39082cafe7422b356de1f20f14bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="fddff-103">Procédures de mise à niveau du Kit de développement logiciel (SDK) des applications Windows Universal</span><span class="sxs-lookup"><span data-stu-id="fddff-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="fddff-104">Si vous avez déjà intégré une version antérieure d'Engagement dans votre application, vous devez prendre en compte les points suivants lors de la mise à niveau du Kit de développement logiciel.</span><span class="sxs-lookup"><span data-stu-id="fddff-104">If you already have integrated an older version of Engagement into your application, you have to consider the following points when upgrading the SDK.</span></span>

<span data-ttu-id="fddff-105">Vous devrez peut-être suivre quelques procédures si vous avez manqué plusieurs versions du kit SDK.</span><span class="sxs-lookup"><span data-stu-id="fddff-105">You may have to follow several procedures if you missed several versions of the SDK.</span></span> <span data-ttu-id="fddff-106">Par exemple, si vous migrez de la version 0.10.1 vers 0.11.0, vous devez tout d'abord suivre la procédure « Migration de 0.9.0 vers 0.10.1 », puis la procédure « Migration de 0.10.1 vers 0.11.0 ».</span><span class="sxs-lookup"><span data-stu-id="fddff-106">For example if you migrate from 0.10.1 to 0.11.0 you have to first follow the "from 0.9.0 to 0.10.1" procedure then the "from 0.10.1 to 0.11.0" procedure.</span></span>

## <a name="from-330-to-340"></a><span data-ttu-id="fddff-107">Migration de 3.3.0 vers 3.4.0</span><span class="sxs-lookup"><span data-stu-id="fddff-107">From 3.3.0 to 3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="fddff-108">Journaux des tests</span><span class="sxs-lookup"><span data-stu-id="fddff-108">Test logs</span></span>
<span data-ttu-id="fddff-109">Les journaux de console produits par le Kit de développement logiciel (SDK) peuvent maintenant être activés/désactivés/filtrés.</span><span class="sxs-lookup"><span data-stu-id="fddff-109">Console logs produced by the SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="fddff-110">Pour personnaliser ce résultat, mettez à jour la propriété `EngagementAgent.Instance.TestLogEnabled` avec une des valeurs disponibles à partir de l'énumération `EngagementTestLogLevel`, par exemple :</span><span class="sxs-lookup"><span data-stu-id="fddff-110">To customize this, update the property `EngagementAgent.Instance.TestLogEnabled` to one of the value available from the `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="fddff-111">Ressources</span><span class="sxs-lookup"><span data-stu-id="fddff-111">Resources</span></span>
<span data-ttu-id="fddff-112">La superposition Reach a été améliorée.</span><span class="sxs-lookup"><span data-stu-id="fddff-112">The Reach overlay has been improved.</span></span> <span data-ttu-id="fddff-113">Elle fait partie des ressources du package NuGet du Kit de développement logiciel (SDK).</span><span class="sxs-lookup"><span data-stu-id="fddff-113">It is part of the SDK NuGet package resources.</span></span>

<span data-ttu-id="fddff-114">Lors de la mise à niveau vers la nouvelle version du Kit de développement logiciel (SDK), vous pouvez choisir de conserver ou non les fichiers existants dans le dossier de superposition de vos ressources :</span><span class="sxs-lookup"><span data-stu-id="fddff-114">While upgrading to the new version of the SDK you can choose whether you want to keep your existing files from the overlay folder of your resources or not:</span></span>

* <span data-ttu-id="fddff-115">Si la superposition précédente vous convient ou que vous intégrez manuellement les éléments `WebView` , vous pouvez choisir de conserver vos fichiers existants car ils resteront opérationnels.</span><span class="sxs-lookup"><span data-stu-id="fddff-115">If the previous overlay is working for you or you are integrating the `WebView` elements manually then you can decide to keep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="fddff-116">Si vous souhaitez effectuer la mise à jour vers la nouvelle superposition, remplacez simplement l’ensemble du dossier `overlay` contenant vos ressources par le nouveau dossier contenant le package du Kit de développement logiciel (SDK) (applications UWP : après la mise à niveau, vous trouverez le nouveau dossier de superposition sous %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="fddff-116">If you want to update to the new overlay, just replace the whole `overlay` folder from your resources with the new one from the SDK package (UWP apps: after the upgrade, you can get the new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="fddff-117">L’utilisation de la nouvelle superposition remplacera toutes les personnalisations apportées à la version précédente.</span><span class="sxs-lookup"><span data-stu-id="fddff-117">Using the new overlay will overwrite any customizations made on the previous version.</span></span>
> 
> 

## <a name="from-320-to-330"></a><span data-ttu-id="fddff-118">De 3.2.0 à 3.3.0</span><span class="sxs-lookup"><span data-stu-id="fddff-118">From 3.2.0 to 3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="fddff-119">Ressources</span><span class="sxs-lookup"><span data-stu-id="fddff-119">Resources</span></span>
<span data-ttu-id="fddff-120">Cette étape concerne uniquement les ressources personnalisées.</span><span class="sxs-lookup"><span data-stu-id="fddff-120">This step concerns customized resources only.</span></span> <span data-ttu-id="fddff-121">Si vous avez personnalisé les ressources fournies par le Kit de développement logiciel (HTML, images, superposition), vous devez ensuite les sauvegarder avant de les mettre à niveau et réappliquer votre personnalisation sur les ressources mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="fddff-121">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-to-320"></a><span data-ttu-id="fddff-122">De 3.1.0 à 3.2.0</span><span class="sxs-lookup"><span data-stu-id="fddff-122">From 3.1.0 to 3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="fddff-123">Ressources</span><span class="sxs-lookup"><span data-stu-id="fddff-123">Resources</span></span>
<span data-ttu-id="fddff-124">Cette étape concerne uniquement les ressources personnalisées.</span><span class="sxs-lookup"><span data-stu-id="fddff-124">This step concerns customized resources only.</span></span> <span data-ttu-id="fddff-125">Si vous avez personnalisé les ressources fournies par le Kit de développement logiciel (HTML, images, superposition), vous devez ensuite les sauvegarder avant de les mettre à niveau et réappliquer votre personnalisation sur les ressources mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="fddff-125">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="fddff-126">l'intégration de vue web</span><span class="sxs-lookup"><span data-stu-id="fddff-126">Webview integration</span></span>
<span data-ttu-id="fddff-127">Certaines améliorations pour la correspondance des facteurs de forme d'appareil ont été introduites dans cette version.</span><span class="sxs-lookup"><span data-stu-id="fddff-127">Some improvements to match different device form factors were introduced in this version.</span></span> <span data-ttu-id="fddff-128">Assurez-vous que votre intégration de la vue Web correspond à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="fddff-128">Make sure that your integration of the webview match the following:</span></span>

<span data-ttu-id="fddff-129">Dans votre page XAML () :</span><span class="sxs-lookup"><span data-stu-id="fddff-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="fddff-130">Et dans votre fichier .cs associé :</span><span class="sxs-lookup"><span data-stu-id="fddff-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated to within a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

              #region to implement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update the webview when the app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update the webview when the app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure to detach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are the current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements to the correct size.
              /// </summary>
              /// <param name="width">The width of your current display.</param>
              /// <param name="height">The height of your current display.</param>
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
              /// Handler that takes the Windows.Current.SizeChanged and indicates that webviews have to be resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes the ApplicationView.VisibleBoundsChanged and indicates that webviews have to be resized
              /// </summary>
              /// <param name="sender">The related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements to the correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-to-300"></a><span data-ttu-id="fddff-131">Migration de 2.0.0 vers 3.0.0</span><span class="sxs-lookup"><span data-stu-id="fddff-131">From 2.0.0 to 3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="fddff-132">Ressources</span><span class="sxs-lookup"><span data-stu-id="fddff-132">Resources</span></span>
<span data-ttu-id="fddff-133">Cette étape concerne uniquement les ressources personnalisées.</span><span class="sxs-lookup"><span data-stu-id="fddff-133">This step concerns customized resources only.</span></span> <span data-ttu-id="fddff-134">Si vous avez personnalisé les ressources fournies par le Kit de développement logiciel (HTML, images, superposition), vous devez ensuite les sauvegarder avant de les mettre à niveau et réappliquer votre personnalisation sur les ressources mises à niveau.</span><span class="sxs-lookup"><span data-stu-id="fddff-134">If you have customized the resources provided by the SDK (html, images, overlay) then you have to backup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-to-200"></a><span data-ttu-id="fddff-135">Migration de 1.1.1 vers 2.0.0</span><span class="sxs-lookup"><span data-stu-id="fddff-135">From 1.1.1 to 2.0.0</span></span>
<span data-ttu-id="fddff-136">La section qui suit décrit comment migrer une intégration du SDK à partir du service Capptain offert par Capptain SAS dans une application reposant sur Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="fddff-136">The following describes how to migrate an SDK integration from the Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="fddff-137">Capptain et Engagement Mobile ne sont pas les mêmes services et la procédure décrite ci-dessous explique uniquement comment migrer l'application cliente.</span><span class="sxs-lookup"><span data-stu-id="fddff-137">Capptain and Mobile Engagement are not the same services and the procedure given below only highlights how to migrate the client app.</span></span> <span data-ttu-id="fddff-138">La migration du SDK dans l'application ne migre PAS vos données des serveurs Capptain vers les serveurs Engagement Mobile.</span><span class="sxs-lookup"><span data-stu-id="fddff-138">Migrating the SDK in the app will NOT migrate your data from the Capptain servers to the Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="fddff-139">Si vous migrez à partir d'une version antérieure, consultez le site web de Capptain pour migrer tout d'abord vers 1.1.1, puis appliquez la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="fddff-139">If you are migrating from an earlier version, please consult the Capptain web site to migrate to 1.1.1 first then apply the following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="fddff-140">Package NuGet</span><span class="sxs-lookup"><span data-stu-id="fddff-140">Nuget package</span></span>
<span data-ttu-id="fddff-141">Remplacez **Capptain.WindowsPhone** par le package NuGet **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="fddff-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="fddff-142">Application d'Engagement Mobile</span><span class="sxs-lookup"><span data-stu-id="fddff-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="fddff-143">Le SDK utilise le terme `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="fddff-143">The SDK uses the term `Engagement`.</span></span> <span data-ttu-id="fddff-144">Vous devez mettre à jour votre projet pour qu'il corresponde à cette modification.</span><span class="sxs-lookup"><span data-stu-id="fddff-144">You need to update your project to match this change.</span></span>

<span data-ttu-id="fddff-145">Vous devez désinstaller votre package nuget Capptain actuel.</span><span class="sxs-lookup"><span data-stu-id="fddff-145">You need to uninstall your current Capptain nuget package.</span></span> <span data-ttu-id="fddff-146">Considérez que toutes vos modifications dans le dossier de ressources Capptain seront supprimées.</span><span class="sxs-lookup"><span data-stu-id="fddff-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="fddff-147">Si vous souhaitez conserver ces fichiers, effectuez-en une copie.</span><span class="sxs-lookup"><span data-stu-id="fddff-147">If you want to keep those files then make a copy of them.</span></span>

<span data-ttu-id="fddff-148">Après cela, installez le nouveau package nuget Microsoft Azure Engagement sur votre projet.</span><span class="sxs-lookup"><span data-stu-id="fddff-148">After that, install the new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="fddff-149">Vous le trouverez directement sur le [site web NuGet].</span><span class="sxs-lookup"><span data-stu-id="fddff-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="fddff-150">ou ici.</span><span class="sxs-lookup"><span data-stu-id="fddff-150">or here index.</span></span> <span data-ttu-id="fddff-151">Cette action remplace tous les fichiers de ressources utilisés par Engagement et ajoute la nouvelle DLL Engagement à vos références de projet.</span><span class="sxs-lookup"><span data-stu-id="fddff-151">This action replaces all resources files used by Engagement and adds the new Engagement DLL to your project References.</span></span>

<span data-ttu-id="fddff-152">Vous devez nettoyer vos références de projet en supprimant les références à la DLL Capptain.</span><span class="sxs-lookup"><span data-stu-id="fddff-152">You have to clean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="fddff-153">Si vous ne le faites pas, la version de Capptain génère un conflit et une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="fddff-153">If you do not make this, the version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="fddff-154">Si vous avez personnalisé des ressources Capptain, copiez le contenu de vos anciens fichiers et collez-le dans les nouveaux fichiers Engagement.</span><span class="sxs-lookup"><span data-stu-id="fddff-154">If you have customized Capptain resources, copy your old files content and paste them in the new Engagement files.</span></span> <span data-ttu-id="fddff-155">Notez que les fichiers xaml et cs doivent être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="fddff-155">Please note that both xaml and cs files have to be updated.</span></span>

<span data-ttu-id="fddff-156">Une fois ces étapes terminées, il vous suffit de remplacer les anciennes références Capptain par les nouvelles références Engagement.</span><span class="sxs-lookup"><span data-stu-id="fddff-156">When those steps are completed you only have to replace old Capptain references by the new Engagement references.</span></span>

1. <span data-ttu-id="fddff-157">Tous les espaces de noms Capptain doivent être mis à jour.</span><span class="sxs-lookup"><span data-stu-id="fddff-157">All Capptain namespaces have to be updated.</span></span>
   
    <span data-ttu-id="fddff-158">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="fddff-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="fddff-159">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="fddff-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="fddff-160">Toutes les classes Capptain qui contiennent « Capptain » doivent contenir « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="fddff-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="fddff-161">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="fddff-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="fddff-162">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="fddff-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="fddff-163">Pour les fichiers xaml, les attributs et les espaces de noms Capptain changent également.</span><span class="sxs-lookup"><span data-stu-id="fddff-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="fddff-164">Avant la migration :</span><span class="sxs-lookup"><span data-stu-id="fddff-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="fddff-165">Après la migration :</span><span class="sxs-lookup"><span data-stu-id="fddff-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="fddff-166">Modifications des pages de superposition</span><span class="sxs-lookup"><span data-stu-id="fddff-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="fddff-167">La superposition change également.</span><span class="sxs-lookup"><span data-stu-id="fddff-167">Overlay also changes.</span></span> <span data-ttu-id="fddff-168">Son nouvel espace de noms est `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="fddff-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="fddff-169">Il doit être utilisé dans les fichiers xaml et cs.</span><span class="sxs-lookup"><span data-stu-id="fddff-169">It has to be used in both xaml and cs files.</span></span> <span data-ttu-id="fddff-170">En outre, `CapptainGrid` doit être nommé `EngagementGrid`, `capptain_notification_content` et `capptain_announcement_content` se nomment `engagement_notification_content` et `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="fddff-170">Moreover `CapptainGrid` is to be named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="fddff-171">Pour la superposition :</span><span class="sxs-lookup"><span data-stu-id="fddff-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="fddff-172">Cela devient :</span><span class="sxs-lookup"><span data-stu-id="fddff-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="fddff-173">Quant aux autres ressources telles que les images Capptain et les fichiers HTML, notez qu'elles ont également été renommées de façon à utiliser « Engagement ».</span><span class="sxs-lookup"><span data-stu-id="fddff-173">For the other resources like Capptain pictures and HTML files, please note that they also have been renamed to use "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="fddff-174">Déclaration de projet</span><span class="sxs-lookup"><span data-stu-id="fddff-174">Project declaration</span></span>
<span data-ttu-id="fddff-175">Sur Package.appxmanifest, `File Type Associations` a été mis à jour à partir de :</span><span class="sxs-lookup"><span data-stu-id="fddff-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="fddff-176">capptain\_reach\_content to engagement\_reach\_content</span><span class="sxs-lookup"><span data-stu-id="fddff-176">capptain\_reach\_content to engagement\_reach\_content</span></span>
* <span data-ttu-id="fddff-177">capptain\_log\_file to engagement\_log\_file</span><span class="sxs-lookup"><span data-stu-id="fddff-177">capptain\_log\_file to engagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="fddff-178">ID de l'application / clé SDK</span><span class="sxs-lookup"><span data-stu-id="fddff-178">Application ID / SDK Key</span></span>
<span data-ttu-id="fddff-179">Engagement utilise une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="fddff-179">Engagement uses a connection string.</span></span> <span data-ttu-id="fddff-180">Il est inutile de spécifier un ID d'application et une clé SDK avec Mobile Engagement. Il suffit de spécifier une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="fddff-180">You don't have to specify an application ID and an SDK key with Mobile Engagement, you only have to specify a connection string.</span></span> <span data-ttu-id="fddff-181">Vous pouvez la configurer dans votre fichier EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="fddff-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="fddff-182">La configuration d'Engagement peut être définie dans le fichier `Resources\EngagementConfiguration.xml` de votre projet.</span><span class="sxs-lookup"><span data-stu-id="fddff-182">The Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="fddff-183">Modifiez ce fichier pour spécifier :</span><span class="sxs-lookup"><span data-stu-id="fddff-183">Edit this file to specify:</span></span>

* <span data-ttu-id="fddff-184">Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="fddff-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="fddff-185">Si vous souhaitez plutôt la spécifier au moment de l'exécution, vous pouvez appeler la méthode suivante avant l'initialisation de l'agent Engagement :</span><span class="sxs-lookup"><span data-stu-id="fddff-185">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="fddff-186">La chaîne de connexion de votre application est affichée sur le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="fddff-186">The connection string for your application is displayed on the Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="fddff-187">Changement de noms d'éléments</span><span class="sxs-lookup"><span data-stu-id="fddff-187">Items name change</span></span>
<span data-ttu-id="fddff-188">Tous les éléments nommés *capptain* ont été renommés *engagement*.</span><span class="sxs-lookup"><span data-stu-id="fddff-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="fddff-189">De même pour *Capptain* (renommés *Engagement*).</span><span class="sxs-lookup"><span data-stu-id="fddff-189">Similarly for *Capptain* to *Engagement*.</span></span>

<span data-ttu-id="fddff-190">Exemples d'éléments Capptain couramment utilisés :</span><span class="sxs-lookup"><span data-stu-id="fddff-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="fddff-191">CapptainConfiguration se nomme maintenant EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="fddff-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="fddff-192">CapptainAgent se nomme maintenant EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="fddff-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="fddff-193">CapptainReach se nomme maintenant EngagementReach</span><span class="sxs-lookup"><span data-stu-id="fddff-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="fddff-194">CapptainHttpConfig se nomme maintenant EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="fddff-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="fddff-195">GetCapptainPageName se nomme maintenant GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="fddff-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="fddff-196">Notez que ce changement affecte également les méthodes substituées.</span><span class="sxs-lookup"><span data-stu-id="fddff-196">Note that rename also affects overridden methods.</span></span>

