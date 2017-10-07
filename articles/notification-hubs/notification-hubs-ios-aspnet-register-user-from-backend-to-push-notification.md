---
title: "Inscription de l’utilisateur actif aux notifications Push au moyen de l’API Web | Microsoft Docs"
description: "Découvrez comment demander l’inscription aux notifications Push dans une application iOS avec Azure Notification Hubs lorsque l’inscription est réalisée par l’API web ASP.NET."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 4e3772cf-20db-4b9f-bb74-886adfaaa65d
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: fd56bb2dd627b31f00363851a4e76484aa382988
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="register-the-current-user-for-push-notifications-by-using-aspnet"></a><span data-ttu-id="823ac-103">Inscription de l’utilisateur actif aux notifications Push à l’aide d’ASP.NET</span><span class="sxs-lookup"><span data-stu-id="823ac-103">Register the current user for push notifications by using ASP.NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="823ac-104">iOS</span><span class="sxs-lookup"><span data-stu-id="823ac-104">iOS</span></span>](notification-hubs-ios-aspnet-register-user-from-backend-to-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="823ac-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="823ac-105">Overview</span></span>
<span data-ttu-id="823ac-106">Cette rubrique montre comment demander une inscription aux notifications Push avec Azure Notification Hubs lorsque l’inscription est réalisée par l’API Web ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="823ac-106">This topic shows you how to request push notification registration with Azure Notification Hubs when registration is performed by ASP.NET Web API.</span></span> <span data-ttu-id="823ac-107">Cette rubrique s'inscrit dans le prolongement du didacticiel [Notification des utilisateurs avec Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="823ac-107">This topic extends the tutorial [Notify users with Notification Hubs].</span></span> <span data-ttu-id="823ac-108">Vous devez avoir suivi les étapes de ce didacticiel permettant de créer le service mobile authentifié.</span><span class="sxs-lookup"><span data-stu-id="823ac-108">You must have already completed the required steps in that tutorial to create the authenticated mobile service.</span></span> <span data-ttu-id="823ac-109">Pour plus d'informations sur les scénarios de notification des utilisateurs, consultez la rubrique [Notification des utilisateurs avec Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="823ac-109">For more information on the notify users scenario, see [Notify users with Notification Hubs].</span></span>

## <a name="update-your-app"></a><span data-ttu-id="823ac-110">Mise à jour de votre application</span><span class="sxs-lookup"><span data-stu-id="823ac-110">Update your app</span></span>
1. <span data-ttu-id="823ac-111">Dans MainStoryboard_iPhone.storyboard, ajoutez les composants suivants de la bibliothèque d'objets :</span><span class="sxs-lookup"><span data-stu-id="823ac-111">In your MainStoryboard_iPhone.storyboard, add the following components from the object library:</span></span>
   
   * <span data-ttu-id="823ac-112">**Étiquette**: « Envoi d’une notification Push à l’utilisateur avec Notification Hubs »</span><span class="sxs-lookup"><span data-stu-id="823ac-112">**Label**: "Push to User with Notification Hubs"</span></span>
   * <span data-ttu-id="823ac-113">**Étiquette**: « InstallationId »</span><span class="sxs-lookup"><span data-stu-id="823ac-113">**Label**: "InstallationId"</span></span>
   * <span data-ttu-id="823ac-114">**Étiquette**: « Utilisateur »</span><span class="sxs-lookup"><span data-stu-id="823ac-114">**Label**: "User"</span></span>
   * <span data-ttu-id="823ac-115">**Zone de texte**: « Utilisateur »</span><span class="sxs-lookup"><span data-stu-id="823ac-115">**Text Field**: "User"</span></span>
   * <span data-ttu-id="823ac-116">**Étiquette**: « Mot de passe »</span><span class="sxs-lookup"><span data-stu-id="823ac-116">**Label**: "Password"</span></span>
   * <span data-ttu-id="823ac-117">**Zone de texte**: « Mot de passe »</span><span class="sxs-lookup"><span data-stu-id="823ac-117">**Text Field**: "Password"</span></span>
   * <span data-ttu-id="823ac-118">**Bouton**: « Connexion »</span><span class="sxs-lookup"><span data-stu-id="823ac-118">**Button**: "Login"</span></span>
     
     <span data-ttu-id="823ac-119">À ce stade, votre storyboard a normalement l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="823ac-119">At this point, your storyboard looks like the following:</span></span>
     
      ![][0]
2. <span data-ttu-id="823ac-120">Dans l’éditeur de l’Assistant, créez des outlets pour tous les contrôles commutés et appelez-les, connectez les champs texte au View Controller (délegué), puis créez une **Action** pour le bouton **login**.</span><span class="sxs-lookup"><span data-stu-id="823ac-120">In the assistant editor, create outlets for all the switched controls and call them, connect the text fields with the View Controller (delegate), and create an **Action** for the **login** button.</span></span>
   
       ![][1]
   
       Your BreakingNewsViewController.h file should now contain the following code:
   
        @property (weak, nonatomic) IBOutlet UILabel *installationId;
        @property (weak, nonatomic) IBOutlet UITextField *User;
        @property (weak, nonatomic) IBOutlet UITextField *Password;
   
        - (IBAction)login:(id)sender;
3. <span data-ttu-id="823ac-121">Créez une classe nommée **DeviceInfo**, puis copiez le code suivant dans la section de l'interface du fichier DeviceInfo.h :</span><span class="sxs-lookup"><span data-stu-id="823ac-121">Create a class named **DeviceInfo**, and copy the following code into the interface section of the file DeviceInfo.h:</span></span>
   
        @property (readonly, nonatomic) NSString* installationId;
        @property (nonatomic) NSData* deviceToken;
4. <span data-ttu-id="823ac-122">Copiez le code suivant dans la section d'implémentation du fichier DeviceInfo.m :</span><span class="sxs-lookup"><span data-stu-id="823ac-122">Copy the following code in the implementation section of the DeviceInfo.m file:</span></span>
   
            @synthesize installationId = _installationId;
   
            - (id)init {
                if (!(self = [super init]))
                    return nil;
   
                NSUserDefaults *defaults = [NSUserDefaults standardUserDefaults];
                _installationId = [defaults stringForKey:@"PushToUserInstallationId"];
                if(!_installationId) {
                    CFUUIDRef newUUID = CFUUIDCreate(kCFAllocatorDefault);
                    _installationId = (__bridge_transfer NSString *)CFUUIDCreateString(kCFAllocatorDefault, newUUID);
                    CFRelease(newUUID);
   
                    //store the install ID so we don't generate a new one next time
                    [defaults setObject:_installationId forKey:@"PushToUserInstallationId"];
                    [defaults synchronize];
                }
   
                return self;
            }
   
            - (NSString*)getDeviceTokenInHex {
                const unsigned *tokenBytes = [[self deviceToken] bytes];
                NSString *hexToken = [NSString stringWithFormat:@"%08X%08X%08X%08X%08X%08X%08X%08X",
                                      ntohl(tokenBytes[0]), ntohl(tokenBytes[1]), ntohl(tokenBytes[2]),
                                      ntohl(tokenBytes[3]), ntohl(tokenBytes[4]), ntohl(tokenBytes[5]),
                                      ntohl(tokenBytes[6]), ntohl(tokenBytes[7])];
                return hexToken;
            }
5. <span data-ttu-id="823ac-123">Dans PushToUserAppDelegate.h, ajoutez le singleton de propriété suivant :</span><span class="sxs-lookup"><span data-stu-id="823ac-123">In PushToUserAppDelegate.h, add the following property singleton:</span></span>
   
        @property (strong, nonatomic) DeviceInfo* deviceInfo;
6. <span data-ttu-id="823ac-124">Dans la méthode **didFinishLaunchingWithOptions** du fichier PushToUserAppDelegate.m, ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="823ac-124">In the **didFinishLaunchingWithOptions** method in PushToUserAppDelegate.m, add the following code:</span></span>
   
        self.deviceInfo = [[DeviceInfo alloc] init];
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound];
   
    <span data-ttu-id="823ac-125">La première ligne initialise le singleton **DeviceInfo** .</span><span class="sxs-lookup"><span data-stu-id="823ac-125">The first line initializes the **DeviceInfo** singleton.</span></span> <span data-ttu-id="823ac-126">La seconde ligne lance l'inscription pour les notifications Push, qui est déjà présente si vous avez préalablement suivi le didacticiel [Prise en main de Notification Hubs] .</span><span class="sxs-lookup"><span data-stu-id="823ac-126">The second line starts the registration for push notifications, which is already present is you have already completed the [Get Started with Notification Hubs] tutorial.</span></span>
7. <span data-ttu-id="823ac-127">Dans PushToUserAppDelegate.m, implémentez la méthode **didRegisterForRemoteNotificationsWithDeviceToken** dans AppDelegate et ajoutez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="823ac-127">In PushToUserAppDelegate.m, implement the method **didRegisterForRemoteNotificationsWithDeviceToken** in your AppDelegate and add the following code:</span></span>
   
        self.deviceInfo.deviceToken = deviceToken;
   
    <span data-ttu-id="823ac-128">Cela définit le jeton d’appareil de la requête.</span><span class="sxs-lookup"><span data-stu-id="823ac-128">This sets the device token for the request.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="823ac-129">À ce stade, il ne doit pas y avoir d’autre code dans cette méthode.</span><span class="sxs-lookup"><span data-stu-id="823ac-129">At this point, there should not be any other code in this method.</span></span> <span data-ttu-id="823ac-130">S'il existe déjà un appel à la méthode **registerNativeWithDeviceToken** que vous avez ajoutée lorsque vous avez suivi le didacticiel [Prise en main de Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) , vous devez placer l'appel en commentaire ou le supprimer.</span><span class="sxs-lookup"><span data-stu-id="823ac-130">If you already have a call to the **registerNativeWithDeviceToken** method that was added when you completed the [Get Started with Notification Hubs](/manage/services/notification-hubs/get-started-notification-hubs-ios/) tutorial, you must comment-out or remove that call.</span></span>
   > 
   > 
8. <span data-ttu-id="823ac-131">Dans le fichier PushToUserAppDelegate.m, ajoutez la méthode de gestionnaire suivante :</span><span class="sxs-lookup"><span data-stu-id="823ac-131">In the PushToUserAppDelegate.m file, add the following handler method:</span></span>
   
   * <span data-ttu-id="823ac-132">application (void) :(UIApplication *) application didReceiveRemoteNotification :(NSDictionary *) userInfo {NSLog (@ « % @ », userInfo) ;   UIAlertView * alerte = [[alloc UIAlertView] initWithTitle:@"Notification » message : [userInfo objectForKey:@"inAppMessage »] délégué : nil cancelButtonTitle : @ otherButtonTitles:nil de « OK », nil] ;   [afficher alerte] ; }</span><span class="sxs-lookup"><span data-stu-id="823ac-132">(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {   NSLog(@"%@", userInfo);   UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:                         [userInfo objectForKey:@"inAppMessage"] delegate:nil cancelButtonTitle:                         @"OK" otherButtonTitles:nil, nil];   [alert show]; }</span></span>
   
   <span data-ttu-id="823ac-133">Cette méthode affiche une alerte dans l'interface utilisateur lorsque votre application reçoit des notifications alors qu'elle est en cours d'exécution.</span><span class="sxs-lookup"><span data-stu-id="823ac-133">This method displays an alert in the UI when your app receives notifications while it is running.</span></span>
9. <span data-ttu-id="823ac-134">Ouvrez le fichier PushToUserViewController.m et revenez au clavier dans l'implémentation suivante :</span><span class="sxs-lookup"><span data-stu-id="823ac-134">Open the PushToUserViewController.m file, and return the keyboard in the following implementation:</span></span>
   
        - (BOOL)textFieldShouldReturn:(UITextField *)theTextField {
            if (theTextField == self.User || theTextField == self.Password) {
                [theTextField resignFirstResponder];
            }
            return YES;
        }
10. <span data-ttu-id="823ac-135">Dans la méthode **viewDidLoad** du fichier PushToUserViewController.m, initialisez l'étiquette installationId comme suit :</span><span class="sxs-lookup"><span data-stu-id="823ac-135">In the **viewDidLoad** method in the PushToUserViewController.m file, initialize the installationId label as follows:</span></span>
    
         DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
         Self.installationId.text = deviceInfo.installationId;
11. <span data-ttu-id="823ac-136">Ajoutez les propriétés suivantes à l'interface du fichier PushToUserViewController.m :</span><span class="sxs-lookup"><span data-stu-id="823ac-136">Add the following properties in interface in PushToUserViewController.m:</span></span>
    
        @property (readonly) NSOperationQueue* downloadQueue;
        - (NSString*)base64forData:(NSData*)theData;
12. <span data-ttu-id="823ac-137">Ajoutez ensuite l'implémentation suivante :</span><span class="sxs-lookup"><span data-stu-id="823ac-137">Then, add the following implementation:</span></span>
    
            - (NSOperationQueue *)downloadQueue {
                if (!_downloadQueue) {
                    _downloadQueue = [[NSOperationQueue alloc] init];
                    _downloadQueue.name = @"Download Queue";
                    _downloadQueue.maxConcurrentOperationCount = 1;
                }
                return _downloadQueue;
            }
    
            // base64 encoding
            - (NSString*)base64forData:(NSData*)theData
            {
                const uint8_t* input = (const uint8_t*)[theData bytes];
                NSInteger length = [theData length];
    
                static char table[] = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
    
                NSMutableData* data = [NSMutableData dataWithLength:((length + 2) / 3) * 4];
                uint8_t* output = (uint8_t*)data.mutableBytes;
    
                NSInteger i;
                for (i=0; i < length; i += 3) {
                    NSInteger value = 0;
                    NSInteger j;
                    for (j = i; j < (i + 3); j++) {
                        value <<= 8;
    
                        if (j < length) {
                            value |= (0xFF & input[j]);
                        }
                    }
    
                    NSInteger theIndex = (i / 3) * 4;
                    output[theIndex + 0] =                    table[(value >> 18) & 0x3F];
                    output[theIndex + 1] =                    table[(value >> 12) & 0x3F];
                    output[theIndex + 2] = (i + 1) < length ? table[(value >> 6)  & 0x3F] : '=';
                    output[theIndex + 3] = (i + 2) < length ? table[(value >> 0)  & 0x3F] : '=';
                }
    
                return [[NSString alloc] initWithData:data encoding:NSASCIIStringEncoding];
            }
13. <span data-ttu-id="823ac-138">Copiez le code suivant dans la méthode de gestionnaire **login** créée par XCode :</span><span class="sxs-lookup"><span data-stu-id="823ac-138">Copy the following code into the **login** handler method created by XCode:</span></span>
    
            DeviceInfo* deviceInfo = [(PushToUserAppDelegate*)[[UIApplication sharedApplication]delegate] deviceInfo];
    
            // build JSON
            NSString* json = [NSString stringWithFormat:@"{\"platform\":\"ios\", \"instId\":\"%@\", \"deviceToken\":\"%@\"}", deviceInfo.installationId, [deviceInfo getDeviceTokenInHex]];
    
            // build auth string
            NSString* authString = [NSString stringWithFormat:@"%@:%@", self.User.text, self.Password.text];
    
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://nhnotifyuser.azurewebsites.net/api/register"]];
            [request setHTTPMethod:@"POST"];
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];
            [request addValue:[@([json lengthOfBytesUsingEncoding:NSUTF8StringEncoding]) description] forHTTPHeaderField:@"Content-Length"];
            [request addValue:@"application/json" forHTTPHeaderField:@"Content-Type"];
            [request addValue:[NSString stringWithFormat:@"Basic %@",[self base64forData:[authString dataUsingEncoding:NSUTF8StringEncoding]]] forHTTPHeaderField:@"Authorization"];
    
            // connect with POST
            [NSURLConnection sendAsynchronousRequest:request queue:[self downloadQueue] completionHandler:^(NSURLResponse* response, NSData* data, NSError* error) {
                // add UIAlert depending on response.
                if (error != nil) {
                    NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*)response;
                    if ([httpResponse statusCode] == 200) {
                        UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Back-end registration" message:@"Registration successful" delegate:nil cancelButtonTitle: @"OK" otherButtonTitles:nil, nil];
                        [alert show];
                    } else {
                        NSLog(@"status: %ld", (long)[httpResponse statusCode]);
                    }
                } else {
                    NSLog(@"error: %@", error);
                }
            }];
    
    <span data-ttu-id="823ac-139">Cette méthode obtient à la fois un ID d'installation et un canal pour les notifications Push et les envoie avec le type d'appareil à la méthode d'API Web authentifiée qui crée une inscription dans Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="823ac-139">This method gets both an installation ID and channel for push notifications and sends it, along with the device type, to the authenticated Web API method that creates a registration in Notification Hubs.</span></span> <span data-ttu-id="823ac-140">Cette API Web a été définie dans le cadre du didacticiel [Notification des utilisateurs avec Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="823ac-140">This Web API was defined in [Notify users with Notification Hubs].</span></span>

<span data-ttu-id="823ac-141">Maintenant que l'application cliente est à jour, retournez au didacticiel [Notification des utilisateurs avec Notification Hubs] et mettez le service mobile à jour pour qu'il envoie des notifications à l'aide de Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="823ac-141">Now that the client app has been updated, return to the [Notify users with Notification Hubs] and update the mobile service to send notifications by using Notification Hubs.</span></span>

<!-- Anchors. -->

<!-- Images. -->
[0]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios1.png
[1]: ./media/notification-hubs-ios-aspnet-register-user-push-notifications/notification-hub-user-aspnet-ios2.png

<!-- URLs. -->
<span data-ttu-id="823ac-142">[Notification des utilisateurs avec Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="823ac-142">[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users-aspnet</span></span>

<span data-ttu-id="823ac-143">[Prise en main de Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span><span class="sxs-lookup"><span data-stu-id="823ac-143">[Get Started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-ios</span></span>