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
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="9d535-104">Azure Notification Hubs notifie les utilisateurs pour iOS avec backend .NET</span><span class="sxs-lookup"><span data-stu-id="9d535-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="9d535-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="9d535-105">Overview</span></span>
<span data-ttu-id="9d535-106">Prise en charge des notifications push dans Azure vous permet de tooaccess un facile à utiliser, multiplateforme et infrastructure par émission de données à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.</span><span class="sxs-lookup"><span data-stu-id="9d535-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="9d535-107">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push utilisateur de notifications tooa application spécifique sur un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="9d535-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="9d535-108">Un serveur principal ASP.NET WebAPI est utilisé tooauthenticate clients et les notifications de toogenerate, comme indiqué dans la rubrique d’aide hello [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="9d535-108">An ASP.NET WebAPI backend is used tooauthenticate clients and toogenerate notifications, as shown in hello guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="9d535-109">Ce didacticiel repose sur l'hypothèse que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d535-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="9d535-110">Ce didacticiel est également toohello requis de hello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9d535-110">This tutorial is also hello prerequisite toohello [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="9d535-111">Si vous souhaitez que les applications mobiles toouse en tant que votre service principal, consultez hello [Mobile Apps prise en main Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="9d535-111">If you want toouse Mobile Apps as your backend service, see hello [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="9d535-112">Modification de votre application iOS</span><span class="sxs-lookup"><span data-stu-id="9d535-112">Modify your iOS app</span></span>
1. <span data-ttu-id="9d535-113">Application à Page unique hello ouvrir Affichage vous avez créé dans hello [mise en route avec Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9d535-113">Open hello Single Page view app you created in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9d535-114">Dans cette section, nous partons du principe que vous avez configuré votre projet avec un nom d’organisation vide.</span><span class="sxs-lookup"><span data-stu-id="9d535-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="9d535-115">Si ce n’est pas le cas, vous devez tooprepend votre organisation tooall classe nom.</span><span class="sxs-lookup"><span data-stu-id="9d535-115">If not, you will need tooprepend your organization name tooall class names.</span></span>
   > 
   > 
2. <span data-ttu-id="9d535-116">Dans votre Main.storyboard ajouter des composants de hello indiqués dans la capture d’écran hello ci-dessous à partir de la bibliothèque d’objets hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-116">In your Main.storyboard add hello components shown in hello screenshot below from hello object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="9d535-117">**Nom d’utilisateur**: UITextField un texte d’espace réservé, *Entrez le nom d’utilisateur*, immédiatement sous hello envoyer étiquette de résultats et de contrainte toohello gauche et les marges avec le bouton droit et sous hello envoyer l’étiquette de résultats.</span><span class="sxs-lookup"><span data-stu-id="9d535-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath hello send results label and constrained toohello left and right margins and beneath hello send results label.</span></span>
   * <span data-ttu-id="9d535-118">**Mot de passe**: UITextField un texte d’espace réservé, *entrer le mot de passe*, immédiatement sous hello du champ de texte Nom d’utilisateur et de contrainte toohello gauche et vers la droite les marges et sous le champ de texte Nom d’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath hello username text field and constrained toohello left and right margins and beneath hello username text field.</span></span> <span data-ttu-id="9d535-119">Vérifiez hello **sécuriser la saisie de texte** option Bonjour inspecteur d’attribut, sous *retourner la clé*.</span><span class="sxs-lookup"><span data-stu-id="9d535-119">Check hello **Secure Text Entry** option in hello Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="9d535-120">**Ouvrez une session**: A UIButton étiqueté immédiatement sous le champ de texte de mot de passe hello et décochez la case hello **activé** option Bonjour inspecteur d’attributs, sous *contenu du contrôle*</span><span class="sxs-lookup"><span data-stu-id="9d535-120">**Log in**: A UIButton labeled immediately beneath hello password text field and uncheck hello **Enabled** option in hello Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="9d535-121">**WNS**: étiquette et l’envoi de commutateur tooenable hello notification Service de Notification Windows si elle a été paramétrée sur le concentrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-121">**WNS**: Label and switch tooenable sending hello notification Windows Notification Service if it has been setup on hello hub.</span></span> <span data-ttu-id="9d535-122">Consultez hello [Windows prise en main](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9d535-122">See hello [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="9d535-123">**GCM**: étiquette et l’envoi de commutateur tooenable hello tooGoogle de notification de messagerie Cloud si elle a été paramétrée sur le concentrateur de hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-123">**GCM**: Label and switch tooenable sending hello notification tooGoogle Cloud Messaging if it has been setup on hello hub.</span></span> <span data-ttu-id="9d535-124">Consultez le didacticiel [Prise en main d'Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="9d535-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="9d535-125">**APNS**: étiquette et l’envoi de commutateur tooenable hello toohello de notification Apple plateforme Notification Service.</span><span class="sxs-lookup"><span data-stu-id="9d535-125">**APNS**: Label and switch tooenable sending hello notification toohello Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="9d535-126">**RECIPENT Username**: UITextField un texte d’espace réservé, *balise de nom d’utilisateur destinataire*, immédiatement sous hello GCM étiqueter et contrainte toohello gauche et droite marges et sous hello GCM l’étiquette.</span><span class="sxs-lookup"><span data-stu-id="9d535-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath hello GCM label and constrained toohello left and right margins and beneath hello GCM label.</span></span>

    <span data-ttu-id="9d535-127">Certains composants ont été ajoutés dans hello [mise en route avec Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="9d535-127">Some components were added in hello [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="9d535-128">**CTRL** faire glisser à partir de composants hello en hello vue tooViewController.h et ajouter ces nouveaux prises.</span><span class="sxs-lookup"><span data-stu-id="9d535-128">**Ctrl** drag from hello components in hello view tooViewController.h and add these new outlets.</span></span>
   
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
2. <span data-ttu-id="9d535-129">Dans ViewController.h, ajoutez suivant de hello `#define` juste en dessous de vos instructions d’importation.</span><span class="sxs-lookup"><span data-stu-id="9d535-129">In ViewController.h, add hello following `#define` just below your import statements.</span></span> <span data-ttu-id="9d535-130">Hello de substitution *< Entrez de point de terminaison principal votre\>*  espace réservé par hello URL de Destination utilisé toodeploy de votre serveur principal d’application dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-130">Substitute hello *<Enter Your Backend Endpoint\>* placeholder with hello Destination URL you used toodeploy your app backend in hello previous section.</span></span> <span data-ttu-id="9d535-131">For example, *http://votre_serveur_principal.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="9d535-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="9d535-132">Dans votre projet, créez un nouveau **/Cocoa Touch de classe** nommé **RegisterClient** toointerface avec hello ASP.NET back-end, vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="9d535-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** toointerface with hello ASP.NET back-end you created.</span></span> <span data-ttu-id="9d535-133">Créer la classe hello héritant de `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="9d535-133">Create hello class inheriting from `NSObject`.</span></span> <span data-ttu-id="9d535-134">Ajoutez ensuite hello après Bonjour RegisterClient.h de code.</span><span class="sxs-lookup"><span data-stu-id="9d535-134">Then add hello following code in hello RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="9d535-135">Mettre à jour hello RegisterClient.m hello `@interface` section :</span><span class="sxs-lookup"><span data-stu-id="9d535-135">In hello RegisterClient.m update hello `@interface` section:</span></span>
   
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
5. <span data-ttu-id="9d535-136">Remplacez hello `@implementation` section Bonjour RegisterClient.m avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="9d535-136">Replace hello `@implementation` section in hello RegisterClient.m with hello following code.</span></span>

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

    <span data-ttu-id="9d535-137">code Hello ci-dessus implémente la logique de hello expliquée dans l’article d’aide sur hello [l’inscription à partir de votre serveur principal d’application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) tooperform reste à l’aide de NSURLSession appelle tooyour serveur principal d’application et NSUserDefaults toolocally magasin hello registrationId retourné par le concentrateur de notification hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-137">hello code above implements hello logic explained in hello guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession tooperform REST calls tooyour app backend, and NSUserDefaults toolocally store hello registrationId returned by hello notification hub.</span></span>

    <span data-ttu-id="9d535-138">Notez que cette classe nécessite sa propriété **authorizationHeader** toobe correctement défini dans l’ordre toowork.</span><span class="sxs-lookup"><span data-stu-id="9d535-138">Note that this class requires its property **authorizationHeader** toobe set in order toowork properly.</span></span> <span data-ttu-id="9d535-139">Cette propriété est définie par hello **ViewController** classe après connexion hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-139">This property is set by hello **ViewController** class after hello log in.</span></span>

1. <span data-ttu-id="9d535-140">Dans ViewController.h, ajoutez une instruction `#import` pour RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="9d535-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="9d535-141">Ensuite, ajoutez une déclaration pour le jeton du périphérique hello et référencer tooa `RegisterClient` instance Bonjour `@interface` section :</span><span class="sxs-lookup"><span data-stu-id="9d535-141">Then add a declaration for hello device token and reference tooa `RegisterClient` instance in hello `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="9d535-142">Dans ViewController.m, ajoutez une déclaration de méthode privée Bonjour `@interface` section :</span><span class="sxs-lookup"><span data-stu-id="9d535-142">In ViewController.m, add a private method declaration in hello `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create hello Authorization header tooperform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="9d535-143">Hello extrait de code suivant n’est pas un schéma d’authentification sécurisée, vous devez vous servir d’implémentation hello Hello **createAndSetAuthenticationHeaderWithUsername:AndPassword :** avec votre mécanisme d’authentification spécifique Cette opération génère un toobe de jeton d’authentification consommée par hello register classe de client, par exemple, OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d535-143">hello following snippet is not a secure authentication scheme, you should substitute hello implementation of hello **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token toobe consumed by hello register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="9d535-144">Ensuite, dans hello `@implementation` section de ViewController.m ajouter hello suivant du code qui ajoute l’implémentation hello pour le paramètre hello périphérique jeton et l’authentification d’un en-tête.</span><span class="sxs-lookup"><span data-stu-id="9d535-144">Then in hello `@implementation` section of ViewController.m add hello following code which adds hello implementation for setting hello device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="9d535-145">Notez comment le jeton du périphérique paramètre hello permet hello bouton se connecter.</span><span class="sxs-lookup"><span data-stu-id="9d535-145">Note how setting hello device token enables hello log in button.</span></span> <span data-ttu-id="9d535-146">Il s’agit, car dans le cadre de l’action de connexion hello, contrôleur de la vue hello inscrit pour les notifications push avec le serveur principal d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-146">This is becasue as a part of hello login action, hello view controller registers for push notifications with hello app backend.</span></span> <span data-ttu-id="9d535-147">Par conséquent, nous ne voulons pas se connecter action toobe accessible jusqu'à ce que le jeton du périphérique hello a été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="9d535-147">Hence, we do not want Log In action toobe accessible till hello device token has been properly set up.</span></span> <span data-ttu-id="9d535-148">Vous pouvez découpler journal hello dans à partir de l’enregistrement de push hello tant que première de hello se produit avant les hello ce dernier.</span><span class="sxs-lookup"><span data-stu-id="9d535-148">You can decouple hello log in from hello push registration as long as hello former happens before hello latter.</span></span>
2. <span data-ttu-id="9d535-149">Dans ViewController.m, utilisez hello suivant la méthode d’action des extraits de code tooimplement hello pour votre **connexion** bouton et une méthode toosend hello notification message à l’aide de ASP.NET principal hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-149">In ViewController.m, use hello following snippets tooimplement hello action method for your **Log In** button and a method toosend hello notification message using hello ASP.NET backend.</span></span>
   
       - <span data-ttu-id="9d535-150">(IBAction) LogInAction : expéditeur de (id) {/ / créer l’en-tête d’authentification et la définir dans le Registre client NSString * nom d’utilisateur = self. UsernameField.text ;   Le mot de passe NSString * = self. PasswordField.text ;</span><span class="sxs-lookup"><span data-stu-id="9d535-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="9d535-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="9d535-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="9d535-152">selfie __weak ViewController * = self ;   [self.registerClient registerWithDeviceToken:self.deviceToken balises : nil andCompletion:^(NSError* error) {Si ( ! erreur) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES ;               [self MessageBox:@"Success » message:@"Registered avec succès ! »] ;}) ;}}] ;}</span><span class="sxs-lookup"><span data-stu-id="9d535-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="9d535-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="9d535-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="9d535-154">Passez hello pns et nom d’utilisateur de balise en tant que paramètres avec ASP.NET toohello hello URL REST principal NSURL * requestURL = [NSURL URLWithString : [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @ », BACKEND_ENDPOINT, pns, usernameTag]] ;</span><span class="sxs-lookup"><span data-stu-id="9d535-154">// Pass hello pns and username tag as parameters with hello REST URL toohello ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="9d535-155">Demande de NSMutableURLRequest = [NSMutableURLRequest requestWithURL:requestURL] ;    [demande setHTTPMethod:@"POST »] ;</span><span class="sxs-lookup"><span data-stu-id="9d535-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="9d535-156">Obtenir les authenticationheader fictive hello client de Registre hello authorizationHeaderValue NSString * = [NSString stringWithFormat:@"Basic % @ », self.registerClient.authenticationHeader] ;    [demande setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization »] ;</span><span class="sxs-lookup"><span data-stu-id="9d535-156">// Get hello mock authenticationheader from hello register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="9d535-157">Ajouter le corps du message de notification hello [demande setValue:@"application/json;charset=utf-8 « forHTTPHeaderField:@"Content-Type »] ;    [demande setHTTPBody : [message dataUsingEncoding:NSUTF8StringEncoding]] ;</span><span class="sxs-lookup"><span data-stu-id="9d535-157">//Add hello notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="9d535-158">Exécution d’envoyer une notification hello API REST sur hello ASP.NET principal NSURLSessionDataTask * dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *erreur) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) réponse ;        Si (erreur || httpResponse.statusCode ! = 200) {NSString* état = [NSString stringWithFormat:@"Error état % @: % d\nError : %@\n», pns, httpResponse.statusCode, erreur] ;            dispatch_async(dispatch_get_main_queue(), ^ {/ / ajout de texte, car tous les appels PNS 3 peuvent également avoir des informations tooview [stringByAppendingString:status de setText:[self.sendResults.text self.sendResults]] ;            });            NSLog(status) ;        }</span><span class="sxs-lookup"><span data-stu-id="9d535-158">// Execute hello send notification REST API on hello ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information tooview                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="9d535-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="9d535-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="9d535-160">Mettre à jour action hello pour hello **envoyer une Notification** bouton toouse hello ASP.NET principal et envoyer tooany PNS activé par un commutateur.</span><span class="sxs-lookup"><span data-stu-id="9d535-160">Update hello action for hello **Send Notification** button toouse hello ASP.NET backend and send tooany PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="9d535-161">Dans la fonction **ViewDidLoad**, ajouter hello suit tooinstantiate hello RegisterClient instance et définir un délégué hello pour vos champs de texte.</span><span class="sxs-lookup"><span data-stu-id="9d535-161">In function **ViewDidLoad**, add hello following tooinstantiate hello RegisterClient instance and set hello delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="9d535-162">En **AppDelegate.m**, supprimez tout le contenu de la méthode hello hello **didRegisterForPushNotificationWithDeviceToken : l’application :** et remplacez-la par hello suivant toomake que hello vue contrôleur contient le dernier jeton du périphérique hello récupérée à partir de l’APNs :</span><span class="sxs-lookup"><span data-stu-id="9d535-162">Now in **AppDelegate.m**, remove all hello content of hello method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with hello following toomake sure that hello view controller contains hello latest device token retrieved from APNs:</span></span>
   
       // Add import toohello top of hello file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="9d535-163">Pour finir dans **AppDelegate.m**, assurez-vous que vous avez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="9d535-163">Finally in **AppDelegate.m**, make sure you have hello following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-hello-application"></a><span data-ttu-id="9d535-164">Hello de test Application</span><span class="sxs-lookup"><span data-stu-id="9d535-164">Test hello Application</span></span>
1. <span data-ttu-id="9d535-165">Dans XCode, exécutez l’application hello sur un appareil iOS physiques (push notifications ne fonctionnera pas dans le simulateur de hello).</span><span class="sxs-lookup"><span data-stu-id="9d535-165">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="9d535-166">Dans une application iOS de hello l’interface utilisateur, entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9d535-166">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="9d535-167">Il peuvent être n’importe quelle chaîne, mais ils doivent tous deux être hello même valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="9d535-167">These can be any string, but they must both be hello same string value.</span></span> <span data-ttu-id="9d535-168">Cliquez ensuite sur **Log In**.</span><span class="sxs-lookup"><span data-stu-id="9d535-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="9d535-169">Une fenêtre contextuelle doit s’afficher pour vous informer que l’inscription a abouti.</span><span class="sxs-lookup"><span data-stu-id="9d535-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="9d535-170">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d535-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="9d535-171">Bonjour **balise de nom d’utilisateur destinataire* texte, entrez l’étiquette de nom d’utilisateur hello utilisée avec l’inscription du hello à partir d’un autre périphérique.</span><span class="sxs-lookup"><span data-stu-id="9d535-171">In hello **Recipient username tag* text field, enter hello user name tag used with hello registration from another device.</span></span>
5. <span data-ttu-id="9d535-172">Entrez un message de notification et cliquez sur **Envoyer une notification**.</span><span class="sxs-lookup"><span data-stu-id="9d535-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="9d535-173">Seuls les appareils hello qui ont un enregistrement de balise de nom d’utilisateur destinataire hello recevoir message de notification de hello.</span><span class="sxs-lookup"><span data-stu-id="9d535-173">Only hello devices that have a registration with hello recipient user name tag receive hello notification message.</span></span>  <span data-ttu-id="9d535-174">Il est uniquement envoyé aux utilisateurs de toothose.</span><span class="sxs-lookup"><span data-stu-id="9d535-174">It is only sent toothose users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
