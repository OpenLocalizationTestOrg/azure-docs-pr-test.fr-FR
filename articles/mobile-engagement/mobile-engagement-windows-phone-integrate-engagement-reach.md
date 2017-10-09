---
title: "aaaWindows intégration du Kit de développement logiciel Silverlight atteindre téléphone"
description: Comment tooIntegrate Azure Mobile Engagement atteindre avec les applications Silverlight Windows Phone
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Intégration du Kit de développement logiciel (SDK) du module Couverture Windows Phone Silverlight
Vous devez suivre la procédure d’intégration hello décrite dans hello [intégration du Kit de développement logiciel Windows Phone Silverlight Engagement](mobile-engagement-windows-phone-integrate-engagement.md) avant de suivre ce guide.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Incorporer hello SDK Reach d’Engagement dans votre projet Windows Phone Silverlight
Vous n’avez rien tooadd. `EngagementReach` se trouvent déjà dans votre projet.

> [!TIP]
> Vous pouvez personnaliser les images situés dans hello `Resources` dossier de votre projet, en particulier hello marque icône (cette valeur par défaut toohello Engagement).
> 
> 

## <a name="add-hello-capabilities"></a>Ajouter des fonctionnalités hello
Hello SDK Reach d’Engagement a besoin des fonctions supplémentaires.

Ouvrez votre `WMAppManifest.xml` de fichiers et assurez-vous que hello suivant des fonctions sont déclarés :

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Hello tout d’abord un est utilisé par hello MPNS service tooallow hello affichage de notification de toast. Hello second est utilisé tooembed une tâche de navigateur dans le Kit de développement logiciel de hello.

Modifier hello `WMAppManifest.xml` et ajoutez à l’intérieur de hello `<Capabilities />` balise :

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Activer hello services de notifications Push Microsoft
Bonjour toouse de commande **les services de notifications Push Microsoft** (désignées comme MPNS) votre `WMAppManifest.xml` fichier doit avoir un `<App />` la balise avec un `Publisher` attribut défini toohello nom de votre projet.

## <a name="initialize-hello-engagement-reach-sdk"></a>Initialiser hello SDK Reach d’Engagement
### <a name="engagement-configuration"></a>Configuration d'Engagement
configuration d’Engagement Hello centralisée dans hello `Resources\EngagementConfiguration.xml` fichier de votre projet.

Modifiez cette configuration de portée de fichier toospecify :

* *Facultatif*, indiquent si le push natif hello (MPNS) est activé ou pas entre `<enableNativePush>` et `</enableNativePush>` balises (`true` par défaut).
* *Facultatif*, indiquez le nom du canal de transmission hello entre hello `<channelName>` et `</channelName>` fournissent des balises, hello même que votre application peut actuellement utiliser ou laissez-le vide.

Si vous souhaitez toospecify il lors de l’exécution au lieu de cela, vous pouvez appeler suivant de hello méthode avant l’initialisation de l’agent hello Engagement :

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> Vous pouvez spécifier le nom de hello de hello de canal MPNS push de votre application. Par défaut, Engagement crée un nom basé sur hello appId. Vous n’avez aucun besoin de toospecify hello nom vous-même, sauf si vous prévoyez de canal de transmission toouse hello en dehors de l’Engagement.
> 
> 

### <a name="engagement-initialization"></a>Initialisation d'Engagement
Modifier hello `App.xaml.cs`:

* Ajouter tooyour `using` instructions :
  
      using Microsoft.Azure.Engagement;
* Insérez `EngagementReach.Instance.Init` juste après `EngagementAgent.Instance.Init` dans `Application_Launching` :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Insérer `EngagementReach.Instance.OnActivated` Bonjour `Application_Activated` méthode :
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Hello `EngagementReach.Instance.Init` s’exécute dans un thread dédié. Vous n’avez pas toodo il vous-même.
> 
> 

## <a name="app-store-submission-considerations"></a>Considérations relatives à la soumission App store
Microsoft impose certaines règles lors de l’utilisation des notifications push de hello :

À partir de hello Microsoft [stratégies d’Application] documentation, section 2.9 :

1) Vous devez demander des notifications push de hello utilisateur tooaccept tooreceive. Ajoutez ensuite une notifications push de façon toodisable hello dans vos paramètres.

objet de EngagementReach Hello fournit deux méthodes toomanage hello/opt-retrait, `EnableNativePush()` et `DisableNativePush()`. Par exemple, vous pourriez créer une option dans les paramètres de hello avec un toodisable bascule ou activer MPNS.

Vous pouvez également décider toodeactivate MPNS via la configuration d’Engagement hello\<configuration du portée Kit de développement logiciel windows phone\>.

> 2.9.1) application hello doit décrivent tout d’abord toobe de notifications hello fourni et **obtenir l’autorisation de l’utilisateur hello express (opt-in)**, et **doivent fournir un mécanisme via le hello utilisateur peut refuser de réception notifications Push**. Toutes les notifications sont fournies à l’aide de hello services de notifications Push Microsoft doivent être cohérentes avec hello description fournie toohello utilisateur et doit respecter toutes applicables [stratégies d’Application] [ Content Policies]et [des exigences supplémentaires pour les Types d’Application spécifique].
> 
> 

2) Vous ne devez pas utiliser trop de notifications Push. Engagement gérera les notifications pour vous.

> 2.9.2) application hello et son utilisation de services de notifications Push Microsoft de hello ne doivent pas excessivement utiliser la capacité de réseau ou de la bande passante de hello services de notifications Push Microsoft, ou sinon indûment surcharger un Windows Phone ou autre appareil de Microsoft ou un service avec excessive push notifications, comme déterminé par Microsoft à sa discrétion raisonnable et ne doit pas endommager ou interférer avec les réseaux Microsoft ou serveurs ou des serveurs tiers ni toohello de réseaux connectés services de notifications Push Microsoft.
> 
> 

3) Ne comptez pas sur des informations critiques et MPNS toosend. Engagement utilise MPNS, cette règle s’applique également pour les campagnes hello créées à l’intérieur de hello Engagement frontales.

> 2.9.3) hello services de notifications Push Microsoft n’est peut-être pas les notifications toosend utilisés sont mission critique ou sinon peut affecter les questions de durée de vie ou de décès, y compris sans dispositif médical de limitation des notifications critiques tooa connexes ou de condition. MICROSOFT expressément exclut toute garantie que hello utilisation de hello MICROSOFT PUSH NOTIFICATION SERVICE ou remise de MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS sera être sans interruption, erreur libre, ou sinon garantie tooOCCUR ON A en temps réel base.
> 
> 

**Nous ne pouvons pas garantir que votre application passe les processus de validation hello si vous ne respectez pas ces recommandations.**

## <a name="handle-data-push-optional"></a>Gérer les Push de données (facultatif)
Si vous souhaitez que votre push de données application toobe tooreceive en mesure de portée, vous avez tooimplement deux événements de hello EngagementReach classe :

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

Ensuite, définissez le contenu de hello hello `EngagementReach.Instance.Handler` champ avec votre objet personnalisé dans votre `App.xaml.cs` classe au sein de hello `Application_Launching` (méthode).

**Exemple de code :**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Par défaut, Engagement utilise sa propre implémentation de `EngagementReachHandler`. Vous n’avez pas toocreate votre propre, et si vous procédez ainsi, vous n’avez toooverride chaque méthode. comportement par défaut de Hello est un objet de base d’Engagement tooselect hello.
> 
> 

### <a name="layouts"></a>Mises en forme
Par défaut, portée utilisera hello incorporée des ressources de notifications de hello DLL toodisplay hello et pages.

Toutefois, vous pouvez décider toouse tooreflect de vos propres ressources votre marque dans ces composants.

Vous pouvez remplacer `EngagementReachHandler` méthodes dans votre toouse d’Engagement de tootell sous-classe vos dispositions :

**Exemple de code :**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Hello `CreateNotification` méthode peut retourner une valeur null. notification de Hello ne s’affiche et couverture de campagne hello ne sera supprimé.
> 
> 

toosimplify votre implémentation de la mise en page, nous fournissons également notre propre code xaml qui permettre servir comme base pour votre code. Ils se trouvent dans l’archive du SDK de l’Engagement hello (/ src/portée).

> [!WARNING]
> sources de Hello que nous fournissons sont hello exacte mêmes que ceux que nous utilisons. Par conséquent, si vous souhaitez toomodify les directement, n’oubliez espace de noms toochange hello et hello nom.
> 
> 

### <a name="notification-position"></a>Position des notifications
Par défaut, une notification dans l’application s’affiche dans hello partie inférieure gauche de l’application hello. Vous pouvez modifier ce comportement en substituant hello `GetNotificationPosition` méthode Hello `EngagementReachHandler` objet.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Actuellement, vous pouvez choisir entre hello `BOTTOM` (par défaut) et `TOP` positions.

### <a name="launch-message"></a>Lancer un message
Lorsqu’un utilisateur clique sur une notification système (un toast), lance d’Engagement hello app, charge le contenu hello Hello transmettre des messages et afficher la page hello pour hello correspondant campagne.

Il existe un décalage entre le lancement de hello de hello application et hello l’affichage de page hello (selon la vitesse de hello de votre réseau).

utilisateur toohello tooindicate quelque chose est en cours de chargement, vous devez fournir une informations visuelles, comme une barre de progression ou un indicateur de progression. Engagement ne peut pas gérer cela lui-même. Toutefois, il fournit plusieurs gestionnaires à cet effet.

tooimplement hello rappel, procédez comme :

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

Vous pouvez définir le rappel de hello dans votre `Application_Launching` méthode de votre `App.xaml.cs` fichier, de préférence avant hello `EngagementReach.Instance.Init()` appeler.

> [!TIP]
> Chaque gestionnaire est appelé par le Thread d’interface utilisateur de hello. Vous n’avez pas de tooworry lorsque vous utilisez un MessageBox ou quelque chose dépendant de l’interface utilisateur.
> 
> 

[stratégies d’Application]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[des exigences supplémentaires pour les Types d’Application spécifique]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

