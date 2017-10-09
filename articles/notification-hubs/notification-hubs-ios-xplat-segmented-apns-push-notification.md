---
title: "aaaNotification concentrateurs dernières actualités didacticiel - iOS"
description: "Découvrez comment toouse toosend de concentrateurs de Notification Azure Service Bus avec rupture des appareils de nouvelles notifications tooiOS."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 6ead4169-deff-4947-858c-8c6cf03cc3b2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 763b80b5ffed238b351d95bd3d6a96cb914f53cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilisez toosend concentrateurs de Notification dernières actualités
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toouse Azure Notification Hubs toobroadcast avec rupture nouvelles notifications tooan iOS application. Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories. Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications pour des ventilateurs de musique, etc..

Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello. Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello. Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance. Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Composants requis
Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification][get-started]. Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Ajouter une application de toohello de sélection de catégorie
première étape de Hello est tooadd hello UI éléments tooyour storyboard existant qui permettent de hello utilisateur tooselect catégories tooregister. catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello. Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.

1. Dans votre MainStoryboard_iPhone.storyboard ajoutez hello suivant des composants à partir de la bibliothèque d’objets hello :
   
   * une étiquette intitulée « Dernières nouvelles » ;
   * des étiquettes portant les intitulés de catégories « Monde », « Politiques », « Entreprise », « Technologies », « Science », « Sports » ;
   * Six commutateurs, un par catégorie, définissez chaque commutateur **état** toobe **hors** par défaut.
   * un bouton intitulé « S’abonner ».
     
     Votre storyboard doit ressembler à ce qui suit :
     
     ![][3]
2. Dans l’éditeur de l’assistant hello, créer prises pour tous les commutateurs hello et les appeler « WorldSwitch », « PoliticsSwitch », « BusinessSwitch », « TechnologySwitch », « ScienceSwitch », « SportsSwitch »
3. Créez une action pour le bouton intitulé « S’abonner ». Votre ViewController.h doit contenir des éléments suivants de hello :
   
        @property (weak, nonatomic) IBOutlet UISwitch *WorldSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *PoliticsSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *BusinessSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *TechnologySwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *ScienceSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *SportsSwitch;
   
        - (IBAction)subscribe:(id)sender;
4. Créez une **classe Cocoa Touch** appelée `Notifications`. Copiez hello suivant de code dans la section d’interface hello du fichier de hello Notifications.h :
   
        @property NSData* deviceToken;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName;
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSArray*)categories
                    completion:(void (^)(NSError* error))completion;
   
        - (NSSet*)retrieveCategories;
   
        - (void)subscribeWithCategories:(NSSet*)categories completion:(void (^)(NSError *))completion;
5. Ajoutez hello suivant tooNotifications.m directive d’importation :
   
        #import <WindowsAzureMessaging/WindowsAzureMessaging.h>
6. Copiez hello suivant de code dans la section d’implémentation hello du fichier de hello Notifications.m.
   
        SBNotificationHub* hub;
   
        - (id)initWithConnectionString:(NSString*)listenConnectionString HubName:(NSString*)hubName{
   
            hub = [[SBNotificationHub alloc] initWithConnectionString:listenConnectionString
                                        notificationHubPath:hubName];
   
            return self;
        }
   
        - (void)storeCategoriesAndSubscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
   
            [self subscribeWithCategories:categories completion:completion];
        }

        - (NSSet*)retrieveCategories {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];

            NSArray* categories = [defaults stringArrayForKey:@"BreakingNewsCategories"];

            if (!categories) return [[NSSet alloc] init];
            return [[NSSet alloc] initWithArray:categories];
        }


        - (void)subscribeWithCategories:(NSSet *)categories completion:(void (^)(NSError *))completion
        {
           //[hub registerNativeWithDeviceToken:self.deviceToken tags:categories completion: completion];

            NSString* templateBodyAPNS = @"{\"aps\":{\"alert\":\"$(messageParam)\"}}";

            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"simpleAPNSTemplate" 
                jsonBodyTemplate:templateBodyAPNS expiryTemplate:@"0" tags:categories completion:completion];
        }



    Cette classe utilise le stockage local toostore et récupérer des catégories hello de news reçoit cet appareil. Il contient également un tooregister de méthode pour ces catégories en utilisant un [modèle](notification-hubs-templates-cross-platform-push-messages.md) l’inscription.

1. Dans le fichier de AppDelegate.h hello, ajoutez une instruction d’importation pour Notifications.h et ajouter une propriété d’une instance de la classe de Notifications de hello :
   
        #import "Notifications.h"
   
        @property (nonatomic) Notifications* notifications;
2. Bonjour **didFinishLaunchingWithOptions** méthode dans AppDelegate.m, ajoutez instance de notifications hello code tooinitialize hello début hello de méthode hello.  
   
    `HUBNAME`et `HUBLISTENACCESS` (défini dans hubinfo.h) doit déjà avoir hello `<hub name>` et `<connection string with listen access>` des espaces réservés est remplacé par votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature*que vous avez obtenu précédemment
   
        self.notifications = [[Notifications alloc] initWithConnectionString:HUBLISTENACCESS HubName:HUBNAME];
   
   > [!NOTE]
   > Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente. Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées. clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.
   > 
   > 
3. Bonjour **didRegisterForRemoteNotificationsWithDeviceToken** méthode dans AppDelegate.m, remplacez code hello dans la méthode hello hello après la classe de code toopass hello périphérique jeton toohello des notifications. classe de notifications Hello effectuera hello inscription aux notifications avec les catégories de hello. Si l’utilisateur de hello modifie les sélections de catégorie, nous appelons hello `subscribeWithCategories` méthode dans la réponse toohello **s’abonner** bouton tooupdate les.
   
   > [!NOTE]
   > Étant donné que le jeton du périphérique hello attribué par hello Apple Push Notification Service (APNS) pouvez chance à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification. Cet exemple inscrit pour la notification chaque fois que cette application hello démarre. Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.
   > 
   > 
   
        self.notifications.deviceToken = deviceToken;
   
        // Retrieves hello categories from local storage and requests a registration for these categories
        // each time hello app starts and performs a registration.
   
        NSSet* categories = [self.notifications retrieveCategories];
        [self.notifications subscribeWithCategories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

    Notez qu’à ce stade il ne doit y avoir aucun autre code Bonjour **didRegisterForRemoteNotificationsWithDeviceToken** (méthode).

1. Hello méthodes suivantes doivent déjà être présentes dans AppDelegate.m à partir de la fin de hello [prise en main des concentrateurs de Notification] [ get-started] didacticiel.  Si ce n’est pas le cas, veuillez les ajouter.
   
    -(void) MessageBox :(NSString *) titre message :(NSString *) messageText {}
   
        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:messageText delegate:self
            cancelButtonTitle:@"OK" otherButtonTitles: nil];
        [alert show];
    }
   
   * application (void) :(UIApplication *) application didReceiveRemoteNotification : (NSDictionary *) userInfo {NSLog (@ « % @ », userInfo) ;   [message self MessageBox:@"Notification » : [valueForKey:@"alert [userInfo objectForKey:@"aps »] »]] ; }
   
   Cette méthode gère les notifications reçues lors de l’application hello est en cours d’exécution en affichant un simple **UIAlert**.
2. Dans ViewController.m, ajoutez une instruction d’importation pour AppDelegate.h et copie hello après le code dans hello XCode généré **s’abonner** (méthode). Ce code met à jour hello notification d’enregistrement toouse hello nouvelle catégorie balises hello l’utilisateur a choisi dans l’interface utilisateur hello.
   
       ```
       #import "Notifications.h"
       ```
   
       NSMutableArray* categories = [[NSMutableArray alloc] init];
   
       if (self.WorldSwitch.isOn) [categories addObject:@"World"];
       if (self.PoliticsSwitch.isOn) [categories addObject:@"Politics"];
       if (self.BusinessSwitch.isOn) [categories addObject:@"Business"];
       if (self.TechnologySwitch.isOn) [categories addObject:@"Technology"];
       if (self.ScienceSwitch.isOn) [categories addObject:@"Science"];
       if (self.SportsSwitch.isOn) [categories addObject:@"Sports"];
   
       Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];
   
       [notifications storeCategoriesAndSubscribeWithCategories:categories completion: ^(NSError* error) {
           if (!error) {
               [(AppDelegate*)[[UIApplication sharedApplication]delegate] MessageBox:@"Notification" message:@"Subscribed!"];
           } else {
               NSLog(@"Error subscribing: %@", error);
           }
       }];
   
   Cette méthode crée un **NSMutableArray** de catégories et les utilisations hello **Notifications** liste hello classe toostore hello local stockage et les registres hello balises correspondantes avec votre concentrateur de notification. Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.
3. Dans ViewController.m, ajoutez hello suivant code Bonjour **viewDidLoad** interface utilisateur de méthode tooset hello en fonction de catégories de hello précédemment enregistré.

        // This updates hello UI on startup based on hello status of previously saved categories.

        Notifications* notifications = [(AppDelegate*)[[UIApplication sharedApplication]delegate] notifications];

        NSSet* categories = [notifications retrieveCategories];

        if ([categories containsObject:@"World"]) self.WorldSwitch.on = true;
        if ([categories containsObject:@"Politics"]) self.PoliticsSwitch.on = true;
        if ([categories containsObject:@"Business"]) self.BusinessSwitch.on = true;
        if ([categories containsObject:@"Technology"]) self.TechnologySwitch.on = true;
        if ([categories containsObject:@"Science"]) self.ScienceSwitch.on = true;
        if ([categories containsObject:@"Sports"]) self.SportsSwitch.on = true;



application Hello peut maintenant stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello à chaque démarrage de l’application hello.  utilisateur de Hello peut modifier la sélection hello des catégories lors de l’exécution et cliquez sur hello **s’abonner** méthode tooupdate hello l’inscription de périphérique de hello. Ensuite, vous mettrez à jour hello de toosend application hello avec rupture des notifications sur l’actualité directement dans l’application hello proprement dit.

## <a name="optional-sending-tagged-notifications"></a>(Facultatif) Envoyer des notifications avec balises
Si vous n’avez pas accès tooVisual Studio, vous pouvez ignorer la section suivante de toohello et envoyer des notifications à partir de l’application hello proprement dit. Vous pouvez également envoyer une notification de modèle approprié hello de hello [portail classique Azure] à l’aide d’onglet débogage de hello pour votre concentrateur de notification. 

[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="optional-send-notifications-from-hello-device"></a>(facultatif) Envoyer des notifications à partir de l’appareil de hello
Normalement des notifications sont envoyées par un service principal, mais vous pouvez envoyer des notifications sur l’actualité directement à partir de l’application hello. toodo cela nous mettrons à jour hello `SendNotificationRESTAPI` méthode que nous avons défini Bonjour [prise en main des concentrateurs de Notification] [ get-started] didacticiel.

1. Bonjour de mise à jour ViewController.m `SendNotificationRESTAPI` méthode comme suit afin qu’il accepte un paramètre pour l’étiquette de catégorie hello et envoie hello approprié [modèle](notification-hubs-templates-cross-platform-push-messages.md) notification.
   
        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];
   
            NSString *json;
   
            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];
   
            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];
   
            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];
   
            // Add hello category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];
   
            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\"}",
                    categoryTag, self.notificationMessage.text];
   
            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];
   
            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];
   
            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];
   
            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
   
            // Send hello REST request
            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request
                       completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
               {
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                   if (error || httpResponse.statusCode != 200)
                   {
                       NSLog(@"\nError status: %d\nError: %@", httpResponse.statusCode, error);
                   }
                   if (data != NULL)
                   {
                       //xmlParser = [[NSXMLParser alloc] initWithData:data];
                       //[xmlParser setDelegate:self];
                       //[xmlParser parse];
                   }
               }];
   
            [dataTask resume];
        }
2. Bonjour de mise à jour ViewController.m **envoyer une Notification** action, comme indiqué dans le code hello qui suit. Afin qu’il envoie des notifications de hello à l’aide de chaque balise individuellement et envoyer toomultiple plateformes.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            self.sendResults.text = @"";

            NSArray* categories = [NSArray arrayWithObjects: @"World", @"Politics", @"Business",
                                    @"Technology", @"Science", @"Sports", nil];

            // Lets send hello message as breaking news for each category tooWNS, GCM, and APNS
            // using a template.
            for(NSString* category in categories)
            {
                [self SendNotificationRESTAPI:category];
            }
        }



1. Régénérez votre projet et vérifiez qu’il n’existe aucune erreur de génération.

## <a name="run-hello-app-and-generate-notifications"></a>Exécutez l’application hello et générer des notifications
1. Hello de presse exécuter bouton toobuild hello projet et démarrer l’application hello. Sélectionnez certains tooand toosubscribe de rupture nouvelles options et appuyez sur hello **s’abonner** bouton. Vous devez voir une boîte de dialogue indiquant hello notifications sont abonnées.
   
    ![][1]
   
    Lorsque vous choisissez **s’abonner**, hello des catégories d’applications convertit hello sélectionné dans les balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello.
2. Entrez un toobe message envoyé comme informations de dernière minute puis appuyez sur hello **envoyer une Notification** bouton. Vous pouvez également exécuter notifications de toogenerate l’application console hello .NET.
   
    ![][2]
3. Chaque news toobreaking de périphérique abonné recevra les notifications sur l’actualité hello que vous venez d’envoyer.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, nous l’avons vu comment toobroadcast actualités par catégorie. Envisager d’effectuer une des hello suivant des didacticiels qui mettent en évidence les autres scénarios avancés de concentrateurs de Notification :

* **[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]**
  
    Découvrez comment hello tooexpand dernières actualités application tooenable envoi localisée des notifications.

<!-- Images. -->
[1]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-subscribed.png
[2]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios1.png
[3]: ./media/notification-hubs-ios-send-breaking-news/notification-hub-breakingnews-ios2.png








<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]: notification-hubs-ios-xplat-localized-apns-push-notification.md
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs]: notification-hubs-aspnet-backend-ios-notify-users.md
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/dn530749.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[get-started]: /manage/services/notification-hubs/get-started-notification-hubs-ios/
[portail classique Azure]: https://manage.windowsazure.com
