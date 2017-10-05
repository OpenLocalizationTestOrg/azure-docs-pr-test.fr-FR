---
title: Notifications Push enrichies avec Azure Notification Hubs
description: "Découvrez comment envoyer des notifications Push enrichies à une application iOS depuis Azure. Code samples written in Objective-C and C#."
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
ms.openlocfilehash: 394efdc2dfaff0666bc23d8a448b0a00d414da99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-rich-push"></a><span data-ttu-id="ca978-104">Notifications Push enrichies avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="ca978-104">Azure Notification Hubs Rich Push</span></span>
## <a name="overview"></a><span data-ttu-id="ca978-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ca978-105">Overview</span></span>
<span data-ttu-id="ca978-106">Pour attirer les utilisateurs avec des contenus riches instantanés, une application peut souhaiter envoyer des notifications Push plus sophistiquées que du texte brut.</span><span class="sxs-lookup"><span data-stu-id="ca978-106">In order to engage users with instant rich contents, an application might want to push beyond plain text.</span></span> <span data-ttu-id="ca978-107">Ces notifications promeuvent les interactions entre utilisateurs et présentent du contenu tel que des URL, des sons, des images/coupons et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="ca978-107">These notifications promote user interactions and  present content such as urls, sounds, images/coupons, and more.</span></span> <span data-ttu-id="ca978-108">Ce didacticiel se base sur la rubrique [Envoi de notifications aux utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) et montre comment envoyer des notifications Push qui incorporent des charges utiles (par exemple, une image).</span><span class="sxs-lookup"><span data-stu-id="ca978-108">This tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) topic, and shows how to send push notifications that incorporate payloads (for example, image).</span></span>

<span data-ttu-id="ca978-109">Ce didacticiel est compatible avec iOS 7 et 8.</span><span class="sxs-lookup"><span data-stu-id="ca978-109">This tutorial is compatible with iOS 7 & 8.</span></span>

  ![][IOS1]

<span data-ttu-id="ca978-110">À un niveau élevé :</span><span class="sxs-lookup"><span data-stu-id="ca978-110">At a high level:</span></span>

1. <span data-ttu-id="ca978-111">Le serveur principal :</span><span class="sxs-lookup"><span data-stu-id="ca978-111">The app backend:</span></span>
   * <span data-ttu-id="ca978-112">stocke la charge utile enrichie (dans ce cas, l'image) dans la base de données du serveur principal/stockage local ;</span><span class="sxs-lookup"><span data-stu-id="ca978-112">Stores the rich payload (in this case, image) in the backend database/local storage</span></span>
   * <span data-ttu-id="ca978-113">envoie un ID de cette notification enrichie à l'appareil.</span><span class="sxs-lookup"><span data-stu-id="ca978-113">Sends ID of this rich notification to the device</span></span>
2. <span data-ttu-id="ca978-114">L'application sur l'appareil :</span><span class="sxs-lookup"><span data-stu-id="ca978-114">App on the device:</span></span>
   * <span data-ttu-id="ca978-115">contacte le serveur principal en demandant la charge utile enrichie avec l'ID qu'elle reçoit ;</span><span class="sxs-lookup"><span data-stu-id="ca978-115">Contacts the backend requesting the rich payload with the ID it receives</span></span>
   * <span data-ttu-id="ca978-116">envoie des notifications aux utilisateurs sur l'appareil lorsque la récupération de données est terminée, et affiche la charge utile immédiatement lorsque les utilisateurs cliquent pour en savoir plus.</span><span class="sxs-lookup"><span data-stu-id="ca978-116">Sends users notifications on the device when data retrieval is complete, and shows the payload immediately when users tap to learn more</span></span>

## <a name="webapi-project"></a><span data-ttu-id="ca978-117">Projet WebAPI</span><span class="sxs-lookup"><span data-stu-id="ca978-117">WebAPI Project</span></span>
1. <span data-ttu-id="ca978-118">Dans Visual Studio, ouvrez le projet **AppBackend** que vous avez créé dans le didacticiel [Notification des utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="ca978-118">In Visual Studio, open the **AppBackend** project that you created in the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
2. <span data-ttu-id="ca978-119">Obtenez l’image que vous souhaitez utiliser pour avertir les utilisateurs et placez-la dans un dossier **img** dans votre répertoire de projet.</span><span class="sxs-lookup"><span data-stu-id="ca978-119">Obtain an image you would like to notify users with, and put it in an **img** folder in your project directory.</span></span>
3. <span data-ttu-id="ca978-120">Cliquez sur **Afficher tous les fichiers** dans l’Explorateur de solutions et cliquez sur le dossier à **Inclure dans le projet**.</span><span class="sxs-lookup"><span data-stu-id="ca978-120">Click **Show All Files** in the Solution Explorer, and right-click the folder to **Include In Project**.</span></span>
4. <span data-ttu-id="ca978-121">L’image étant sélectionnée, modifiez son action de génération dans la fenêtre Propriétés de la **Ressource incorporée**.</span><span class="sxs-lookup"><span data-stu-id="ca978-121">With the image selected, change its Build Action in Properties window to **Embedded Resource**.</span></span>
   
    ![][IOS2]
5. <span data-ttu-id="ca978-122">Dans **Notifications.cs**, ajoutez le code suivant à l’aide de l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="ca978-122">In **Notifications.cs**, add the following using statement:</span></span>
   
        using System.Reflection;
6. <span data-ttu-id="ca978-123">Mettez à jour l’ensemble de la classe **Notifications** avec le code suivant.</span><span class="sxs-lookup"><span data-stu-id="ca978-123">Update the whole **Notifications** class with the following code.</span></span> <span data-ttu-id="ca978-124">Veillez à remplacer les espaces réservés par les informations d’identification de votre hub de notification et le nom du fichier image.</span><span class="sxs-lookup"><span data-stu-id="ca978-124">Be sure to replace the placeholders with your notification hub credentials and image file name.</span></span>
   
        public class Notification {
            public int Id { get; set; }
            // Initial notification message to display to users
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
                // Placeholders: replace with the connection string (with full access) for your notification hub and the hub name from the Azure Classics Portal
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
   > <span data-ttu-id="ca978-125">(facultatif) Consultez [Comment faire pour incorporer des ressources et y accéder à l’aide de Visual C#](http://support.microsoft.com/kb/319292) pour plus d’informations sur la façon d’ajouter et d’obtenir des ressources de projet.</span><span class="sxs-lookup"><span data-stu-id="ca978-125">(optional) Refer to [How to embed and access resources by using Visual C#](http://support.microsoft.com/kb/319292) for more information on how to add and obtain project resources.</span></span>
   > 
   > 
7. <span data-ttu-id="ca978-126">Dans **NotificationsController.cs**, redéfinissez **NotificationsController** avec les extraits de code suivants.</span><span class="sxs-lookup"><span data-stu-id="ca978-126">In **NotificationsController.cs**, redefine **NotificationsController**  with the following snippets.</span></span> <span data-ttu-id="ca978-127">Ceci envoie un ID de notification enrichi sans assistance initial à l’appareil et permet l’extraction de l’image sur le client :</span><span class="sxs-lookup"><span data-stu-id="ca978-127">This sends an initial silent rich notification id to device and allows client-side retrieval of image:</span></span>
   
        // Return http response with image binary
        public HttpResponseMessage Get(int id) {
            var stream = Notifications.Instance.ReadImage(id);
   
            var result = new HttpResponseMessage(HttpStatusCode.OK);
            result.Content = new StreamContent(stream);
            // Switch in your image extension for "png"
            result.Content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/{png}");
   
            return result;
        }
   
        // Create rich notification and send initial silent notification (containing id) to client
        public async Task<HttpResponseMessage> Post() {
            // Replace the placeholder with image file name
            var richNotificationInTheBackend = Notifications.Instance.CreateNotification("Check this image out!", "img",  "{logo.png}");
   
            var usernameTag = "username:" + HttpContext.Current.User.Identity.Name;
   
            // Silent notification with content available
            var aboutUser = "{\"aps\": {\"content-available\": 1, \"sound\":\"\"}, \"richId\": \"" + richNotificationInTheBackend.Id.ToString() + "\",  \"richMessage\": \"" + richNotificationInTheBackend.Message + "\", \"richType\": \"" + richNotificationInTheBackend.RichType + "\"}";
   
            // Send notification to apns
            await Notifications.Instance.Hub.SendAppleNativeNotificationAsync(aboutUser, usernameTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
8. <span data-ttu-id="ca978-128">Nous allons maintenant redéployer cette application sur un site web Azure afin de la rendre accessible à tous les appareils.</span><span class="sxs-lookup"><span data-stu-id="ca978-128">Now we will re-deploy this app to an Azure Website in order to make it accessible from all devices.</span></span> <span data-ttu-id="ca978-129">Cliquez avec le bouton droit sur le projet **AppBackend**, puis sélectionnez **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ca978-129">Right-click on the **AppBackend** project and select **Publish**.</span></span>
9. <span data-ttu-id="ca978-130">Sélectionnez Site web Azure comme cible de publication.</span><span class="sxs-lookup"><span data-stu-id="ca978-130">Select Azure Website as your publish target.</span></span> <span data-ttu-id="ca978-131">Connectez-vous avec votre compte Azure, sélectionnez un site web (nouveau ou existant), puis notez la valeur de la propriété **URL de destination** sous l’onglet **Connexion**.</span><span class="sxs-lookup"><span data-stu-id="ca978-131">Log in with your Azure account and select an existing or new Website, and make a note of the **destination URL** property in the **Connection** tab.</span></span> <span data-ttu-id="ca978-132">Plus loin dans ce didacticiel, nous utiliserons cette URL comme *point de terminaison principal* .</span><span class="sxs-lookup"><span data-stu-id="ca978-132">We will refer to this URL as your *backend endpoint* later in this tutorial.</span></span> <span data-ttu-id="ca978-133">Cliquez sur **Publier**.</span><span class="sxs-lookup"><span data-stu-id="ca978-133">Click **Publish**.</span></span>

## <a name="modify-the-ios-project"></a><span data-ttu-id="ca978-134">Modification du projet iOS</span><span class="sxs-lookup"><span data-stu-id="ca978-134">Modify the iOS project</span></span>
<span data-ttu-id="ca978-135">Maintenant que vous avez modifié votre serveur principal d'application pour qu'il envoie uniquement l' *ID* d'une notification, vous allez modifier votre application iOS pour gérer cet ID et récupérer le message enrichi à partir de votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="ca978-135">Now that you have modified your app backend to send just the *id* of a notification, you will change your iOS app to handle that id and retrieve the rich message from your backend.</span></span>

1. <span data-ttu-id="ca978-136">Ouvrez votre projet iOS et activez les notifications à distance en accédant à votre cible d’application principale dans la section **Cibles** .</span><span class="sxs-lookup"><span data-stu-id="ca978-136">Open your iOS project, and enable remote notifications by going to your main app target in the **Targets** section.</span></span>
2. <span data-ttu-id="ca978-137">Cliquez sur **Capacités**, activez **Modes d’arrière-plan** et cochez la case **Notifications à distance**.</span><span class="sxs-lookup"><span data-stu-id="ca978-137">Click on **Capabilities**, turn on **Background Modes**, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS3]
3. <span data-ttu-id="ca978-138">Accédez à **Main.storyboard**et assurez-vous que vous disposez d’un contrôleur d’affichage (dénommé Contrôle d’affichage d’accueil dans ce didacticiel) provenant du didacticiel [Envoi de notifications aux utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="ca978-138">Go to **Main.storyboard**, and make sure you have a View Controller (refered to as Home View Controller in this tutorial) from [Notify User](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial.</span></span>
4. <span data-ttu-id="ca978-139">Ajoutez un **Contrôleur de navigation** à votre table de montage séquentiel et faites-le glisser vers le contrôleur d’affichage d’accueil pour en faire **l’affichage racine** de la navigation.</span><span class="sxs-lookup"><span data-stu-id="ca978-139">Add a **Navigation Controller** to your storyboard, and control-drag to Home View Controller to make it the **root view** of navigation.</span></span> <span data-ttu-id="ca978-140">Vérifiez que **Est contrôleur d’affichage initial** dans l’inspecteur d’attributs est sélectionné pour le contrôleur de navigation uniquement.</span><span class="sxs-lookup"><span data-stu-id="ca978-140">Make sure the **Is Initial View Controller** in Attributes inspector is selected for the Navigation Controller only.</span></span>
5. <span data-ttu-id="ca978-141">Ajoutez un **contrôleur d’affichage** à la table de montage séquentiel et ajoutez un **affichage d’image**.</span><span class="sxs-lookup"><span data-stu-id="ca978-141">Add a **View Controller** to storyboard and add an **Image View**.</span></span> <span data-ttu-id="ca978-142">Il s’agit de la page que les utilisateurs verront une fois qu’ils souhaiteront en savoir plus en cliquant sur la notification.</span><span class="sxs-lookup"><span data-stu-id="ca978-142">This is the page users will see once they choose to learn more by clicking on the notifiication.</span></span> <span data-ttu-id="ca978-143">Votre storyboard doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="ca978-143">Your storyboard should look as follows:</span></span>
   
    ![][IOS4]
6. <span data-ttu-id="ca978-144">Cliquez sur le **contrôleur d’affichage d’accueil** dans la table de montage séquentiel et vérifiez que **homeViewController** est défini en tant que **classe personnalisée** et que **ID de table de montage séquentiel** figure sous l’inspecteur d’identité.</span><span class="sxs-lookup"><span data-stu-id="ca978-144">Click on the **Home View Controller** in storyboard, and make sure it has **homeViewController** as its **Custom Class** and **Storyboard ID** under the Identity inspector.</span></span>
7. <span data-ttu-id="ca978-145">Faites de même pour le contrôleur d’affichage d’image avec **imageViewController**.</span><span class="sxs-lookup"><span data-stu-id="ca978-145">Do the same for Image View Controller as **imageViewController**.</span></span>
8. <span data-ttu-id="ca978-146">Ensuite, créez une classe de contrôleur d’affichage intitulée **imageViewController** pour gérer l’interface utilisateur que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="ca978-146">Then, create a new View Controller class titled **imageViewController** to handle the UI you just created.</span></span>
9. <span data-ttu-id="ca978-147">Dans **imageViewController.h**, ajoutez le code suivant aux déclarations d’interface du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="ca978-147">In **imageViewController.h**, add the following to the controller's interface declarations.</span></span> <span data-ttu-id="ca978-148">Effectuez un glisser-déplacer, tout en appuyant sur la touche Ctrl, depuis l’affichage de l’image dans la table de montage séquentiel vers ces propriétés pour lier les deux :</span><span class="sxs-lookup"><span data-stu-id="ca978-148">Make sure to control-drag from the storyboard image view to these properties to link the two:</span></span>
   
        @property (weak, nonatomic) IBOutlet UIImageView *myImage;
        @property (strong) UIImage* imagePayload;
10. <span data-ttu-id="ca978-149">Dans **imageViewController.m**, ajoutez ce qui suit à la fin de **viewDidload** :</span><span class="sxs-lookup"><span data-stu-id="ca978-149">In **imageViewController.m**, add the following at the end of **viewDidload**:</span></span>
    
        // Display the UI Image in UI Image View
        [self.myImage setImage:self.imagePayload];
11. <span data-ttu-id="ca978-150">Dans **AppDelegate.m**, importez le contrôleur d’image que vous avez créé :</span><span class="sxs-lookup"><span data-stu-id="ca978-150">In **AppDelegate.m**, import the image controller you created:</span></span>
    
        #import "imageViewController.h"
12. <span data-ttu-id="ca978-151">Ajoutez une section d’interface avec la déclaration suivante :</span><span class="sxs-lookup"><span data-stu-id="ca978-151">Add an interface section with the following declaration:</span></span>
    
        @interface AppDelegate ()
    
        @property UIImage* imagePayload;
        @property NSDictionary* userInfo;
        @property BOOL iOS8;
    
        // Obtain content from backend with notification id
        - (void)retrieveRichImageWithId:(int)richId completion: (void(^)(NSError*)) completion;
    
        // Redirect to Image View Controller after notification interaction
        - (void)redirectToImageViewWithImage: (UIImage *)img;
    
        @end
13. <span data-ttu-id="ca978-152">Dans **AppDelegate**, vérifiez que votre application est inscrite aux notifications en mode silencieux dans **application: didFinishLaunchingWithOptions** :</span><span class="sxs-lookup"><span data-stu-id="ca978-152">In **AppDelegate**, make sure your app registers for silent notifications in **application: didFinishLaunchingWithOptions**:</span></span>
    
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

1. <span data-ttu-id="ca978-153">Insérez l’implémentation suivante pour **application:didRegisterForRemoteNotificationsWithDeviceToken** afin de prendre en compte les modifications d’interface utilisateur du tableau de montage séquentiel :</span><span class="sxs-lookup"><span data-stu-id="ca978-153">Subsitute in the following implementation for **application:didRegisterForRemoteNotificationsWithDeviceToken** to take the storyboard UI changes into account:</span></span>
   
       // Access navigation controller which is at the root of window
       UINavigationController *nc = (UINavigationController *)self.window.rootViewController;
       // Get home view controller from stack on navigation controller
       homeViewController *hvc = (homeViewController *)[nc.viewControllers objectAtIndex:0];
       hvc.deviceToken = deviceToken;
2. <span data-ttu-id="ca978-154">Puis ajoutez les méthodes ci-après à **AppDelegate.m** pour récupérer l’image à partir de votre point de terminaison et envoyer une notification locale à la fin de la récupération.</span><span class="sxs-lookup"><span data-stu-id="ca978-154">Then, add the following methods to **AppDelegate.m** to retrieve the image from your endpoint and send a local notification when retrieval is complete.</span></span> <span data-ttu-id="ca978-155">Prenez soin de remplacer l’espace réservé `{backend endpoint}` par le point de terminaison de votre serveur principal :</span><span class="sxs-lookup"><span data-stu-id="ca978-155">Make sure to substitute the placeholder `{backend endpoint}` with your backend endpoint:</span></span>
   
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
                   // From NSData to UIImage
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
   
                       // "5" is arbitrary here to give you enough time to quit out of the app and receive push notifications
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
           // Add "else if" here to handle more types of rich content such as url, sound files, etc.
       }
3. <span data-ttu-id="ca978-156">Gérez la notification locale ci-dessus en ouvrant le contrôleur d’affichage d’image dans **AppDelegate.m** avec les méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ca978-156">Handle the local notification above by opening up the image view controller in **AppDelegate.m** with the following methods:</span></span>
   
       // Helper: redirect users to image view controller
       - (void)redirectToImageViewWithImage: (UIImage *)img {
           UINavigationController *navigationController = (UINavigationController*) self.window.rootViewController;
           UIStoryboard *mainStoryboard = [UIStoryboard storyboardWithName:@"Main"
                                                                    bundle: nil];
           imageViewController *imgViewController = [mainStoryboard instantiateViewControllerWithIdentifier: @"imageViewController"];
           // Pass data/image to image view controller
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
           // Add "else if" here to handle more buttons
       }
   
       // Handle notification setting actions in iOS8
       - (void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forLocalNotification:(UILocalNotification *)notification completionHandler:(void (^)())completionHandler {
           // Handle richPush related buttons
           if ([identifier isEqualToString:@"richPushMore"]) {
               [self redirectToImageViewWithImage:self.imagePayload];
           }
           completionHandler();
       }

## <a name="run-the-application"></a><span data-ttu-id="ca978-157">Exécution de l’application</span><span class="sxs-lookup"><span data-stu-id="ca978-157">Run the Application</span></span>
1. <span data-ttu-id="ca978-158">Dans XCode, exécutez l’application sur un appareil iOS physique (les notifications Push ne fonctionnent pas dans le simulateur).</span><span class="sxs-lookup"><span data-stu-id="ca978-158">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="ca978-159">Dans l’interface utilisateur de l’application iOS, entrez un nom d’utilisateur et un mot de passe de la même valeur pour l’authentification et cliquez sur **Se connecter**.</span><span class="sxs-lookup"><span data-stu-id="ca978-159">In the iOS app UI, enter a username and password of the same value for authentication and click **Log In**.</span></span>
3. <span data-ttu-id="ca978-160">Cliquez sur **Envoyer des notifications Push** : une alerte dans l’application doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="ca978-160">Click **Send push** and you should see an in-app alert.</span></span> <span data-ttu-id="ca978-161">Si vous cliquez sur **Plus**, l’image que vous avez choisi d’inclure dans votre serveur principal d’application s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ca978-161">If you click on **More**, you will be brought to the image you chose to include in your app backend.</span></span>
4. <span data-ttu-id="ca978-162">Vous pouvez également cliquer sur **Envoyer des notifications Push** et appuyer immédiatement sur le bouton Accueil de votre appareil.</span><span class="sxs-lookup"><span data-stu-id="ca978-162">You can also click **Send push** and immediately press the home button of your device.</span></span> <span data-ttu-id="ca978-163">Dans quelques instants, vous allez recevoir une notification Push.</span><span class="sxs-lookup"><span data-stu-id="ca978-163">In a few moments, you will receive a push notification.</span></span> <span data-ttu-id="ca978-164">Si vous cliquez dessus ou si vous cliquez sur Plus, votre application et le contenu d’images enrichi apparaissent.</span><span class="sxs-lookup"><span data-stu-id="ca978-164">If you tap on it or click More, you will be brought to your app and the rich image content.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-1.png
[IOS2]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-2.png
[IOS3]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-3.png
[IOS4]: ./media/notification-hubs-aspnet-backend-ios-rich-push/rich-push-ios-4.png
