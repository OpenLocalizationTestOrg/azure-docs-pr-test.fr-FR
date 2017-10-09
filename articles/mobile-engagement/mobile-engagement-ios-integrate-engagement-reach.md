---
title: "aaaAzure Mobile Engagement iOS intégration d’atteindre SDK | Documents Microsoft"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f5f5857-867c-40c5-9d76-675a343a0296
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 40c9bfbdb475ab0b97bdbc9cea798a59cb8a71ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-reach-on-ios"></a>Comment les tooIntegrate Engagement sur iOS
Vous devez suivre la procédure d’intégration hello décrite dans hello [comment tooIntegrate Engagement sur iOS document](mobile-engagement-ios-integrate-engagement.md) avant de suivre ce guide.

Cette documentation nécessite XCode 8. Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Il existe un bogue connu concernant cette version précédente quand elle est exécutée sur des appareils iOS 10 : les notifications système ne sont pas activées. toofix avoir tooimplement hello déconseillé API `application:didReceiveRemoteNotification:` dans votre application déléguer comme suit :

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée. Vous devez basculer tooXCode 8 dès que possible.
>
>

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Activer votre tooreceive d’application en mode silencieux des Notifications Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

## <a name="integration-steps"></a>Étapes d'intégration
### <a name="embed-hello-engagement-reach-sdk-into-your-ios-project"></a>Incorporer hello SDK Reach d’Engagement dans votre projet iOS
* Ajouter le sdk de portée de hello dans votre projet Xcode. Dans Xcode, accédez trop**projet \> ajouter tooproject** et choisissez hello `EngagementReach` dossier.

### <a name="modify-your-application-delegate"></a>Modifier votre délégué d'Application
* En hello en haut de votre fichier d’implémentation, importez le module d’Engagement atteindre hello :

      [...]
      #import "AEReachModule.h"
* Dans la méthode `applicationDidFinishLaunching:` ou `application:didFinishLaunchingWithOptions:`, créez un module de portée et passer en ligne de l’initialisation Engagement tooyour existante :

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
        [...]

        return YES;
      }
* Modifier **'icon.png'** chaîne dont vous souhaitez définir comme l’icône de votre nom de l’image hello.
* Si vous souhaitez toouse hello option *valeur de badge mise à jour* dans les campagnes Reach ou si vous souhaitez que le push natif toouse \<format/Native de SaaS/portée API/campagne Push\> campagnes, vous devez laisser hello portée module gérer Hello badge icône lui-même (elle supprime automatiquement le badge d’application hello et également réinitialiser la valeur hello stockée par Engagement chaque fois qu’application hello est démarré ou foregrounded). Cela est fait en ajoutant hello ligne suivante après l’initialisation du module portée :

      [reach setAutoBadgeEnabled:YES];
* Si vous souhaitez push de données de couverture toohandle, vous devez laisser votre délégué de l’Application est conforme toohello `AEReachDataPushDelegate` protocole. Ajoutez hello ligne suivante après l’initialisation du module portée :

      [reach setDataPushDelegate:self];
* Ensuite, vous pouvez implémenter les méthodes hello `onDataPushStringReceived:` et `onDataPushBase64ReceivedWithDecodedBody:andEncodedBody:` dans votre délégué d’application :

      -(BOOL)didReceiveStringDataPushWithCategory:(NSString*)category body:(NSString*)body
      {
         NSLog(@"String data push message with category <%@> received: %@", category, body);
         return YES;
      }

      -(BOOL)didReceiveBase64DataPushWithCategory:(NSString*)category decodedBody:(NSData *)decodedBody encodedBody:(NSString *)encodedBody
      {
         NSLog(@"Base64 data push message with category <%@> received: %@", category, encodedBody);
         // Do something useful with decodedBody like updating an image view
         return YES;
      }

### <a name="category"></a>Catégorie
paramètre de catégorie Hello est facultatif lorsque vous créez une campagne de Push de données et permet de que vous toofilter données exécute un push. Cela est utile si vous souhaitez que les différents types de toopush de `Base64` tooidentify de données et que vous souhaitez leur type avant de les analyser.

**Votre application est maintenant prêt tooreceive et affichage de contenu atteint !**

## <a name="how-tooreceive-announcements-and-polls-at-any-time"></a>Comment tooreceive annonces et les sondages à tout moment
Engagement peut envoyer des notifications de portée aux utilisateurs finaux de tooyour à tout moment à l’aide de hello Apple Push Notification Service.

tooenable cette fonctionnalité, vous avez tooprepare votre application pour les notifications de push d’Apple et modifier votre délégué de l’application.

### <a name="prepare-your-application-for-apple-push-notifications"></a>Préparer votre application pour les notifications Push Apple
Suivez le guide de hello : [comment tooPrepare votre Application pour les Notifications Push Apple](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)

### <a name="add-hello-necessary-client-code"></a>Ajoutez le code du client nécessaire hello
*À ce stade votre application doit avoir un certificat Apple push inscrit dans le serveur frontal de hello Engagement.*

Si elle n’est pas déjà fait, vous devez tooregister des notifications push tooreceive de votre application.

* Hello d’importation `User Notification` framework :

        #import <UserNotifications/UserNotifications.h>
* Ajouter hello ligne suivante au démarrage de votre application (en général, dans `application:didFinishLaunchingWithOptions:`) :

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

Ensuite, vous devez le jeton du périphérique tooprovide tooEngagement hello retourné par les serveurs d’Apple. Cette opération est effectuée dans la méthode hello nommé `application:didRegisterForRemoteNotificationsWithDeviceToken:` dans votre délégué d’application :

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
        [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

Enfin, vous avez tooinform hello Engagement SDK lorsque votre application reçoit une notification à distance. toodo qui, appelez hello méthode `applicationDidReceiveRemoteNotification:fetchCompletionHandler:` dans votre délégué d’application :

    - (void)application:(UIApplication*)application didReceiveRemoteNotification:(NSDictionary*)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

> [!IMPORTANT]
> Par défaut, l’Engagement atteindre contrôle hello completionHandler. Si vous souhaitez toomanually répondre toohello `handler` dans votre code, vous pouvez passer nil pour hello `handler` bloquer l’achèvement de hello argument et le contrôle vous-même. Consultez hello `UIBackgroundFetchResult` type pour obtenir la liste des valeurs possibles.
>
>

### <a name="full-example"></a>Exemple complet
Voici un exemple complet d'intégration :

    #pragma mark -
    #pragma mark Application lifecycle

    - (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions
    {
      /* Reach module */
      AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
      [reach setAutoBadgeEnabled:YES];

      /* Engagement initialization */
      [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
      [[EngagementAgent shared] setPushDelegate:self];

      /* Views */
      [window addSubview:[tabBarController view]];
      [window makeKeyAndVisible];

      [application registerForRemoteNotificationTypes:UIRemoteNotificationTypeAlert|UIRemoteNotificationTypeBadge|UIRemoteNotificationTypeSound];
      return YES;
    }

    - (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
    {
      [[EngagementAgent shared] registerDeviceToken:deviceToken];
    }

    - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
    }

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Résoudre les conflits de délégué UNUserNotificationCenter

*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*

A `UNUserNotificationCenter` délégué est utilisé par le cycle de vie hello SDK toomonitor hello de notifications d’Engagement sur les appareils qui exécutent sur iOS ou supérieure à 10. Hello SDK possède sa propre implémentation de hello `UNUserNotificationCenterDelegate` de protocole, mais il peut y avoir qu’un seul `UNUserNotificationCenter` déléguer par application. Tout autre délégué ajouté toohello `UNUserNotificationCenter` objet est en conflit avec hello Engagement une. Si hello SDK détecte le délégué de votre ou de plusieurs autres tiers alors qu’il n’utilise pas sa propre implémentation toogive vous une chance tooresolve hello est en conflit. Vous devez tooadd hello Engagement logique tooyour possèdent des conflits de hello tooresolve délégué dans l’ordre.

Il existe deux façons tooachieve cela.

Proposition de 1, simplement en transfert votre délégué appelle toohello SDK :

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Ou 2, en héritant de hello `AEUserNotificationHandler` classe

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Vous pouvez déterminer si une notification d’Engagement ou non, en passant son `userInfo` dictionnaire toohello Agent `isEngagementPushPayload:` méthode de classe.

Vérifiez que hello `UNUserNotificationCenter` délégué de l’objet a la valeur délégué tooyour dans soit hello `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` méthode du délégué de votre application.
Par exemple, si vous avez implémenté hello ci-dessus proposition 1 :

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }

## <a name="how-toocustomize-campaigns"></a>Comment les campagnes toocustomize
### <a name="notifications"></a>Notifications
Il existe deux types de notifications : les notifications système et les notifications dans l'application.

Les notifications système sont gérées par iOS et ne peuvent pas être personnalisées.

Les notifications dans l’application sont constituées d’une vue qui est ajoutée dynamiquement toohello fenêtre d’application actuelle. Il s'agit d'une superposition de notification. Superpositions de notification sont parfaites pour une intégration rapide car ils ne nécessitent pas vous toomodify n’importe quelle vue dans votre application.

#### <a name="layout"></a>Disposition
apparence hello toomodify vos notifications dans l’application, il suffit de modifier le fichier de hello `AENotificationView.xib` tooyour a besoin, tant que vous conservez les valeurs de balise hello et les types de sous-vues existant de hello.

Par défaut, les notifications dans l’application sont présentées sous l’écran hello hello. Si vous préférez toodisplay en haut de hello de l’écran, modifier hello fourni `AENotificationView.xib` et modifiez hello `AutoSizing` propriété de vue principale de hello donc peuvent rester en haut hello de son super-vue.

#### <a name="categories"></a>Catégories
Lorsque vous modifiez hello fourni mise en page, vous modifiez apparence hello toutes vos notifications. Les catégories permettent toodefine que différents ciblés recherche (et éventuellement des comportements) pour les notifications. Une catégorie peut être spécifiée lorsque vous créez une campagne Reach. N'oubliez pas que les catégories vous permettent également de personnaliser les annonces et les sondages, décrits plus avant dans ce document.

tooregister un gestionnaire de catégorie pour les notifications, vous devez tooadd un appel une fois hello atteindre le module est initialisé.

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:@"my_category"];
    ...

`myNotifier`doit être une instance d’un objet qui est conforme toohello protocole `AENotifier`.

Vous pouvez implémenter des méthodes de protocole hello par vous-même ou vous pouvez choisir tooreimplement hello existants de la classe `AEDefaultNotifier` qui exécute déjà la plupart du travail de hello.

Par exemple, si vous souhaitez un affichage des notifications tooredefine hello pour une catégorie spécifique, vous pouvez suivre cet exemple :

    #import "AEDefaultNotifier.h"
    #import "AENotificationView.h"
    @interface MyNotifier : AEDefaultNotifier
    @end

    @implementation MyNotifier

    -(NSString*)nibNameForCategory:(NSString*)category
    {
      return "MyNotificationView";
    }

    @end

Cet exemple simple de catégorie part du principe que vous possédez un fichier nommé `MyNotificationView.xib` dans votre offre groupée d'applications principale. Si la méthode hello n’est pas en mesure de toofind correspondante `.xib`Engagement génère un message dans la console hello et notification de hello n’apparaissent pas.

fichier nib de Hello fournie doit respecter hello suivant les règles :

* Il doit contenir une seule vue.
* Sous-vues doivent être de hello même de type hello celles à l’intérieur de fichier nib de hello fourni nommé`AENotificationView.xib`
* Sous-vues doivent avoir hello même balises comme celles à l’intérieur de fichier nib de hello fourni nommé hello`AENotificationView.xib`

> [!TIP]
> Simplement copier le fichier nib hello fourni nommé `AENotificationView.xib`et commencer à travailler à partir de là. Mais attention, hello vue à l’intérieur de ce fichier nib est associé toohello classe `AENotificationView`. Cette classe redéfini méthode hello `layoutSubViews` toomove et redimensionner ses sous-vues selon toocontext. Vous souhaiterez peut-être tooreplace avec un `UIView` ou la classe d’affichage personnalisé pour vous.
>
>

Si vous avez besoin d’une personnalisation plus approfondie de vos notifications (si vous souhaitez que pour l’instance tooload votre vue directement à partir de code de hello), il est recommandé de tootake examiner hello a fourni la documentation de code et de la classe source de `Protocol ReferencesDefaultNotifier` et `AENotifier`.

Notez que vous pouvez utiliser hello même notifiant pour plusieurs catégories.

Vous pouvez le notificateur de valeur par défaut hello également redéfini comme suit :

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerNotifier:myNotifier forCategory:kAEReachDefaultCategory];

##### <a name="notification-handling"></a>Gestion des notifications
Lorsque vous utilisez la catégorie par défaut de hello, certaines méthodes de cycle de vie sont appelées sur hello `AEReachContent` tooreport des statistiques et mise à jour hello campagne l’état de l’objet :

* Lors de la notification de hello s’affiche dans l’application, hello `displayNotification` méthode est appelée (qui fournit des statistiques) par `AEReachModule` si `handleNotification:` retourne `YES`.
* Si la notification de hello est fermée, hello `exitNotification` méthode est appelée, la statistique est signalée et campagnes suivants peuvent maintenant être traités.
* Cliquez sur la notification de hello `actionNotification` est appelée, la statistique est signalée et hello associé action est effectuée.

Si votre implémentation de `AENotifier` contournements hello le comportement par défaut, vous pouvez toocall ces méthodes de cycle de vie vous-même. Hello suivant exemples illustre certains cas où le comportement par défaut de hello est ignorée :

* Vous n'étendez pas `AEDefaultNotifier`, par exemple, vous avez implémenté la gestion des catégories à partir de zéro.
* Vous a substitué `prepareNotificationView:forContent:`, être d’au moins sûr toomap `onNotificationActioned` ou `onNotificationExited` tooone de vos contrôles U.I.

> [!WARNING]
> Si `handleNotification:` lève une exception, hello contenu est supprimé et `drop` est appelé, cela est signalé dans les statistiques et campagnes suivants peuvent maintenant être traités.
>
>

#### <a name="include-notification-as-part-of-an-existing-view"></a>Incluez des notifications dans le cadre d'une vue existante
Les superpositions sont idéales pour une intégration rapide mais peuvent parfois ne pas être pratiques ou avoir des effets secondaires indésirables.

Si vous n’êtes pas satisfait de système de superposition hello dans certains de vos affichages, vous pouvez le personnaliser pour ces vues.

Vous pouvez décider tooinclude à notre disposition de notification dans vos vues existantes. toodo il y a donc deux styles de mise en œuvre :

1. Ajouter l’affichage des notifications hello à l’aide du constructeur d’interface

   * Ouvrez *Interface Builder*
   * Placez un 320 x 60 (ou si vous êtes sur iPad 768 x 60) `UIView` où vous souhaitez hello notification tooappear
   * La valeur hello balise pour cette vue trop : **36822491**
2. Ajouter la vue des notifications hello par programmation. Ajoutez simplement hello suivant code lorsque votre vue a été initialisée :

       UIView* notificationView = [[UIView alloc] initWithFrame:CGRectMake(0, 0, 320, 60)]; //Replace x and y coordinate values tooyour needs.
       notificationView.tag = NOTIFICATION_AREA_VIEW_TAG;
       [self.view addSubview:notificationView];

La macro `NOTIFICATION_AREA_VIEW_TAG` se trouve dans `AEDefaultNotifier.h`.

> [!NOTE]
> notificateur de valeur par défaut Hello détecte automatiquement cette mise en page de notification hello est inclus dans cette vue et n’ajoute pas d’un segment de recouvrement pour celle-ci.
>
>

### <a name="announcements-and-polls"></a>Annonces et sondages
#### <a name="layouts"></a>Mises en forme
Vous pouvez modifier les fichiers hello `AEDefaultAnnouncementView.xib` et `AEDefaultPollView.xib` tant que vous conservez les valeurs de balise hello et les types de sous-vues existant de hello.

#### <a name="categories"></a>Catégories
##### <a name="alternate-layouts"></a>Autres dispositions
Telles que les notifications, catégorie de la campagne hello peut être utilisé toohave des formes différentes vos annonces et les interroge.

toocreate une catégorie pour une annonce, vous devez étendre **AEAnnouncementViewController** et l’inscrire une fois le module de couverture hello a été initialisé :

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:@"my_category"];

> [!NOTE]
> Chaque fois un utilisateur clique sur une notification pour une annonce avec la catégorie de hello « mon\_catégorie », votre contrôleur d’affichage inscrits (dans ce cas `MyCustomAnnouncementViewController`) sera initialisé en appelant la méthode hello `initWithAnnouncement:` et affichage de hello sera fenêtre d’application actuelle toohello ajouté.
>
>

Dans votre implémentation de hello `AEAnnouncementViewController` classe que vous aurez une propriété de hello tooread `announcement` tooinitialize votre sous-vues. Considérez l’exemple hello ci-dessous, où deux étiquettes sont initialisés à l’aide de `title` et `body` propriétés Hello `AEReachAnnouncement` classe :

    -(void)loadView
    {
        [super loadView];

        UILabel* titleLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        titleLabel.font = [UIFont systemFontOfSize:32.0];
        titleLabel.text = self.announcement.title;

        UILabel* bodyLabel = [[UILabel alloc] initWithFrame:CGRectMake(10, 20, 300, 60)];
        bodyLabel.font = [UIFont systemFontOfSize:24.0];
        bodyLabel.text = self.announcement.body;

        [self.view addSubview:titleLabel];
        [self.view addSubview:bodyLabel];
    }

Si vous ne souhaitez pas vos vues tooload par vous-même mais que vous souhaitiez simplement la disposition de vue annonce tooreuse hello par défaut, vous pouvez simplement mettre le contrôleur de votre affichage personnalisé étend la classe hello fourni `AEDefaultAnnouncementViewController`. Dans ce cas, en double fichier nib de hello `AEDefaultAnnouncementView.xib` et renommez-la peut être chargé par le contrôleur de votre affichage personnalisé (pour un contrôleur nommé `CustomAnnouncementViewController`, vous devez appeler votre fichier nib `CustomAnnouncementView.xib`).

catégorie de par défaut hello tooreplace des annonces, inscrire simplement votre contrôleur de vue personnalisée pour la catégorie hello définie dans `kAEReachDefaultCategory`:

    [reach registerAnnouncementController:[MyCustomAnnouncementViewController class] forCategory:kAEReachDefaultCategory];

Interroge peut être personnalisée hello identique :

    AEReachModule* reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
    [reach registerPollController:[MyCustomPollViewController class] forCategory:@"my_category"];

Cette fois-ci, le hello fourni `MyCustomPollViewController` doit étendre `AEPollViewController`. Ou vous pouvez choisir tooextend à partir du contrôleur hello par défaut : `AEDefaultPollViewController`.

> [!IMPORTANT]
> N’oubliez pas toocall soit `action` (`submitAnswers:` pour l’affichage des contrôleurs de sondage personnalisé) ou `exit` avant le contrôleur d’affichage hello est fermée. Sinon, les statistiques ne seront pas envoyées (autrement dit, aucune analytique sur une campagne de hello) et plus de campagnes important suivant ne seront pas informés qu’après le redémarrage du processus d’application hello.
>
>

##### <a name="implementation-example"></a>Exemple d'implémentation
Dans cette implémentation, vue d’annonce personnalisée hello est chargé à partir d’un fichier xib externe.

Comme pour la personnalisation de la notification avancés, il est recommandé toolook au code source de hello d’implémentation standard de hello.

`CustomAnnouncementViewController.h`

    //Interface
    @interface CustomAnnouncementViewController : AEAnnouncementViewController {
      UILabel* titleLabel;
      UITextView* descTextView;
      UIWebView* htmlWebView;
      UIButton* okButton;
      UIButton* cancelButton;
    }

    @property (nonatomic, retain) IBOutlet UILabel* titleLabel;
    @property (nonatomic, retain) IBOutlet UITextView* descTextView;
    @property (nonatomic, retain) IBOutlet UIWebView* htmlWebView;
    @property (nonatomic, retain) IBOutlet UIButton* okButton;
    @property (nonatomic, retain) IBOutlet UIButton* cancelButton;

    -(IBAction)okButtonClicked:(id)sender;
    -(IBAction)cancelButtonClicked:(id)sender;

`CustomAnnouncementViewController.m`

    //Implementation
    @implementation CustomAnnouncementViewController
    @synthesize titleLabel;
    @synthesize descTextView;
    @synthesize htmlWebView;
    @synthesize okButton;
    @synthesize cancelButton;

    -(id)initWithAnnouncement:(AEReachAnnouncement*)anAnnouncement
    {
      self = [super initWithNibName:@"CustomAnnouncementViewController" bundle:nil];
      if (self != nil) {
        self.announcement = anAnnouncement;
      }
      return self;
    }

    - (void) dealloc
    {
      [titleLabel release];
      [descTextView release];
      [htmlWebView release];
      [okButton release];
      [cancelButton release];
      [super dealloc];
    }

    - (void)viewDidLoad {
      [super viewDidLoad];

      /* Init announcement title */
      titleLabel.text = self.announcement.title;

      /* Init announcement body */
      if(self.announcement.type == AEAnnouncementTypeHtml)
      {
        titleLabel.hidden = YES;
        htmlWebView.hidden = NO;
        [htmlWebView loadHTMLString:self.announcement.body baseURL:[NSURL URLWithString:@"http://localhost/"]];
      }
      else
      {
        titleLabel.hidden = NO;
        htmlWebView.hidden = YES;
        descTextView.text = self.announcement.body;
      }

      /* Set action button label */
      if([self.announcement.actionLabel length] > 0)
        [okButton setTitle:self.announcement.actionLabel forState:UIControlStateNormal];

      /* Set exit button label */
      if([self.announcement.exitLabel length] > 0)
        [cancelButton setTitle:self.announcement.exitLabel forState:UIControlStateNormal];
    }

    #pragma mark Actions

    -(IBAction)okButtonClicked:(id)sender
    {
        [self action];
    }

    -(IBAction)cancelButtonClicked:(id)sender
    {
        [self exit];
    }

    @end
