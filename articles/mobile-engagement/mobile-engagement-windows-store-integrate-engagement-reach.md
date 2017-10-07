---
title: "aaaWindows Universal intégration du Kit de développement logiciel atteindre applications"
description: Comment tooIntegrate Azure Mobile Engagement atteindre avec les applications Windows universelles
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Intégration du Kit de développement logiciel du module Couverture des applications Windows Universal
Vous devez suivre la procédure d’intégration hello décrite dans hello [intégration du Kit de développement logiciel Windows universel Engagement](mobile-engagement-windows-store-integrate-engagement.md) avant de suivre ce guide.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Incorporer hello SDK Reach d’Engagement dans votre projet Windows universel
Vous n’avez rien tooadd. `EngagementReach` se trouvent déjà dans votre projet.

> [!TIP]
> Vous pouvez personnaliser les images situés dans hello `Resources` dossier de votre projet, en particulier hello marque icône (cette valeur par défaut toohello Engagement). Sur les applications universelles, vous pouvez également déplacer hello `Resources` dossier sur votre tooshare projet partagé son contenu entre les applications, mais vous aurez tookeep hello `Resources\EngagementConfiguration.xml` des fichiers sur son emplacement par défaut car il est dépendant de la plate-forme.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Activer hello Service de Notification Windows
### <a name="windows-8x-and-windows-phone-81-only"></a>Windows 8.x et Windows Phone 8.1 uniquement
Bonjour toouse de commande **Service de Notification Windows** (désignées comme WNS) dans votre `Package.appxmanifest` des fichiers sur `Application UI` cliquez sur `All Image Assets` dans zone de gauche bot hello. À hello à droite de la zone hello `Notifications`, modifiez `toast capable` de `(not set)` trop`(Yes)`.

### <a name="all-platforms"></a>Toutes les plateformes
Vous devez toosynchronize votre application tooyour Microsoft compte et toohello engagement plateforme. Pour cela vous avez besoin toocreate un compte ou une session [centre de développement windows](https://dev.windows.com). Une fois que créer une application et que vous recherchez hello SID et une clé secrète. Sur hello engagement frontal, allez sur la configuration de votre application dans `native push` et coller vos informations d’identification. Ensuite, cliquez avec le bouton droit sur votre projet, puis sélectionnez `store` et `Associate App with hello Store...`. Vous devez simplement l’application hello de tooselect vous avez créez-le avant toosynchronize.

## <a name="initialize-hello-engagement-reach-sdk"></a>Initialiser hello SDK Reach d’Engagement
Modifier hello `App.xaml.cs`:

* Insérez `EngagementReach.Instance.Init` juste après `EngagementAgent.Instance.Init` dans votre méthode `InitEngagement` :
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Hello `EngagementReach.Instance.Init` s’exécute dans un thread dédié. Vous n’avez pas toodo il vous-même.

> [!NOTE]
> Si vous utilisez des notifications push ailleurs dans votre application, vous avez trop[partager votre canal push](#push-channel-sharing) avec Engagement atteindre.
> 
> 

## <a name="integration"></a>Intégration
Engagement fournit les bannières dans l’application de deux façons tooadd hello portée et spot pour annonces et les sondages dans votre application : hello superposition intégration et l’intégration manuelle des vues web hello. Vous ne devez pas combiner les deux approches sur hello même page.

choix de Hello entre l’intégration de deux hello peut se résumer ainsi :

* Vous pouvez choisir hello superposition intégration si vos pages hérite déjà de hello Agent `EngagementPage`, il vous suffit de remplacement `EngagementPage` par `EngagementPageOverlay` et `xmlns:engagement="using:Microsoft.Azure.Engagement"` par `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` dans vos pages.
* Vous pouvez choisir intégration manuelle des vues web hello si vous voulez tooprecisely place hello atteindre de l’interface utilisateur dans vos pages, ou si vous ne souhaitez pas tooadd un autre pages de niveau tooyour d’héritage. 

### <a name="overlay-integration"></a>Intégration de superposition
segment de recouvrement Hello Engagement ajoute dynamiquement des éléments d’interface utilisateur hello utilisé toodisplay couvertures campagne dans votre page. Si hello superposition ne convient à votre disposition vous devez envisager les vues web hello intégration manuelle à la place.

Votre modification de fichier .xaml `EngagementPage` trop de référence`EngagementPageOverlay`

* Ajoutez les déclarations d’espaces de noms tooyour :
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Remplacez `engagement:EngagementPage` par `engagement:EngagementPageOverlay` :

**Avec EngagementPage :**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**Avec EngagementPageOverlay :**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Puis, dans le fichier .cs, ajoutez à votre page le mot-clé `EngagementPageOverlay` au lieu de `EngagementPage`, puis importez `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Remplacez `EngagementPage` par `EngagementPageOverlay` :

**Avec EngagementPage :**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**Avec EngagementPageOverlay :**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Hello superposition d’Engagement ajoute un `Grid` élément au-dessus de votre page composé de votre mise en page et de hello deux `WebView` éléments les uns pour hello bannière et hello autres un pour la vue de spot hello.

Vous pouvez personnaliser les éléments de segment de recouvrement hello directement dans hello `EngagementPageOverlay.cs` fichier.

### <a name="web-views-manual-integration"></a>Intégration manuelle de vues web
Portée recherchent vos pages pour hello deux `WebView` éléments chargés d’afficher la bannière de hello et affichage de spot hello. Hello la seule chose que vous avez toodo est tooadd ces deux `WebView` éléments quelque part dans vos pages, Voici un exemple :

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


Dans cette hello exemple `WebView` éléments est toofit étendue de leur conteneur qui automatiquement les tailles nouveau en cas de changement de taille de fenêtre rotation ou de l’écran.

> [!WARNING]
> Il est important de tookeep hello dénomination `engagement_notification_content` et `engagement_announcement_content` pour hello `WebView` éléments. Reach les identifie par leur nom. 
> 
> 

## <a name="handle-datapush-optional"></a>Gérer les Push de données (facultatif)
Si vous souhaitez que votre push de données application toobe tooreceive en mesure de portée, vous avez tooimplement deux événements de hello EngagementReach classe :

Dans App.xaml.cs dans le constructeur de App() hello ajouter :

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

Vous pouvez voir que le rappel hello de chaque méthode retourne une valeur booléenne. Engagement envoie un back-end de commentaires tooits après la distribution de push de données hello. Si le rappel de hello retourne la valeur false, hello `exit` commentaires sera envoyé. Dans le cas contraire, il s'agira du retour `action`. Si aucun rappel n’est définie pour les événements de hello, hello `drop` commentaires seront affichera tooEngagement.

> [!WARNING]
> Engagement n’est pas en mesure de tooreceive des évaluations de multiples pour un push de données. Si vous prévoyez tooset plusieurs gestionnaires d’un événement, n’oubliez pas que les commentaires hello correspondent toohello dernière celui envoyé. Dans ce cas, nous vous recommandons de tooalways renvoie hello même valeur tooavoid ayant des commentaires à confusion sur hello frontal.
> 
> 

## <a name="customize-ui-optional"></a>Personnaliser l'interface utilisateur (facultatif)
### <a name="first-step"></a>Première étape
Nous permettent de portée de hello toocustomize l’interface utilisateur.

toodo, vous devez toocreate une sous-classe de hello `EngagementReachHandler` classe.

**Exemple de code :**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

Ensuite, définissez le contenu de hello hello `EngagementReach.Instance.Handler` champ avec votre objet personnalisé dans votre `App.xaml.cs` classe au sein de hello `App()` (méthode).

**Exemple de code :**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Par défaut, Engagement utilise sa propre implémentation de `EngagementReachHandler`.
> Vous n’avez pas toocreate votre propre, et si vous procédez ainsi, vous n’avez toooverride chaque méthode. comportement par défaut de Hello est un objet de base d’Engagement tooselect hello.
> 
> 

### <a name="web-view"></a>Vue web
Par défaut, portée utilisera hello incorporée des ressources de notifications de hello DLL toodisplay hello et pages.

tooprovide complète des possibilités de personnalisation nous utilisons uniquement l’affichage web. Si vous souhaitez que les dispositions toocustomize, substituer directement les fichiers de ressources hello `EngagementAnnouncement.html` et `EngagementNotification.html`. Tout le code a besoin d’engagement `<body></body>` toorun correctement. Toutefois, vous pouvez ajouter des balises en dehors de `engagement_webview_area`.

Toutefois, vous pouvez décider toouse vos propres ressources.

Vous pouvez remplacer `EngagementReachHandler` dans votre toouse d’Engagement de tootell sous-classe vos dispositions, mais acceptent mécanisme hello soins tooembedded :

**Exemple de code :**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


Par défaut, AnnouncementHTML est `ms-appx-web:///Resources/EngagementAnnouncement.html`. Il représente le fichier html hello concevoir contenu hello d’un message envoyé (annonce de texte, Web anoucement et annonce d’interrogation). AnnouncementName est `engagement_announcement_content`. Il est le nom hello de conception du webview hello dans votre page xaml.

NotificationHTML est `ms-appx-web:///Resources/EngagementNotification.html`. Il représente le fichier html hello concevoir notification hello d’un message envoyé. NotificationName est `engagement_notification_content`. Il est le nom hello de conception du webview hello dans votre page xaml.

### <a name="customization"></a>Personnalisation
Vous pouvez personnaliser comme bon vous semble les vues web des notifications et des annonces, du moment que vous conservez l'objet Engagement. Prenez soin que webview objet est décrit trois fois : hello première fois dans votre xaml, deuxième fois dans votre fichier .cs dans la méthode de « setwebview() » hello et troisième heure dans le fichier html de hello.

* Dans votre code xaml, vous décrivez composant webview graphique disposition en cours de hello.
* Dans votre fichier .cs, vous pouvez définir « setwebview() », dans laquelle vous définissez dimension hello du webview de deux hello (notification, annonce). Il est très efficace lors du redimensionne de l’application hello.
* Dans le fichier html de Engagement hello nous décrivent la création de contenu, webview hello et hello positions d’éléments entre eux.

### <a name="launch-message"></a>Lancer un message
Lorsqu’un utilisateur clique sur une notification système (un toast), Engagement lance l’application hello, charge le contenu hello Hello transmettre des messages et afficher la page hello pour les campagnes correspondants hello.

Il existe un décalage entre le lancement de hello de hello application et hello l’affichage de page hello (selon la vitesse de hello de votre réseau).

utilisateur toohello tooindicate quelque chose est en cours de chargement, vous devez fournir une informations visuelles, comme une barre de progression ou un indicateur de progression. Engagement ne peut pas gérer cela lui-même. Toutefois, il fournit plusieurs gestionnaires à cet effet.

ajouter de rappel hello tooimplement dans App.xaml.cs dans « App() publique {} » :

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Vous pouvez définir le rappel de hello dans votre méthode de « Public App() {} » de votre `App.xaml.cs` fichier, de préférence avant hello `EngagementReach.Instance.Init()` appeler.

> [!TIP]
> Chaque gestionnaire est appelé par le Thread d’interface utilisateur de hello. Vous n’avez pas de tooworry lorsque vous utilisez un MessageBox ou quelque chose dépendant de l’interface utilisateur.
> 
> 

## <a id="push-channel-sharing"></a> Partage de canal Push
Si vous utilisez des notifications push pour un autre objet dans votre application vous avez la fonctionnalité de partage de hello SDK de l’Engagement de canal de push toouse hello. Il s’agit de tooavoid manqué push.

* Vous pouvez fournir votre propre push toohello Engagement atteindre l’initialisation de canal. Hello SDK utilise au lieu de demander un nouveau.

Mettre à jour de l’initialisation d’Engagement atteindre hello avec votre canal push Bonjour `InitEngagement` méthode hello `App.xaml.cs` fichier :

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* Ou bien, si vous souhaitez simplement tooconsume hello push canal après l’initialisation de portée hello vous pouvez définir un rappel sur l’Engagement atteindre de canal tooget hello push qui a été créé par le Kit de développement logiciel de hello.

Définir votre rappel en tout lieu **après** hello d’initialisation de portée :

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Astuce concernant les schémas personnalisés
Il est possible d'utiliser des schémas personnalisés. Vous pouvez envoyer un type différent de l’URI d’engagement toobe de serveur frontal utilisé dans votre application d’engagement. Les schémas par défaut comme `http, ftp, ...` sont gérés par Windows. Une fenêtre vous informera si aucune application par défaut n'est installée sur l'appareil. Vous pouvez également créer un schéma personnalisé pour votre application.

Hello tooset de façon simple un schéma personnalisé dans votre application est tooopen votre `Package.appxmanifest` accédez dans `Declarations` Panneau de configuration. Sélectionnez `Protocol` Bonjour, faites défiler les déclarations disponibles boîte et l’ajouter. Modifier hello `Name` nom de champ avec votre nouveau protocole voulu.

Toouse maintenant ce protocole, modifiez votre `App.xaml.cs` avec hello `OnActivated` (méthode) et n’oubliez pas également engagement tooinitialize ici :

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

