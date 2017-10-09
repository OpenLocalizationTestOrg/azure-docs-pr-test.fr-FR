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
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="8c617-104">Notifications Push enrichies avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="8c617-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="8c617-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="8c617-105">Overview</span></span>
<span data-ttu-id="8c617-106">Dans l’ordre tooengage les utilisateurs instantanée contenu riche, une application peut vouloir toopush au-delà de texte brut.</span><span class="sxs-lookup"><span data-stu-id="8c617-106">In order tooengage users with instant rich contents, an application might want toopush beyond plain text.</span></span> <span data-ttu-id="8c617-107">Ces notifications promeuvent les interactions entre utilisateurs et présentent du contenu tel que des URL, des sons, des images/coupons et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="8c617-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="8c617-108">Ce didacticiel s’appuie sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) rubrique et montre comment toosend push notifications qui incorporent des charges utiles (par exemple, image).</span><span class="sxs-lookup"><span data-stu-id="8c617-108">This tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how toosend push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="8c617-109">Ce didacticiel est compatible avec iOS 7 et 8.</span><span class="sxs-lookup"><span data-stu-id="8c617-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="8c617-110">À un niveau élevé :</span><span class="sxs-lookup"><span data-stu-id="8c617-110">At a high level:</span></span>

1. <span data-ttu-id="8c617-111">serveur principal d’application Hello :</span><span class="sxs-lookup"><span data-stu-id="8c617-111">hello app backend:</span></span>
   * <span data-ttu-id="8c617-112">Magasins hello riche charge utile (dans ce cas, l’image) dans le stockage de base de données/local hello principal</span><span class="sxs-lookup"><span data-stu-id="8c617-112">Stores hello rich payload (in this case, image) in hello backend database/local storage</span></span>
   * <span data-ttu-id="8c617-113">Envoie l’ID du périphérique toohello enrichi de notification</span><span class="sxs-lookup"><span data-stu-id="8c617-113">Sends ID of this rich notification toohello device</span></span>
2. <span data-ttu-id="8c617-114">Application sur l’appareil de hello :</span><span class="sxs-lookup"><span data-stu-id="8c617-114">App on hello device:</span></span>
   * <span data-ttu-id="8c617-115">Contacts hello principal demandant la charge utile de riches hello avec l’ID de hello qu’il reçoit</span><span class="sxs-lookup"><span data-stu-id="8c617-115">Contacts hello backend requesting hello rich payload with hello ID it receives</span></span>
   * <span data-ttu-id="8c617-116">Envoie des notifications d’utilisateurs sur l’appareil de hello lors de la récupération des données est terminée et affiche la charge utile de hello immédiatement lorsque les utilisateurs appuient sur toolearn plus</span><span class="sxs-lookup"><span data-stu-id="8c617-116">Sends users notifications on hello device when data retrieval is complete, and shows hello payload immediately when users tap toolearn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="8c617-117">Projet WebAPI</span><span class="sxs-lookup"><span data-stu-id="8c617-117">WebAPI Project</span></span>
1. <span data-ttu-id="8c617-118">Dans Visual Studio, ouvrez hello **AppBackend** projet que vous avez créé dans hello [avertir les utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8c617-118">In Visual Studio, open hello **AppBackend** project that you created in hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="8c617-119">Obtenir une image vous que les utilisateurs de toonotify avec et placez-le dans un **img** dossier dans votre répertoire de projet.</span><span class="sxs-lookup"><span data-stu-id="8c617-119">Obtain an image you would like toonotify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="8c617-120">Cliquez sur **afficher tous les fichiers** dans hello l’Explorateur de solutions et cliquez sur le dossier de hello trop**inclure dans le projet**.</span><span class="sxs-lookup"><span data-stu-id="8c617-120">Click **Show All Files** in hello Solution Explorer, and right-click hello folder too**Include In Project**.</span></span>
4. <span data-ttu-id="8c617-121">Image hello sélectionnée, de modifier son Action de génération dans la fenêtre Propriétés trop**ressource incorporée**.</span><span class="sxs-lookup"><span data-stu-id="8c617-121">With hello image selected, change its Build Action in Properties window too**Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="8c617-122">Dans **Notifications.cs**, ajoutez hello qui suit à l’aide d’instruction :</span><span class="sxs-lookup"><span data-stu-id="8c617-122">In **Notifications.cs**, add hello following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="8c617-123">Hello de mise à jour entière **Notifications** classe avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="8c617-123">Update hello whole **Notifications** class with hello following code.</span></span> <span data-ttu-id="8c617-124">Être tooreplace que des espaces réservés de hello avec vos informations d’identification du hub de notification et le nom du fichier image.</span><span class="sxs-lookup"><span data-stu-id="8c617-124">Be sure tooreplace hello placeholders with your notification hub credentials and image file name.</span></span>
   
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
   > <span data-ttu-id="8c617-125">(facultatif) Consultez trop[comment tooembed et l’accès aux ressources à l’aide de Visual C#](http://support.microsoft.com/kb/319292) pour plus d’informations sur la façon de tooadd et obtenir des ressources de projet.</span><span class="sxs-lookup"><span data-stu-id="8c617-125">(optional) Refer too[How tooembed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how tooadd and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="8c617-126">Dans **NotificationsController.cs**, redéfinir **NotificationsController** avec hello suivant des extraits de code.</span><span class="sxs-lookup"><span data-stu-id="8c617-126">In **NotificationsController.cs**, redefine **NotificationsController**  with hello following snippets.</span></span> <span data-ttu-id="8c617-127">Cela envoie un toodevice id de la notification initiale riche en mode silencieux et permet l’extraction du côté client de l’image :</span><span class="sxs-lookup"><span data-stu-id="8c617-127">This sends an initial silent rich notification id toodevice and allows client-side retrieval of image:</span></span>
   
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
8. <span data-ttu-id="8c617-128">Maintenant nous sera redéployer cette application de tooan site Web Azure dans l’ordre toomake accessible à partir de tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="8c617-128">Now we will re-deploy this app tooan Azure Website in order toomake it accessible from all devices.</span></span> <span data-ttu-id="8c617-129">Avec le bouton droit sur hello **AppBackend** de projet et sélectionnez **publier**.</span><span class="sxs-lookup"><span data-stu-id="8c617-129">Right-click on hello **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="8c617-130">Sélectionnez Site web Azure comme cible de publication.</span><span class="sxs-lookup"><span data-stu-id="8c617-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="8c617-131">Connectez-vous avec votre compte Azure, sélectionnez un site Web existant ou nouveau et prenez note de hello **URL de destination** propriété Bonjour **connexion** onglet. Nous appelons URL toothis comme votre *point de terminaison principal* plus loin dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8c617-131">Log in with your Azure account and select an existing or new Website, and make a note of hello **destination URL** property in hello **Connection** tab. We will refer toothis URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="8c617-132">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="8c617-132">Click **Publish**.</span></span>

## <a name="modify-hello-ios-project"></a><span data-ttu-id="8c617-133">Modifier le projet iOS de hello</span><span class="sxs-lookup"><span data-stu-id="8c617-133">Modify hello iOS project</span></span>
<span data-ttu-id="8c617-134">Maintenant que vous avez modifié votre hello simplement d’application back-end toosend *id* d’une notification, vous allez modifier votre toohandle d’application iOS cet id et récupérer le message de type hello enrichi à partir de votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="8c617-134">Now that you have modified your app backend toosend just hello *id* of a notification, you will change your iOS app toohandle that id and retrieve hello rich message from your backend.</span></span>

1. <span data-ttu-id="8c617-135">Ouvrez votre projet iOS et activer les notifications à distance en accédant de cible tooyour principal de l’application Bonjour **cibles** section.</span><span class="sxs-lookup"><span data-stu-id="8c617-135">Open your iOS project, and enable remote notifications by going tooyour main app target in hello **Targets** section.</span></span>
2. <span data-ttu-id="8c617-136">Cliquez sur **fonctionnalités**, activez **Modes d’arrière-plan**et vérifiez hello **des Notifications à distance** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="8c617-136">Click on **Capabilities**, turn on **Background Modes**, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="8c617-137">Accédez trop**Main.storyboard**et assurez-vous que vous disposez d’un contrôleur de vue (indiqué tooas accueil View Controller dans ce didacticiel) à partir de [notifier l’utilisateur](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="8c617-137">Go too**Main.storyboard**, and make sure you have a View Controller (refered tooas Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="8c617-138">Ajouter un **Navigation contrôleur** tooyour d’animation et faites glisser la touche contrôle toomake de vue contrôleur tooHome il hello **racine vue** de navigation.</span><span class="sxs-lookup"><span data-stu-id="8c617-138">Add a **Navigation Controller** tooyour storyboard, and control-drag tooHome View Controller toomake it hello **root view** of navigation.</span></span> <span data-ttu-id="8c617-139">Vérifiez que hello **contrôleur d’affichage Initial est** dans les attributs inspecteur est sélectionné pour hello contrôleur de Navigation.</span><span class="sxs-lookup"><span data-stu-id="8c617-139">Make sure hello **Is Initial View Controller** in Attributes inspector is selected for hello Navigation Controller only.</span></span>
5. <span data-ttu-id="8c617-140">Ajouter un **View Controller** toostoryboard et ajoutez un **affichage Image**.</span><span class="sxs-lookup"><span data-stu-id="8c617-140">Add a **View Controller** toostoryboard and add an **Image View**.</span></span> <span data-ttu-id="8c617-141">Il s’agit de page hello les utilisateurs verront une fois qu’ils choisissent toolearn plus en cliquant sur les notifiication hello.</span><span class="sxs-lookup"><span data-stu-id="8c617-141">This is hello page users will see once they choose toolearn more by clicking on hello notifiication.</span></span> <span data-ttu-id="8c617-142">Votre storyboard doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="8c617-142">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="8c617-143">Cliquez sur hello **accueil View Controller** dans la table de montage séquentiel et assurez-vous qu’il a **homeViewController** en tant que son **classe personnalisée** et **ID de table de montage séquentiel**sous inspecteur d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="8c617-143">Click on hello **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under hello Identity inspector.</span></span>
7. <span data-ttu-id="8c617-144">De même hello pour le contrôleur de vue d’Image en tant que **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="8c617-144">Do hello same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="8c617-145">Ensuite, créez une nouvelle classe de contrôleur d’affichage intitulée **imageViewController** toohandle hello l’interface utilisateur que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="8c617-145">Then, create a new View Controller class titled **imageViewController** toohandle hello UI you just created.</span></span>
9. <span data-ttu-id="8c617-146">Dans **imageViewController.h**, ajouter hello suivant des déclarations d’interface du contrôleur toohello.</span><span class="sxs-lookup"><span data-stu-id="8c617-146">In **imageViewController.h**, add hello following toohello controller's interface declarations.</span></span> <span data-ttu-id="8c617-147">Assurez-vous que toocontrol, faites glisser hello storyboard image vue toothese propriétés toolink hello deux :</span><span class="sxs-lookup"><span data-stu-id="8c617-147">Make sure toocontrol-drag from hello storyboard image view toothese properties toolink hello two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="8c617-148">Dans **imageViewController.m**, ajoutez hello qui suit à la fin de hello de **viewDidload**:</span><span class="sxs-lookup"><span data-stu-id="8c617-148">In **imageViewController.m**, add hello following at hello end of **viewDidload**:</span></span>
    
        // Display hello UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="8c617-149">Dans **AppDelegate.m**, contrôleur d’image hello importation vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="8c617-149">In **AppDelegate.m**, import hello image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="8c617-150">Ajoutez une section d’interface avec hello suit déclaration :</span><span class="sxs-lookup"><span data-stu-id="8c617-150">Add an interface section with hello following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect tooImage View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="8c617-151">Dans **AppDelegate**, vérifiez que votre application est inscrite aux notifications en mode silencieux dans **application: didFinishLaunchingWithOptions** :</span><span class="sxs-lookup"><span data-stu-id="8c617-151">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="8c617-152">Remplacez Bonjour après la mise en oeuvre pour **application : didRegisterForRemoteNotificationsWithDeviceToken** storyboard de hello tootake interface utilisateur change en compte :</span><span class="sxs-lookup"><span data-stu-id="8c617-152">Subsitute in hello following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** tootake hello storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at hello root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="8c617-153">Ensuite, ajoutez hello trop des méthodes suivantes**AppDelegate.m** tooretrieve hello image à partir de votre point de terminaison et d’envoyer une notification locale lors de la récupération est terminée.</span><span class="sxs-lookup"><span data-stu-id="8c617-153">Then, add hello following methods too**AppDelegate.m** tooretrieve hello image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="8c617-154">Assurez-vous qu’espace réservé de hello toosubstitute `{backend endpoint}` avec votre point de terminaison principal :</span><span class="sxs-lookup"><span data-stu-id="8c617-154">Make sure toosubstitute hello placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
3. <span data-ttu-id="8c617-155">Gérer les notifications de local hello ci-dessus en ouvrant hello image Vue contrôleur **AppDelegate.m** avec hello méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="8c617-155">Handle hello local notification above by opening up hello image view controller in **AppDelegate.m** with hello following methods:</span></span>
   
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

## <a name="run-hello-application"></a><span data-ttu-id="8c617-156">Exécutez hello Application</span><span class="sxs-lookup"><span data-stu-id="8c617-156">Run hello Application</span></span>
1. <span data-ttu-id="8c617-157">Dans XCode, exécutez l’application hello sur un appareil iOS physiques (push notifications ne fonctionnera pas dans le simulateur de hello).</span><span class="sxs-lookup"><span data-stu-id="8c617-157">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="8c617-158">Dans une application iOS de hello l’interface utilisateur, entrez un nom d’utilisateur et un mot de passe de hello même valeur pour l’authentification et cliquez sur **journal dans**.</span><span class="sxs-lookup"><span data-stu-id="8c617-158">In hello iOS app UI, enter a username and password of hello same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="8c617-159">Cliquez sur **Envoyer des notifications Push** : une alerte dans l’application doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="8c617-159">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="8c617-160">Si vous cliquez sur **plus**, vous serez image toohello remises choisis tooinclude à votre serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="8c617-160">If you click on **More**, you will be brought toohello image you chose tooinclude in your app backend.</span></span>
4. <span data-ttu-id="8c617-161">Vous pouvez également cliquer sur **envoi push** et appuyez immédiatement sur bouton Accueil de hello de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="8c617-161">You can also click **Send push** and immediately press hello home button of your device.</span></span> <span data-ttu-id="8c617-162">Dans quelques instants, vous allez recevoir une notification Push.</span><span class="sxs-lookup"><span data-stu-id="8c617-162">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="8c617-163">Si vous cliquez dessus ou cliquez sur plus d’informations, vous serez amené à tooyour application et hello le contenu riche d’image.</span><span class="sxs-lookup"><span data-stu-id="8c617-163">If you tap on it or click More, you will be brought tooyour app and hello rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
