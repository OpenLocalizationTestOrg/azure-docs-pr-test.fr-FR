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
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Procédures de mise à niveau du Kit de développement logiciel (SDK) des applications Windows Universal
Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions du Kit de développement logiciel de hello. Par exemple, si vous migrez à partir de 0.10.1 too0.11.0 avoir toofirst suivez hello » à partir de 0.9.0 too0.10.1 « procédure puis hello » à partir de 0.10.1 too0.11.0 « procédure.

## <a name="from-330-too340"></a>À partir de 3.3.0 too3.4.0
### <a name="test-logs"></a>Journaux des tests
Journaux de la console produits par hello SDK peuvent être activé/désactivé/filtrées. toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Ressources
segment de recouvrement Hello portée a été améliorée. Il fait partie des ressources de package NuGet du Kit de développement logiciel hello.

Lors de la mise à niveau toohello une nouvelle version du Kit de développement logiciel de hello, vous pouvez choisir que si vous souhaitez tookeep vos fichiers à partir de hello superposition dossier des ressources ou non :

* Si l’utilisation de segment de recouvrement hello précédente pour vous ou vous intégrez hello `WebView` éléments manuellement vos fichiers de sortie, vous pouvez décider tookeep, il continuera de fonctionner. 
* Si vous souhaitez tooupdate toohello nouveau segment de recouvrement, hello suffit de remplacer toute `overlay` dossier à partir de vos ressources avec hello nouveau à partir du package SDK de hello (applications UWP : après la mise à niveau de hello, vous pouvez obtenir le nouveau dossier de superposition hello à partir de % USERPROFILE%\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> À l’aide de la superposition de nouveau hello remplace les personnalisations effectuées sur la version précédente de hello.
> 
> 

## <a name="from-320-too330"></a>À partir de 3.2.0 too3.3.0
### <a name="resources"></a>Ressources
Cette étape concerne uniquement les ressources personnalisées. Si vous avez personnalisé les ressources hello fournies par hello SDK (html, images, segment de recouvrement), vous avez toobackup avant la mise à niveau et appliquez à nouveau votre personnalisation sur mis à niveau ressources.

## <a name="from-310-too320"></a>À partir de 3.1.0 too3.2.0
### <a name="resources"></a>Ressources
Cette étape concerne uniquement les ressources personnalisées. Si vous avez personnalisé les ressources hello fournies par hello SDK (html, images, segment de recouvrement), vous avez toobackup avant la mise à niveau et appliquez à nouveau votre personnalisation sur mis à niveau ressources.

### <a name="webview-integration"></a>l'intégration de vue web
Certains facteurs de forme de périphérique différent toomatch améliorations ont été introduites dans cette version. Assurez-vous que l’intégration de hello webview correspondent aux suivants de hello :

Dans votre page XAML () :

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

Et dans votre fichier .cs associé :

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

## <a name="from-200-too300"></a>À partir de 2.0.0 too3.0.0
### <a name="resources"></a>Ressources
Cette étape concerne uniquement les ressources personnalisées. Si vous avez personnalisé les ressources hello fournies par hello SDK (html, images, segment de recouvrement), vous avez toobackup avant la mise à niveau et appliquez à nouveau votre personnalisation sur mis à niveau ressources.

## <a name="from-111-too200"></a>À partir de 1.1.1 too2.0.0
Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement. 

> [!IMPORTANT]
> Capptain et Mobile Engagement sont hello pas les mêmes services et procédure hello fourni ci-dessous uniquement met en évidence comment toomigrate hello application cliente. Migration hello SDK dans l’application hello ne fait pas migrer vos données des hello Capptain toohello Mobile Engagement serveurs
> 
> 

Si vous effectuez une migration à partir d’une version antérieure, veuillez consultez hello Capptain site web toomigrate too1.1.1 tout d’abord, appliquez hello procédure

### <a name="nuget-package"></a>Package NuGet
Remplacez **Capptain.WindowsPhone** par le package NuGet **MicrosoftAzure.MobileEngagement**.

### <a name="applying-mobile-engagement"></a>Application d'Engagement Mobile
Hello SDK utilise le terme de hello `Engagement`. Vous devez tooupdate toomatch de votre projet cette modification.

Vous devez toouninstall votre package nuget Capptain. Considérez que toutes vos modifications dans le dossier de ressources Capptain seront supprimées. Si vous souhaitez tookeep ces fichiers, faites une copie d’eux.

Après cela, installer le nouveau package de nuget Microsoft Azure Engagement hello sur votre projet. Vous le trouverez directement sur le [site web NuGet]. ou ici. Ce remplace action tous les fichiers de ressources utilisées par l’Engagement et ajoute hello nouvelle DLL d’Engagement tooyour les références de projet.

Vous avez tooclean à vos références de projet et en supprimant les références Capptain DLL. Si vous n’apportez pas cette option, version hello de Capptain est en conflit et erreur se produira.

Si vous avez personnalisé les ressources Capptain, copiez votre ancien contenu de fichiers et les coller dans des fichiers de Engagement hello. Notez que les fichiers xaml et cs ont toobe mis à jour.

Une fois ces étapes terminées il vous suffit tooreplace les anciennes références Capptain par nouvelles références d’Engagement hello.

1. Tous les espaces de noms Capptain ont toobe mis à jour.
   
    Avant la migration :
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Après la migration :
   
        using Microsoft.Azure.Engagement;
2. Toutes les classes Capptain qui contiennent « Capptain » doivent contenir « Engagement ».
   
    Avant la migration :
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Après la migration :
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. Pour les fichiers xaml, les attributs et les espaces de noms Capptain changent également.
   
    Avant la migration :
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Après la migration :
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Modifications des pages de superposition
   
   > [!IMPORTANT]
   > La superposition change également. Son nouvel espace de noms est `Microsoft.Azure.Engagement.Overlay`. Il a toobe utilisé dans les fichiers xaml et cs. En outre `CapptainGrid` toobe nommé `EngagementGrid`, `capptain_notification_content` et `capptain_announcement_content` sont nommés `engagement_notification_content` et `engagement_announcement_content`.
   > 
   > 
   
    Pour la superposition :
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Cela devient :
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Pourquoi autres ressources telles que Capptain images et des fichiers HTML, notez qu’ils ont également été renommé toouse « Engagement ».

### <a name="project-declaration"></a>Déclaration de projet
Sur Package.appxmanifest, `File Type Associations` a été mis à jour à partir de :

* capptain\_atteindre\_tooengagement contenu\_atteindre\_contenu
* capptain\_journal\_tooengagement de fichiers\_journal\_fichier

### <a name="application-id--sdk-key"></a>ID de l'application / clé SDK
Engagement utilise une chaîne de connexion. Vous n’avez pas toospecify un ID d’application et une clé de kit de développement logiciel avec Mobile Engagement, vous devez uniquement toospecify une chaîne de connexion. Vous pouvez la configurer dans votre fichier EngagementConfiguration.

configuration d’Engagement Hello peut être définie dans votre `Resources\EngagementConfiguration.xml` le fichier de votre projet.

Modifiez cette toospecify de fichier :

* Votre chaîne de connexion d'application entre les balises `<connectionString>` and `<\connectionString>`.

Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

chaîne de connexion Hello pour votre application s’affiche sur hello portail classique Azure.

### <a name="items-name-change"></a>Changement de noms d'éléments
Tous les éléments nommés *capptain* ont été renommés *engagement*. De même pour *Capptain* trop*Engagement*.

Exemples d'éléments Capptain couramment utilisés :

* CapptainConfiguration se nomme maintenant EngagementConfiguration
* CapptainAgent se nomme maintenant EngagementAgent
* CapptainReach se nomme maintenant EngagementReach
* CapptainHttpConfig se nomme maintenant EngagementHttpConfig
* GetCapptainPageName se nomme maintenant GetEngagementPageName

Notez que ce changement affecte également les méthodes substituées.

