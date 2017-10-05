---
title: Azure Notification Hubs notifie les utilisateurs pour iOS avec backend .NET
description: "Découvrez comment envoyer des notifications Push aux utilisateurs dans Azure. Exemples de code écrits en Objective-C et l'API .NET pour le serveur principal."
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
ms.openlocfilehash: 0fa7a886e1ecb0a90b6aebc1dbf9ef0c6ce1acf1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-for-ios-with-net-backend"></a><span data-ttu-id="05755-104">Azure Notification Hubs notifie les utilisateurs pour iOS avec backend .NET</span><span class="sxs-lookup"><span data-stu-id="05755-104">Azure Notification Hubs Notify Users for iOS with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="05755-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="05755-105">Overview</span></span>
<span data-ttu-id="05755-106">La prise en charge des notifications Push dans Azure vous permet d’accéder à une infrastructure Push conviviale, multi-plateforme et avec montée en charge qui simplifie fortement l’implémentation des notifications Push pour les applications consommateur et entreprise pour les plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="05755-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="05755-107">Ce didacticiel explique comment utiliser Azure Notification Hubs pour envoyer des notifications Push à un utilisateur particulier d'une application sur un appareil spécifique.</span><span class="sxs-lookup"><span data-stu-id="05755-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="05755-108">Un code WebAPI principal ASP.NET est utilisé pour authentifier les clients et pour générer les notifications, comme le présente la rubrique d’aide [Inscription auprès du serveur principal de votre application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span><span class="sxs-lookup"><span data-stu-id="05755-108">An ASP.NET WebAPI backend is used to authenticate clients and to generate notifications, as shown in the guidance topic [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend).</span></span>

> [!NOTE]
> <span data-ttu-id="05755-109">Ce didacticiel repose sur l'hypothèse que vous avez créé et configuré votre concentrateur de notification comme décrit dans [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="05755-109">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span> <span data-ttu-id="05755-110">Ce didacticiel est également un prérequis pour le didacticiel sur les [notifications Push sécurisées (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="05755-110">This tutorial is also the prerequisite to the [Secure Push (iOS)](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md) tutorial.</span></span>
> <span data-ttu-id="05755-111">Si vous souhaitez utiliser Mobile Apps comme service principal, voir l’article [Mobile Apps concernant la prise en main des notifications Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="05755-111">If you want to use Mobile Apps as your backend service, see the [Mobile Apps Get Started with Push](../app-service-mobile/app-service-mobile-ios-get-started-push.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="modify-your-ios-app"></a><span data-ttu-id="05755-112">Modification de votre application iOS</span><span class="sxs-lookup"><span data-stu-id="05755-112">Modify your iOS app</span></span>
1. <span data-ttu-id="05755-113">Ouvrez l'application d'affichage Page simple que vous avez créée dans le didacticiel [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="05755-113">Open the Single Page view app you created in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="05755-114">Dans cette section, nous partons du principe que vous avez configuré votre projet avec un nom d’organisation vide.</span><span class="sxs-lookup"><span data-stu-id="05755-114">In this section we assume that your project is configured with an empty organization name.</span></span> <span data-ttu-id="05755-115">Si ce n’est pas le cas, vous devez ajouter le nom de votre organisation à tous les noms de classe.</span><span class="sxs-lookup"><span data-stu-id="05755-115">If not, you will need to prepend your organization name to all class names.</span></span>
   > 
   > 
2. <span data-ttu-id="05755-116">Dans Main.storyboard, ajoutez les composants indiqués dans la capture d'écran ci-dessous de la bibliothèque d'objets :</span><span class="sxs-lookup"><span data-stu-id="05755-116">In your Main.storyboard add the components shown in the screenshot below from the object library.</span></span>
   
    ![][1]
   
   * <span data-ttu-id="05755-117">**Nom d'utilisateur**: champ UITextField avec du texte d'espace réservé, *Entrer le nom d'utilisateur*, juste en dessous de l'étiquette des résultats d'envoi et entre les marges gauche et droite, en dessous de l'étiquette des résultats d'envoi.</span><span class="sxs-lookup"><span data-stu-id="05755-117">**Username**: A UITextField with placeholder text, *Enter Username*, immediately beneath the send results label and constrained to the left and right margins and beneath the send results label.</span></span>
   * <span data-ttu-id="05755-118">**Mot de passe**: champ UITextField avec du texte d'espace réservé, *Entrer le mot de passe*, juste en dessous du champ de texte du nom d'utilisateur et entre les marges gauche et droite, en dessous du champ de texte du nom d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="05755-118">**Password**: A UITextField with placeholder text, *Enter Password*, immediately beneath the username text field and constrained to the left and right margins and beneath the username text field.</span></span> <span data-ttu-id="05755-119">Cochez l'option **Sécuriser l'entrée de texte** dans l'inspecteur d'attributs sous *Touche Retour*.</span><span class="sxs-lookup"><span data-stu-id="05755-119">Check the **Secure Text Entry** option in the Attribute Inspector, under *Return Key*.</span></span>
   * <span data-ttu-id="05755-120">**Connexion** : un UIButton étiqueté immédiatement en dessous du champ de texte du mot de passe ; décochez l’option **Activé** dans l’inspecteur d’attributs, sous *Contrôle-Contenu*</span><span class="sxs-lookup"><span data-stu-id="05755-120">**Log in**: A UIButton labeled immediately beneath the password text field and uncheck the **Enabled** option in the Attributes Inspector, under *Control-Content*</span></span>
   * <span data-ttu-id="05755-121">**WNS**: étiquette et commutateur pour activer l'envoi de la notification du service de notification Windows, si elle a été configurée sur le hub.</span><span class="sxs-lookup"><span data-stu-id="05755-121">**WNS**: Label and switch to enable sending the notification Windows Notification Service if it has been setup on the hub.</span></span> <span data-ttu-id="05755-122">Consultez le didacticiel [Prise en main de Windows](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).</span><span class="sxs-lookup"><span data-stu-id="05755-122">See the [Windows Getting Started](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span>
   * <span data-ttu-id="05755-123">**GCM**: étiquette et commutateur pour activer l'envoi de la notification à Google Cloud Messaging, si elle a été configurée sur le hub.</span><span class="sxs-lookup"><span data-stu-id="05755-123">**GCM**: Label and switch to enable sending the notification to Google Cloud Messaging if it has been setup on the hub.</span></span> <span data-ttu-id="05755-124">Consultez le didacticiel [Prise en main d'Android](notification-hubs-android-push-notification-google-gcm-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="05755-124">See [Android Getting Started](notification-hubs-android-push-notification-google-gcm-get-started.md) tutorial.</span></span>
   * <span data-ttu-id="05755-125">**APNS**: étiquette et commutateur pour activer l'envoi de la notification au service de notification de la plateforme Apple.</span><span class="sxs-lookup"><span data-stu-id="05755-125">**APNS**: Label and switch to enable sending the notification to the Apple Platform Notification Service.</span></span>
   * <span data-ttu-id="05755-126">**Nom d'utilisateur du destinataire**: champ UITextField avec du texte d'espace réservé, *Balise du nom d'utilisateur du destinataire*, juste en dessous de l'étiquette GCM et entre les marges gauche et droite, en dessous de l'étiquette GCM.</span><span class="sxs-lookup"><span data-stu-id="05755-126">**Recipent Username**:A UITextField with placeholder text, *Recipient username tag*, immediately beneath the GCM label and constrained to the left and right margins and beneath the GCM label.</span></span>

    <span data-ttu-id="05755-127">Certains composants ont été ajoutés dans le didacticiel [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="05755-127">Some components were added in the [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md) tutorial.</span></span>

1. <span data-ttu-id="05755-128">**Ctrl** et faites glisser les composants de l'affichage vers ViewController.h, puis ajoutez ces nouvelles sorties.</span><span class="sxs-lookup"><span data-stu-id="05755-128">**Ctrl** drag from the components in the view to ViewController.h and add these new outlets.</span></span>
   
        @property (weak, nonatomic) IBOutlet UITextField *UsernameField;
        @property (weak, nonatomic) IBOutlet UITextField *PasswordField;
        @property (weak, nonatomic) IBOutlet UITextField *RecipientField;
        @property (weak, nonatomic) IBOutlet UITextField *NotificationField;
   
        // Used to enable the buttons on the UI
        @property (weak, nonatomic) IBOutlet UIButton *LogInButton;
        @property (weak, nonatomic) IBOutlet UIButton *SendNotificationButton;
   
        // Used to enabled sending notifications across platforms
        @property (weak, nonatomic) IBOutlet UISwitch *WNSSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *GCMSwitch;
        @property (weak, nonatomic) IBOutlet UISwitch *APNSSwitch;
   
        - (IBAction)LogInAction:(id)sender;
2. <span data-ttu-id="05755-129">Dans ViewController.h, ajoutez le code `#define` suivant juste en dessous de vos instructions d'importation.</span><span class="sxs-lookup"><span data-stu-id="05755-129">In ViewController.h, add the following `#define` just below your import statements.</span></span> <span data-ttu-id="05755-130">Remplacez l’espace réservé *<Enter Your Backend Endpoint\>* par l’URL de destination que vous avez utilisée pour déployer votre serveur principal d’application dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="05755-130">Substitute the *<Enter Your Backend Endpoint\>* placeholder with the Destination URL you used to deploy your app backend in the previous section.</span></span> <span data-ttu-id="05755-131">For example, *http://votre_serveur_principal.azurewebsites.net*.</span><span class="sxs-lookup"><span data-stu-id="05755-131">For example, *http://you_backend.azurewebsites.net*.</span></span>
   
        #define BACKEND_ENDPOINT @"<Enter Your Backend Endpoint>"
3. <span data-ttu-id="05755-132">Dans votre projet, créez une **classe Cocoa Touch** nommée **RegisterClient** pour communiquer avec le serveur principal ASP.NET que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="05755-132">In your project, create a new **Cocoa Touch class** named **RegisterClient** to interface with the ASP.NET back-end you created.</span></span> <span data-ttu-id="05755-133">Créez la classe en héritant de `NSObject`.</span><span class="sxs-lookup"><span data-stu-id="05755-133">Create the class inheriting from `NSObject`.</span></span> <span data-ttu-id="05755-134">Ensuite, ajoutez le code qui suit dans RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="05755-134">Then add the following code in the RegisterClient.h.</span></span>
   
        @interface RegisterClient : NSObject
   
        @property (strong, nonatomic) NSString* authenticationHeader;
   
        -(void) registerWithDeviceToken:(NSData*)token tags:(NSSet*)tags
            andCompletion:(void(^)(NSError*))completion;
   
        -(instancetype) initWithEndpoint:(NSString*)Endpoint;
   
        @end
4. <span data-ttu-id="05755-135">Dans RegisterClient.m, mettez à jour la section `@interface` :</span><span class="sxs-lookup"><span data-stu-id="05755-135">In the RegisterClient.m update the `@interface` section:</span></span>
   
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
5. <span data-ttu-id="05755-136">Remplacez la section `@implementation` dans RegisterClient.m par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="05755-136">Replace the `@implementation` section in the RegisterClient.m with the following code.</span></span>

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

    <span data-ttu-id="05755-137">Le code ci-dessus implémente la logique expliquée dans l'article [Inscription auprès du serveur principal de votre application](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) , et utilise NSURLSession pour passer des appels REST à votre serveur principal d'application et NSUserDefaults pour stocker en local la valeur registrationId renvoyée par le concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="05755-137">The code above implements the logic explained in the guidance article [Registering from your app backend](notification-hubs-push-notification-registration-management.md#registration-management-from-a-backend) using NSURLSession to perform REST calls to your app backend, and NSUserDefaults to locally store the registrationId returned by the notification hub.</span></span>

    <span data-ttu-id="05755-138">Notez que cette classe a besoin que sa propriété **authorizationHeader** soit définie afin de fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="05755-138">Note that this class requires its property **authorizationHeader** to be set in order to work properly.</span></span> <span data-ttu-id="05755-139">Cette propriété est définie par la classe **ViewController** après la connexion.</span><span class="sxs-lookup"><span data-stu-id="05755-139">This property is set by the **ViewController** class after the log in.</span></span>

1. <span data-ttu-id="05755-140">Dans ViewController.h, ajoutez une instruction `#import` pour RegisterClient.h.</span><span class="sxs-lookup"><span data-stu-id="05755-140">In ViewController.h, add a `#import` statement for RegisterClient.h.</span></span> <span data-ttu-id="05755-141">Ensuite, ajoutez une déclaration pour le jeton de l'appareil et faites référence à une instance `RegisterClient` dans la section `@interface` :</span><span class="sxs-lookup"><span data-stu-id="05755-141">Then add a declaration for the device token and reference to a `RegisterClient` instance in the `@interface` section:</span></span>
   
        #import "RegisterClient.h"
   
        @property (strong, nonatomic) NSData* deviceToken;
        @property (strong, nonatomic) RegisterClient* registerClient;
2. <span data-ttu-id="05755-142">Dans ViewController.m, ajoutez une déclaration de méthode privée dans la section `@interface` :</span><span class="sxs-lookup"><span data-stu-id="05755-142">In ViewController.m, add a private method declaration in the `@interface` section:</span></span>
   
        @interface ViewController () <UITextFieldDelegate, NSURLConnectionDataDelegate, NSXMLParserDelegate>
   
        // create the Authorization header to perform Basic authentication with your app back-end
        -(void) createAndSetAuthenticationHeaderWithUsername:(NSString*)username
                        AndPassword:(NSString*)password;
   
        @end

> [!NOTE]
> <span data-ttu-id="05755-143">L'extrait de code suivant n'étant pas un système d'authentification sécurisé, vous devez remplacer l'implémentation de **createAndSetAuthenticationHeaderWithUsername:AndPassword:** par votre mécanisme d'authentification spécifique qui génère un jeton d'authentification devant être consommé par la classe cliente du registre, par exemple, OAuth, Active Directory.</span><span class="sxs-lookup"><span data-stu-id="05755-143">The following snippet is not a secure authentication scheme, you should substitute the implementation of the **createAndSetAuthenticationHeaderWithUsername:AndPassword:** with your specific authentication mechanism that generates an authentication token to be consumed by the register client class, e.g. OAuth, Active Directory.</span></span>
> 
> 

1. <span data-ttu-id="05755-144">Ensuite, dans la section `@implementation` de ViewController.m, ajoutez le code suivant qui ajoute l'implémentation pour la définition du jeton de l'appareil et de l'en-tête de l'authentification.</span><span class="sxs-lookup"><span data-stu-id="05755-144">Then in the `@implementation` section of ViewController.m add the following code which adds the implementation for setting the device token and authentication header.</span></span>
   
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
   
    <span data-ttu-id="05755-145">Remarquez la façon dont le jeton de l’appareil active le bouton de connexion.</span><span class="sxs-lookup"><span data-stu-id="05755-145">Note how setting the device token enables the log in button.</span></span> <span data-ttu-id="05755-146">Ceci est dû au fait que dans le cadre de l’action de connexion, le contrôleur d’affichage s’inscrit aux notifications Push auprès du serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="05755-146">This is becasue as a part of the login action, the view controller registers for push notifications with the app backend.</span></span> <span data-ttu-id="05755-147">De ce fait, l’action de connexion ne doit pas être accessible tant que le jeton de l’appareil n’a pas été correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="05755-147">Hence, we do not want Log In action to be accessible till the device token has been properly set up.</span></span> <span data-ttu-id="05755-148">Vous pouvez découpler la connexion de l’inscription aux notifications Push dans la mesure où la connexion se produit avant l’inscription.</span><span class="sxs-lookup"><span data-stu-id="05755-148">You can decouple the log in from the push registration as long as the former happens before the latter.</span></span>
2. <span data-ttu-id="05755-149">Dans ViewController.m, utilisez les extraits de code suivants pour implémenter la méthode d'action de votre bouton **Connexion** et une méthode pour envoyer le message de notification à l'aide du serveur principal ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="05755-149">In ViewController.m, use the following snippets to implement the action method for your **Log In** button and a method to send the notification message using the ASP.NET backend.</span></span>
   
       - <span data-ttu-id="05755-150">(IBAction) LogInAction : expéditeur de (id) {/ / créer l’en-tête d’authentification et la définir dans le Registre client NSString * nom d’utilisateur = self. UsernameField.text ;   Le mot de passe NSString * = self. PasswordField.text ;</span><span class="sxs-lookup"><span data-stu-id="05755-150">(IBAction)LogInAction:(id)sender {   // create authentication header and set it in register client   NSString* username = self.UsernameField.text;   NSString* password = self.PasswordField.text;</span></span>
   
           <span data-ttu-id="05755-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span><span class="sxs-lookup"><span data-stu-id="05755-151">[self createAndSetAuthenticationHeaderWithUsername:username AndPassword:password];</span></span>
   
           <span data-ttu-id="05755-152">selfie __weak ViewController * = self ;   [self.registerClient registerWithDeviceToken:self.deviceToken balises : nil andCompletion:^(NSError* error) {Si ( ! erreur) {dispatch_async(dispatch_get_main_queue(), ^ {selfie. SendNotificationButton.enabled = YES ;               [self MessageBox:@"Success » message:@"Registered avec succès ! »] ;}) ;}}] ;}</span><span class="sxs-lookup"><span data-stu-id="05755-152">__weak ViewController* selfie = self;   [self.registerClient registerWithDeviceToken:self.deviceToken tags:nil       andCompletion:^(NSError* error) {       if (!error) {           dispatch_async(dispatch_get_main_queue(),           ^{               selfie.SendNotificationButton.enabled = YES;               [self MessageBox:@"Success" message:@"Registered successfully!"];           });       }   }]; }</span></span>

        <span data-ttu-id="05755-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span><span class="sxs-lookup"><span data-stu-id="05755-153">- (void)SendNotificationASPNETBackend:(NSString*)pns UsernameTag:(NSString*)usernameTag            Message:(NSString*)message {    NSURLSession* session = [NSURLSession        sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration] delegate:nil        delegateQueue:nil];</span></span>

            <span data-ttu-id="05755-154">Passer de la balise pns et le nom d’utilisateur en tant que paramètres avec l’URL de REST pour le serveur principal d’ASP.NET NSURL * requestURL = [NSURL URLWithString : [NSString stringWithFormat:@"%@/api/notifications? pns = % @& to_tag = % @ », BACKEND_ENDPOINT, pns, usernameTag]] ;</span><span class="sxs-lookup"><span data-stu-id="05755-154">// Pass the pns and username tag as parameters with the REST URL to the ASP.NET backend    NSURL* requestURL = [NSURL URLWithString:[NSString        stringWithFormat:@"%@/api/notifications?pns=%@&to_tag=%@", BACKEND_ENDPOINT, pns,        usernameTag]];</span></span>

            <span data-ttu-id="05755-155">Demande de NSMutableURLRequest = [NSMutableURLRequest requestWithURL:requestURL] ;    [demande setHTTPMethod:@"POST »] ;</span><span class="sxs-lookup"><span data-stu-id="05755-155">NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];    [request setHTTPMethod:@"POST"];</span></span>

            <span data-ttu-id="05755-156">Obtenir l’authenticationheader fictif à partir du client du Registre authorizationHeaderValue NSString * = [NSString stringWithFormat:@"Basic % @ », self.registerClient.authenticationHeader] ;    [demande setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization »] ;</span><span class="sxs-lookup"><span data-stu-id="05755-156">// Get the mock authenticationheader from the register client    NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@",        self.registerClient.authenticationHeader];    [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];</span></span>

            <span data-ttu-id="05755-157">Ajouter le corps du message de notification [demande setValue:@"application/json;charset=utf-8 « forHTTPHeaderField:@"Content-Type »] ;    [demande setHTTPBody : [message dataUsingEncoding:NSUTF8StringEncoding]] ;</span><span class="sxs-lookup"><span data-stu-id="05755-157">//Add the notification message body    [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];    [request setHTTPBody:[message dataUsingEncoding:NSUTF8StringEncoding]];</span></span>

            <span data-ttu-id="05755-158">Exécutez l’API REST envoyer une notification sur le dataTask ASP.NET principal NSURLSessionDataTask * = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError  *erreur) {NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) réponse ;        Si (erreur || httpResponse.statusCode ! = 200) {NSString* état = [NSString stringWithFormat:@"Error état % @: % d\nError : %@\n», pns, httpResponse.statusCode, erreur] ;            dispatch_async(dispatch_get_main_queue(), ^ {/ / ajout de texte, car tous les appels PNS 3 peuvent également avoir des informations à la vue [stringByAppendingString:status de setText:[self.sendResults.text self.sendResults]] ;            });            NSLog(status) ;        }</span><span class="sxs-lookup"><span data-stu-id="05755-158">// Execute the send notification REST API on the ASP.NET Backend    NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request        completionHandler:^(NSData *data, NSURLResponse *response, NSError *error)    {        NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;        if (error || httpResponse.statusCode != 200)        {            NSString* status = [NSString stringWithFormat:@"Error Status for %@: %d\nError: %@\n",                                pns, httpResponse.statusCode, error];            dispatch_async(dispatch_get_main_queue(),            ^{                // Append text because all 3 PNS calls may also have information to view                [self.sendResults setText:[self.sendResults.text stringByAppendingString:status]];            });            NSLog(status);        }</span></span>

                if (data != NULL)
                {
                    xmlParser = [[NSXMLParser alloc] initWithData:data];
                    [xmlParser setDelegate:self];
                    [xmlParser parse];
                }
            <span data-ttu-id="05755-159">}];    [dataTask resume]; }</span><span class="sxs-lookup"><span data-stu-id="05755-159">}];    [dataTask resume]; }</span></span>


1. <span data-ttu-id="05755-160">Mettez à jour l'action du bouton **Envoyer une notification** pour utiliser le serveur principal ASP.NET et effectuer l'envoi vers n'importe quel PNS activé par un commutateur.</span><span class="sxs-lookup"><span data-stu-id="05755-160">Update the action for the **Send Notification** button to use the ASP.NET backend and send to any PNS enabled by a switch.</span></span>

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



1. <span data-ttu-id="05755-161">Dans la fonction **ViewDidLoad**, ajoutez ce qui suit pour instancier l'instance de RegisterClient et définir le délégué pour vos champs de texte.</span><span class="sxs-lookup"><span data-stu-id="05755-161">In function **ViewDidLoad**, add the following to instantiate the RegisterClient instance and set the delegate for your text fields.</span></span>
   
       self.UsernameField.delegate = self;
       self.PasswordField.delegate = self;
       self.RecipientField.delegate = self;
       self.registerClient = [[RegisterClient alloc] initWithEndpoint:BACKEND_ENDPOINT];
2. <span data-ttu-id="05755-162">À présent, dans **AppDelegate.m**, supprimez tout le contenu de la méthode **application:didRegisterForPushNotificationWithDeviceToken:** et remplacez-le par ce qui suit pour faire en sorte que le contrôleur d’affichage contienne le dernier jeton de l’appareil extrait d’APNs :</span><span class="sxs-lookup"><span data-stu-id="05755-162">Now in **AppDelegate.m**, remove all the content of the method **application:didRegisterForPushNotificationWithDeviceToken:** and replace it with the following to make sure that the view controller contains the latest device token retrieved from APNs:</span></span>
   
       // Add import to the top of the file
       #import "ViewController.h"
   
       - (void)application:(UIApplication *)application
                   didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
       {
           ViewController* rvc = (ViewController*) self.window.rootViewController;
           rvc.deviceToken = deviceToken;
       }
3. <span data-ttu-id="05755-163">Enfin, assurez-vous qu' **AppDelegate.m**contient la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="05755-163">Finally in **AppDelegate.m**, make sure you have the following method:</span></span>
   
       - (void)application:(UIApplication *)application didReceiveRemoteNotification: (NSDictionary *)userInfo {
           NSLog(@"%@", userInfo);
           [self MessageBox:@"Notification" message:[[userInfo objectForKey:@"aps"] valueForKey:@"alert"]];
       }

## <a name="test-the-application"></a><span data-ttu-id="05755-164">Tester l'application</span><span class="sxs-lookup"><span data-stu-id="05755-164">Test the Application</span></span>
1. <span data-ttu-id="05755-165">Dans XCode, exécutez l’application sur un appareil iOS physique (les notifications Push ne fonctionnent pas dans le simulateur).</span><span class="sxs-lookup"><span data-stu-id="05755-165">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="05755-166">Dans l’interface utilisateur de l’application iOS, entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="05755-166">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="05755-167">La valeur peut être une chaîne quelconque, mais elle doit être identique pour les deux.</span><span class="sxs-lookup"><span data-stu-id="05755-167">These can be any string, but they must both be the same string value.</span></span> <span data-ttu-id="05755-168">Cliquez ensuite sur **Log In**.</span><span class="sxs-lookup"><span data-stu-id="05755-168">Then click **Log In**.</span></span>
   
    ![][2]
3. <span data-ttu-id="05755-169">Une fenêtre contextuelle doit s’afficher pour vous informer que l’inscription a abouti.</span><span class="sxs-lookup"><span data-stu-id="05755-169">You should see a pop-up informing you of registration success.</span></span> <span data-ttu-id="05755-170">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="05755-170">Click **OK**.</span></span>
   
    ![][3]
4. <span data-ttu-id="05755-171">Dans le champ de texte **Balise de nom d’utilisateur du destinataire* , entrez la balise de nom d’utilisateur utilisée lors de l’enregistrement sur un autre appareil.</span><span class="sxs-lookup"><span data-stu-id="05755-171">In the **Recipient username tag* text field, enter the user name tag used with the registration from another device.</span></span>
5. <span data-ttu-id="05755-172">Entrez un message de notification et cliquez sur **Envoyer une notification**.</span><span class="sxs-lookup"><span data-stu-id="05755-172">Enter a notification message and click **Send Notification**.</span></span>  <span data-ttu-id="05755-173">Seuls les appareils qui disposent d'un enregistrement avec la balise de nom d'utilisateur du destinataire reçoivent le message de notification.</span><span class="sxs-lookup"><span data-stu-id="05755-173">Only the devices that have a registration with the recipient user name tag receive the notification message.</span></span>  <span data-ttu-id="05755-174">Il n'est envoyé qu'à ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="05755-174">It is only sent to those users.</span></span>
   
    ![][4]

[1]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-interface.png
[2]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-user-pwd.png
[3]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-registered.png
[4]: ./media/notification-hubs-aspnet-backend-ios-notify-users/notification-hubs-ios-notify-users-enter-msg.png
