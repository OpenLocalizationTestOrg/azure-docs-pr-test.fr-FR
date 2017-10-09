---
title: "aaaAzure concentrateurs de Notification d’avertir les utilisateurs pour iOS avec le serveur principal .NET"
description: "Découvrez comment toosend push notifications toousers dans Azure. Exemples de code écrites en Objective-C et hello API .NET pour hello principal."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 1f7d1410-ef93-4c4b-813b-f075eed20082
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 56aed5b04d2d985b3f0e50c58991607f07b61248
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a>Azure Notification Hubs notifie les utilisateurs pour iOS avec backend .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Vue d'ensemble
Prise en charge des notifications push dans Azure vous permet de tooaccess un facile à utiliser, multiplateforme et infrastructure par émission de données à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes. Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push utilisateur de notifications tooa application spécifique sur un périphérique spécifique. Un serveur principal ASP.NET WebAPI est utilisé tooauthenticate clients et les notifications de toogenerate, comme indiqué dans la rubrique d’aide hello [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).

> [!NOTE]
> Ce didacticiel repose sur l'hypothèse que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md). Ce didacticiel est également toohello requis de hello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) didacticiel.
> Si vous souhaitez que les applications mobiles toouse en tant que votre service principal, consultez hello [Mobile Apps prise en main Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a>Modification de votre application iOS
1. Application à Page unique hello ouvrir Affichage vous avez créé dans hello [mise en route avec Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) didacticiel.
   
   > [!NOTE]
   > Dans cette section, nous partons du principe que vous avez configuré votre projet avec un nom d’organisation vide. Si ce n’est pas le cas, vous devez tooprepend votre organisation tooall classe nom.
   > 
   > 
2. Dans votre Main.storyboard ajouter des composants de hello indiqués dans la capture d’écran hello ci-dessous à partir de la bibliothèque d’objets hello.
   
    ![][1]
   
   * **Nom d’utilisateur**: UITextField un texte d’espace réservé, *Entrez le nom d’utilisateur*, immédiatement sous hello envoyer étiquette de résultats et de contrainte toohello gauche et les marges avec le bouton droit et sous hello envoyer l’étiquette de résultats.
   * **Mot de passe**: UITextField un texte d’espace réservé, *entrer le mot de passe*, immédiatement sous hello du champ de texte Nom d’utilisateur et de contrainte toohello gauche et vers la droite les marges et sous le champ de texte Nom d’utilisateur hello. Vérifiez hello **sécuriser la saisie de texte** option Bonjour inspecteur d’attribut, sous *retourner la clé*.
   * **Ouvrez une session**: A UIButton étiqueté immédiatement sous le champ de texte de mot de passe hello et décochez la case hello **activé** option Bonjour inspecteur d’attributs, sous *contenu du contrôle*
   * **WNS**: étiquette et l’envoi de commutateur tooenable hello notification Service de Notification Windows si elle a été paramétrée sur le concentrateur de hello. Consultez hello [Windows prise en main](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) didacticiel.
   * **GCM**: étiquette et l’envoi de commutateur tooenable hello tooGoogle de notification de messagerie Cloud si elle a été paramétrée sur le concentrateur de hello. Consultez le didacticiel [Prise en main d'Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .
   * **APNS**: étiquette et l’envoi de commutateur tooenable hello toohello de notification Apple plateforme Notification Service.
   * **RECIPENT Username**: UITextField un texte d’espace réservé, *balise de nom d’utilisateur destinataire*, immédiatement sous hello GCM étiqueter et contrainte toohello gauche et droite marges et sous hello GCM l’étiquette.

    Certains composants ont été ajoutés dans hello [mise en route avec Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) didacticiel.

1. **CTRL** faire glisser à partir de composants hello en hello vue tooViewController.h et ajouter ces nouveaux prises.
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used tooenable hello buttons on hello UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used tooenabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. Dans ViewController.h, ajoutez suivant de hello `#define` juste en dessous de vos instructions d’importation. Hello de substitution *< Entrez de point de terminaison principal votre\>*  espace réservé par hello URL de Destination utilisé toodeploy de votre serveur principal d’application dans la section précédente de hello. For example, *http://votre_serveur_principal.azurewebsites.net*.
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. Dans votre projet, créez un nouveau **/Cocoa Touch de classe** nommé **RegisterClient** toointerface avec hello ASP.NET back-end, vous avez créé. Créer la classe hello héritant de `NSObject`. Ajoutez ensuite hello après Bonjour RegisterClient.h de code.
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. Mettre à jour hello RegisterClient.m hello `@interface` section :
   
        @interface RegisterClient ()
   
        @property (strong, nonatomic) NSURLSession* session;
        @property (strong, nonatomic) NSURLSession* endpoint;
   
        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion;
        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion;
        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSString*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion;
   
        @end
5. Remplacez hello `@implementation` section Bonjour RegisterClient.m avec hello suivant de code.

        @implementation RegisterClient

        // Globals used by RegisterClient
        NSString *const RegistrationIdLocalStorageKey = @"RegistrationId";

        -(instancetype) initWithEndpoint:(NSString*)Endpoint
        {
            self = [super init];
            if (self) {
                NSURLSessionConfiguration* config = [NSURLSessionConfiguration defaultSessionConfiguration];
                _session = [NSURLSession sessionWithConfiguration:config delegate:nil delegateQueue:nil];
                _endpoint = Endpoint;
            }
            return self;
        }

        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
                    andCompletion:(void(^)(NSError*))completion
        {
            [self tryToRegisterWithDeviceToken:token tags:tags retry:YES andCompletion:completion];
        }

        -(void) tryToRegisterWithDeviceToken:(NSData*)token tags:(NSSet*)tags retry:(BOOL)retry
                    andCompletion:(void(^)(NSError*))completion
        {
            NSSet* tagsSet = tags?tags:[[NSSet alloc] init];

            NSString *deviceTokenString = [[token description]
                stringByTrimmingCharactersInSet:[NSCharacterSet characterSetWithCharactersInString:@"<>"]];
            deviceTokenString = [[deviceTokenString stringByReplacingOccurrencesOfString:@" " withString:@""]
                                    uppercaseString];

            [self retrieveOrRequestRegistrationIdWithDeviceToken: deviceTokenString
                completion:^(NSString* registrationId, NSError *error) {
                NSLog(@"regId: %@", registrationId);
                if (error) {
                    completion(error);
                    return;
                }

                [self upsertRegistrationWithRegistrationId:registrationId deviceToken:deviceTokenString
                    tags:tagsSet andCompletion:^(NSURLResponse * response, NSError *error) {
                    if (error) {
                        completion(error);
                        return;
                    }

                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if (httpResponse.statusCode == 200) {
                        completion(nil);
                    } else if (httpResponse.statusCode == 410 && retry) {
                        [self tryToRegisterWithDeviceToken:token tags:tags retry:NO andCompletion:completion];
                    } else {
                        NSLog(@"Registration error with response status: %ld", (long)httpResponse.statusCode);

                        completion([NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }

                }];
            }];
        }

        -(void) upsertRegistrationWithRegistrationId:(NSString*)registrationId deviceToken:(NSData*)token
                    tags:(NSSet*)tags andCompletion:(void(^)(NSURLResponse*, NSError*))completion
        {
            NSDictionary* deviceRegistration = @{@"Platform" : @"apns", @"Handle": token,
                                                    @"Tags": [tags allObjects]};
            NSData* jsonData = [NSJSONSerialization dataWithJSONObject:deviceRegistration
                                options:NSJSONWritingPrettyPrinted error:nil];

            NSLog(@"JSON registration: %@", [[NSString alloc] initWithData:jsonData
                                                encoding:NSUTF8StringEncoding]);

            NSString* endpoint = [NSString stringWithFormat:@"%@/api/register/%@", _endpoint,
                                    registrationId];
            NSURL* requestURL = [NSURL URLWithString:endpoint];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"PUT"];
            [request setHTTPBody:jsonData];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];
            [request setValue:@"application/json" forHTTPHeaderField:@"Content-Type"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                if (!error)
                {
                    completion(response, error);
                }
                else
                {
                    NSLog(@"Error request: %@", error);
                    completion(nil, error);
                }
            }];
            [dataTask resume];
        }

        -(void) retrieveOrRequestRegistrationIdWithDeviceToken:(NSString*)token
                    completion:(void(^)(NSString*, NSError*))completion
        {
            NSString* registrationId = [[NSUserDefaults standardUserDefaults]
                                        objectForKey:RegistrationIdLocalStorageKey];

            if (registrationId)
            {
                completion(registrationId, nil);
                return;
            }

            // request new one & save
            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/api/register?handle=%@",
                                    _endpoint, token]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"POST"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",
                                                    self.authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [self.session dataTaskWithRequest:request
                completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)
            {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSString* registrationId = [[NSString alloc] initWithData:data
                        encoding:NSUTF8StringEncoding];

                    // remove quotes
                    registrationId = [registrationId substringWithRange:NSMakeRange(1,
                                        [registrationId length]-2)];

                    [[NSUserDefaults standardUserDefaults] setObject:registrationId
                        forKey:RegistrationIdLocalStorageKey];
                    [[NSUserDefaults standardUserDefaults] synchronize];

                    completion(registrationId, nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"Registration" code:httpResponse.statusCode
                                    userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }

        @end

    code Hello ci-dessus implémente la logique de hello expliquée dans l’article d’aide sur hello [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) tooperform reste à l’aide de NSURLSession appelle tooyour serveur principal d’application et NSUserDefaults toolocally magasin hello registrationId retourné par le concentrateur de notification hello.

    Notez que cette classe nécessite sa propriété **authorizationHeader** toobe correctement défini dans l’ordre toowork. Cette propriété est définie par hello **ViewController** classe après connexion hello.

1. Dans ViewController.h, ajoutez une instruction `#import` pour RegisterClient.h. Ensuite, ajoutez une déclaration pour le jeton du périphérique hello et référencer tooa `RegisterClient` instance Bonjour `@interface` section :
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. Dans ViewController.m, ajoutez une déclaration de méthode privée Bonjour `@interface` section :
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> Hello extrait de code suivant n’est pas un schéma d’authentification sécurisée, vous devez vous servir d’implémentation hello Hello **createAndSetAuthenticationHeaderWithUsername:AndPassword :** avec votre mécanisme d’authentification spécifique Cette opération génère un toobe de jeton d’authentification consommée par hello register classe de client, par exemple, OAuth, Active Directory.
> 
> 

1. Ensuite, dans hello `@implementation` section de ViewController.m ajouter hello suivant du code qui ajoute l’implémentation hello pour le paramètre hello périphérique jeton et l’authentification d’un en-tête.
   
        -(void) setDeviceToken: (NSData*) deviceToken
        {
            _deviceToken = deviceToken;
            self.LogInButton.enabled = YES;
        }
   
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
        {
            NSString* headerValue = [NSString stringWithFormat:@"%@:%@", username, password];
   
            NSData* encodedData = [[headerValue dataUsingEncoding:NSUTF8StringEncoding] base64EncodedDataWithOptions:NSDataBase64EncodingEndLineWithCarriageReturn];
   
            self.registerClient.authenticationHeader = [[NSString alloc] initWithData:encodedData
                                                        encoding:NSUTF8StringEncoding];
        }
   
        -(BOOL)textFieldShouldReturn:(UITextField *)textField
        {
            [textField resignFirstResponder];
            return YES;
        }
   
    Notez comment le jeton du périphérique paramètre hello permet hello bouton se connecter. Il s’agit, car dans le cadre de l’action de connexion hello, contrôleur de la vue hello inscrit pour les notifications push avec le serveur principal d’application hello. Par conséquent, nous ne voulons pas se connecter action toobe accessible jusqu'à ce que le jeton du périphérique hello a été correctement configuré. Vous pouvez découpler journal hello dans à partir de l’enregistrement de push hello tant que première de hello se produit avant les hello ce dernier.
2. Dans ViewController.m, utilisez hello suivant la méthode d’action des extraits de code tooimplement hello pour votre **connexion** bouton et une méthode toosend hello notification message à l’aide de ASP.NET principal hello.
   
       - (IBAction) LogInAction : expéditeur de (id) {/ / créer l’en-tête d’authentification et la définir dans le Registre client NSString * nom d’utilisateur = self. UsernameField.text ;   Le mot de passe NSString * = self. PasswordField.text ;
   
           [self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];
   
           selfie __weak ViewController * = self ;   [self.registerClient registerWithDeviceToken:self.deviceToken balises : nil andCompletion:^(NSError* error) {Si ( ! erreur) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES ;               [self MessageBox:@"Success » message:@"Registered avec succès ! »] ;}) ;}}] ;}

        - (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];

            Passez hello pns et nom d’utilisateur de balise en tant que paramètres avec ASP.NET toohello hello URL REST principal NSURL * requestURL = [NSURL URLWithString : [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @ », BACKEND_ENDPOINT, pns, usernameTag]] ;

            Demande de NSMutableURLRequest = [NSMutableURLRequest requestWithURL:requestURL] ;    [demande setHTTPMethod:@"POST »] ;

            Obtenir les authenticationheader fictive hello client de Registre hello authorizationHeaderValue NSString * = [NSString stringWithFormat:@"Basic % @ », self.registerClient.authenticationHeader] ;    [demande setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization »] ;

            Ajouter le corps du message de notification hello [demande setValue:@"application/json;charset=utf-8 « forHTTPHeaderField:@"Content-Type »] ;    [demande setHTTPBody : [message dataUsingEncoding:NSUTF8StringEncoding]] ;

            Exécution d’envoyer une notification hello API REST sur hello ASP.NET principal NSURLSessionDataTask * dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *erreur) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) réponse ;        Si (erreur || httpResponse.statusCode ! = 200) {NSString* état = [NSString stringWithFormat:@"Error état % @: % d\nError : %@\n», pns, httpResponse.statusCode, erreur] ;            dispatch_async(dispatch_get_main_queue(), ^ {/ / ajout de texte, car tous les appels PNS 3 peuvent également avoir des informations tooview [stringByAppendingString:status de setText:[self.sendResults.text self.sendResults]] ;            });            NSLog(status) ;        }

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            }];    [dataTask resume]; }


1. Mettre à jour action hello pour hello **envoyer une Notification** bouton toouse hello ASP.NET principal et envoyer tooany PNS activé par un commutateur.

        - (IBAction)SendNotificationMessage:(id)sender
        {
            //[self SendNotificationRESTAPI];
            [self SendToEnabledPlatforms];
        }


        -(void)SendToEnabledPlatforms
        {
            NSString* json = [NSString stringWithFormat:@"\"%@\"",self.notificationMessage.text];

            [self.sendResults setText:@""];

            if ([self.WNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"wns" UsernameTag:self.RecipientField.text Message:json];

            if ([self.GCMSwitch isOn])
                [self SendNotificationASPNETBackend:@"gcm" UsernameTag:self.RecipientField.text Message:json];

            if ([self.APNSSwitch isOn])
                [self SendNotificationASPNETBackend:@"apns" UsernameTag:self.RecipientField.text Message:json];
        }



1. Dans la fonction **ViewDidLoad**, ajouter hello suit tooinstantiate hello RegisterClient instance et définir un délégué hello pour vos champs de texte.
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. En **AppDelegate.m**, supprimez tout le contenu de la méthode hello hello **didRegisterForPushNotificationWithDeviceToken : l’application :** et remplacez-la par hello suivant toomake que hello vue contrôleur contient le dernier jeton du périphérique hello récupérée à partir de l’APNs :
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. Pour finir dans **AppDelegate.m**, assurez-vous que vous avez hello suivant de méthode :
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a>Hello de test Application
1. Dans XCode, exécutez l’application hello sur un appareil iOS physiques (push notifications ne fonctionnera pas dans le simulateur de hello).
2. Dans une application iOS de hello l’interface utilisateur, entrez un nom d’utilisateur et un mot de passe. Il peuvent être n’importe quelle chaîne, mais ils doivent tous deux être hello même valeur de chaîne. Cliquez ensuite sur **Log In**.
   
    ![][2]
3. Une fenêtre contextuelle doit s’afficher pour vous informer que l’inscription a abouti. Cliquez sur **OK**.
   
    ![][3]
4. Bonjour **balise de nom d’utilisateur destinataire* texte, entrez l’étiquette de nom d’utilisateur hello utilisée avec l’inscription du hello à partir d’un autre périphérique.
5. Entrez un message de notification et cliquez sur **Envoyer une notification**.  Seuls les appareils hello qui ont un enregistrement de balise de nom d’utilisateur destinataire hello recevoir message de notification de hello.  Il est uniquement envoyé aux utilisateurs de toothose.
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
