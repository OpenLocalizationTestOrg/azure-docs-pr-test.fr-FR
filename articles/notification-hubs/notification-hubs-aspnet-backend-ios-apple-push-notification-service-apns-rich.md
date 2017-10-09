---
title: aaaAzure Notification Hubs riche Push
description: "Découvrez comment toosend enrichi push notifications tooan iOS application à partir d’Azure. Code samples written in Objective-C and C#."
documentationcenter: ios
services: notification-hubs
author: ysxu
manager: erikre
editor: 
ms.assetid: 590304df-c0a4-46c5-8ef5-6a6486bb3340
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 5432d8bf47777371bea3521a0c0176ade75fbd9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-rich-push"></a>Notifications Push enrichies avec Azure Notification Hubs
## <a name="overview"></a>Vue d'ensemble
Dans l’ordre tooengage les utilisateurs instantanée contenu riche, une application peut vouloir toopush au-delà de texte brut. Ces notifications promeuvent les interactions entre utilisateurs et présentent du contenu tel que des URL, des sons, des images/coupons et bien plus encore. Ce didacticiel s’appuie sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) rubrique et montre comment toosend push notifications qui incorporent des charges utiles (par exemple, image).

Ce didacticiel est compatible avec iOS 7 et 8.

  ![][IOS1]

À un niveau élevé :

1. serveur principal d’application Hello :
   * Magasins hello riche charge utile (dans ce cas, l’image) dans le stockage de base de données/local hello principal
   * Envoie l’ID du périphérique toohello enrichi de notification
2. Application sur l’appareil de hello :
   * Contacts hello principal demandant la charge utile de riches hello avec l’ID de hello qu’il reçoit
   * Envoie des notifications d’utilisateurs sur l’appareil de hello lors de la récupération des données est terminée et affiche la charge utile de hello immédiatement lorsque les utilisateurs appuient sur toolearn plus

## <a name="webapi-project"></a>Projet WebAPI
1. Dans Visual Studio, ouvrez hello **AppBackend** projet que vous avez créé dans hello [avertir les utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) didacticiel.
2. Obtenir une image vous que les utilisateurs de toonotify avec et placez-le dans un **img** dossier dans votre répertoire de projet.
3. Cliquez sur **afficher tous les fichiers** dans hello l’Explorateur de solutions et cliquez sur le dossier de hello trop**inclure dans le projet**.
4. Image hello sélectionnée, de modifier son Action de génération dans la fenêtre Propriétés trop**ressource incorporée**.
   
    ![][IOS2]
5. Dans **Notifications.cs**, ajoutez hello qui suit à l’aide d’instruction :
   
        using System.Reflection;
6. Hello de mise à jour entière **Notifications** classe avec hello suivant de code. Être tooreplace que des espaces réservés de hello avec vos informations d’identification du hub de notification et le nom du fichier image.
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message toodisplay toousers
            public string Message { get; set; }
            // Type of rich payload (developer-defined)
            public string RichType { get; set; }
            public string Payload { get; set; }
            public bool Read { get; set; }
        }
   
        public class Notifications {
            public static Notifications Instance = new Notifications();
   
            private List<Notification> notifications = new List<Notification>();
   
            public NotificationHubClient Hub { get; set; }
   
            private Notifications() {
                // Placeholders: replace with hello connection string (with full access) for your notification hub and hello hub name from hello Azure Classics Portal
                Hub = NotificationHubClient.CreateClientFromConnectionString("{conn string with full access}",  "{hub name}");
            }
   
            public Notification CreateNotification(string message, string richType, string payload) {
                var notification = new Notification() {
                    Id = notifications.Count,
                    Message = message,
                    RichType = richType,
                    Payload = payload,
                    Read = false
                };
   
                notifications.Add(notification);
   
                return notification;
            }
   
            public Stream ReadImage(int id) {
                var assembly = Assembly.GetExecutingAssembly();
                // Placeholder: image file name (for example, logo.png).
                return assembly.GetManifestResourceStream("AppBackend.img.{logo.png}");
            }
        }
   
   > [!NOTE]
   > (facultatif) Consultez trop[comment tooembed et l’accès aux ressources à l’aide de Visual C#](http://support.microsoft.com/kb/319292) pour plus d’informations sur la façon de tooadd et obtenir des ressources de projet.
   > 
   > 
7. Dans **NotificationsController.cs**, redéfinir **NotificationsController** avec hello suivant des extraits de code. Cela envoie un toodevice id de la notification initiale riche en mode silencieux et permet l’extraction du côté client de l’image :
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) tooclient
        public async Task<HttpResponseMessage> Post() {
            // Replace hello placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification tooapns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. Maintenant nous sera redéployer cette application de tooan site Web Azure dans l’ordre toomake accessible à partir de tous les appareils. Avec le bouton droit sur hello **AppBackend** de projet et sélectionnez **publier**.
9. Sélectionnez Site web Azure comme cible de publication. Connectez-vous avec votre compte Azure, sélectionnez un site Web existant ou nouveau et prenez note de hello **URL de destination** propriété Bonjour **connexion** onglet. Nous appelons URL toothis comme votre *point de terminaison principal* plus loin dans ce didacticiel. Cliquez sur **Publier**.

## <a name="modify-hello-ios-project"></a>Modifier le projet iOS de hello
Maintenant que vous avez modifié votre hello simplement d’application back-end toosend *id* d’une notification, vous allez modifier votre toohandle d’application iOS cet id et récupérer le message de type hello enrichi à partir de votre serveur principal.

1. Ouvrez votre projet iOS et activer les notifications à distance en accédant de cible tooyour principal de l’application Bonjour **cibles** section.
2. Cliquez sur **fonctionnalités**, activez **Modes d’arrière-plan**et vérifiez hello **des Notifications à distance** case à cocher.
   
    ![][IOS3]
3. Accédez trop**Main.storyboard**et assurez-vous que vous disposez d’un contrôleur de vue (indiqué tooas accueil View Controller dans ce didacticiel) à partir de [notifier l’utilisateur](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) didacticiel.
4. Ajouter un **Navigation contrôleur** tooyour d’animation et faites glisser la touche contrôle toomake de vue contrôleur tooHome il hello **racine vue** de navigation. Vérifiez que hello **contrôleur d’affichage Initial est** dans les attributs inspecteur est sélectionné pour hello contrôleur de Navigation.
5. Ajouter un **View Controller** toostoryboard et ajoutez un **affichage Image**. Il s’agit de page hello les utilisateurs verront une fois qu’ils choisissent toolearn plus en cliquant sur les notifiication hello. Votre storyboard doit ressembler à ce qui suit :
   
    ![][IOS4]
6. Cliquez sur hello **accueil View Controller** dans la table de montage séquentiel et assurez-vous qu’il a **homeViewController** en tant que son **classe personnalisée** et **ID de table de montage séquentiel**sous inspecteur d’identité hello.
7. De même hello pour le contrôleur de vue d’Image en tant que **imageViewController**.
8. Ensuite, créez une nouvelle classe de contrôleur d’affichage intitulée **imageViewController** toohandle hello l’interface utilisateur que vous venez de créer.
9. Dans **imageViewController.h**, ajouter hello suivant des déclarations d’interface du contrôleur toohello. Assurez-vous que toocontrol, faites glisser hello storyboard image vue toothese propriétés toolink hello deux :
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. Dans **imageViewController.m**, ajoutez hello qui suit à la fin de hello de **viewDidload**:
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. Dans **AppDelegate.m**, contrôleur d’image hello importation vous avez créé :
    
        #import "imageViewController.h"
12. Ajoutez une section d’interface avec hello suit déclaration :
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. Dans **AppDelegate**, vérifiez que votre application est inscrite aux notifications en mode silencieux dans **application: didFinishLaunchingWithOptions** :
    
        // Software version
        self.iOS8 = [[UIApplication sharedApplication] respondsToSelector:@selector(registerUserNotificationSettings:)] && [[UIApplication sharedApplication] respondsToSelector:@selector(registerForRemoteNotifications)];
    
        // Register for remote notifications for iOS8 and previous versions
        if (self.iOS8) {
            NSLog(@"This device is running with iOS8.");
    
            // Action
            UIMutableUserNotificationAction *richPushAction = [[UIMutableUserNotificationAction alloc] init];
            richPushAction.identifier = @"richPushMore";
            richPushAction.activationMode = UIUserNotificationActivationModeForeground;
            richPushAction.authenticationRequired = NO;
            richPushAction.title = @"More";
    
            // Notification category
            UIMutableUserNotificationCategory* richPushCategory = [[UIMutableUserNotificationCategory alloc] init];
            richPushCategory.identifier = @"richPush";
            [richPushCategory setActions:@[richPushAction] forContext:UIUserNotificationActionContextDefault];
    
            // Notification categories
            NSSet* richPushCategories = [NSSet setWithObjects:richPushCategory, nil];

            UIUserNotificationSettings *settings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeSound |
                                                    UIUserNotificationTypeAlert |
                                                    UIUserNotificationTypeBadge
                                                                                     categories:richPushCategories];

            [[UIApplication sharedApplication] registerUserNotificationSettings:settings];
            [[UIApplication sharedApplication] registerForRemoteNotifications];

        }
        else {
            // Previous iOS versions
            NSLog(@"This device is running with iOS7 or earlier versions.");

            [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
        }

        return YES;

1. Remplacez Bonjour après la mise en oeuvre pour **application : didRegisterForRemoteNotificationsWithDeviceToken** storyboard de hello tootake interface utilisateur change en compte :
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. Ensuite, ajoutez hello trop des méthodes suivantes**AppDelegate.m** tooretrieve hello image à partir de votre point de terminaison et d’envoyer une notification locale lors de la récupération est terminée. Assurez-vous qu’espace réservé de hello toosubstitute `{backend endpoint}` avec votre point de terminaison principal :
   
       NSString *const GetNotificationEndpoint = @"{backend endpoint}/api/notifications";
   
       // Helper: retrieve notification content from backend with rich notification id
       - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion {
           UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
           homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
           NSString* authenticationHeader = hvc.registerClient.authenticationHeader;
           // Check if authenticated
           if (!authenticationHeader) return;
   
           NSURLSession* session = [NSURLSession
                                    sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                    delegate:nil
                                    delegateQueue:nil];
   
           NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, richId]];
           NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
           [request setHTTPMethod:@"GET"];
           NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
           [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
   
           NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
   
               NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
               if (!error && httpResponse.statusCode == 200) {
                   // From NSData tooUIImage
                   self.imagePayload = [UIImage imageWithData:data];
   
                   completion(nil);
               }
               else {
                   NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                   if (error)
                       completion(error);
                   else {
                       completion([NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                   }
               }
           }];
           [dataTask resume];
       }
   
       // Handle silent push notifications when id is sent from backend
       - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler {
           self.userInfo = userInfo;
           int richId = [[self.userInfo objectForKey:@"richId"] intValue];
           NSString* richType = [self.userInfo objectForKey:@"richType"];
   
           // Retrieve image data
           if ([richType isEqualToString:@"img"]) {  
               [self retrieveRichImageWithId:richId completion:^(NSError* error) {
                   if (!error){
                       // Send local notification
                       UILocalNotification* localNotification = [[UILocalNotification alloc] init];
   
                       // "5" is arbitrary here toogive you enough time tooquit out of hello app and receive push notifications
                       localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:5];
                       localNotification.userInfo = self.userInfo;
                       localNotification.alertBody = [self.userInfo objectForKey:@"richMessage"];
                       localNotification.timeZone = [NSTimeZone defaultTimeZone];
   
                       // iOS8 categories
                       if (self.iOS8) {
                           localNotification.category = @"richPush";
                       }
   
                       [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                       handler(UIBackgroundFetchResultNewData);
                   }
                   else{
                       handler(UIBackgroundFetchResultFailed);
                   }
               }];
           }
           // Add "else if" here toohandle more types of rich content such as url, sound files, etc.
       }
3. Gérer les notifications de local hello ci-dessus en ouvrant hello image Vue contrôleur **AppDelegate.m** avec hello méthodes suivantes :
   
       // Helper: redirect users tooimage view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image tooimage view controller
           imgViewController.imagePayload = img;
   
           // Redirect
           [navigationController pushViewController:imgViewController animated:YES];
       }
   
       // Handle local notification sent above in didReceiveRemoteNotification
       - (void)application:(UIApplication *)application didReceiveLocalNotification:(UILocalNotification *)notification {
           if (application.applicationState == UIApplicationStateActive) {
               // Show in-app alert with an extra "more" button
               UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:notification.alertBody delegate:self cancelButtonTitle:@"OK" otherButtonTitles:@"More", nil];
   
               [alert show];
           }
           // App becomes active from user's tap on notification
           else {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
       }
   
       // Handle buttons in in-app alerts and redirect with data/image
       - (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex {
           // Handle "more" button
           if (buttonIndex == 1)
           {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           // Add "else if" here toohandle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-hello-application"></a>Exécutez hello Application
1. Dans XCode, exécutez l’application hello sur un appareil iOS physiques (push notifications ne fonctionnera pas dans le simulateur de hello).
2. Dans une application iOS de hello l’interface utilisateur, entrez un nom d’utilisateur et un mot de passe de hello même valeur pour l’authentification et cliquez sur **journal dans**.
3. Cliquez sur **Envoyer des notifications Push** : une alerte dans l’application doit s’afficher. Si vous cliquez sur **plus**, vous serez image toohello remises choisis tooinclude à votre serveur principal d’application.
4. Vous pouvez également cliquer sur **envoi push** et appuyez immédiatement sur bouton Accueil de hello de votre appareil. Dans quelques instants, vous allez recevoir une notification Push. Si vous cliquez dessus ou cliquez sur plus d’informations, vous serez amené à tooyour application et hello le contenu riche d’image.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
