---
title: "Notifications Push sécurisées avec Azure Notification Hubs"
description: "Découvrez comment envoyer des notifications Push sécurisées à une application iOS depuis Azure. Code samples written in Objective-C and C#."
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 17d42b0a-2c80-4e35-a1ed-ed510d19f4b4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: e5f09fb3716303bb21fe7442aa6fa8832174838e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="674db-104">Notifications Push sécurisées avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="674db-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="674db-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="674db-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="674db-106">iOS</span><span class="sxs-lookup"><span data-stu-id="674db-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="674db-107">Android</span><span class="sxs-lookup"><span data-stu-id="674db-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="674db-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="674db-108">Overview</span></span>
<span data-ttu-id="674db-109">La prise en charge des notifications Push dans Microsoft Azure vous permet d’accéder à une infrastructure Push conviviale, multiplateforme avec montée en charge qui simplifie fortement l’implémentation des notifications Push pour les applications grand public et d’entreprise destinées aux plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="674db-109">Push notification support in Microsoft Azure enables you to access an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="674db-110">En raison de contraintes liées à la réglementation ou à la sécurité, une application peut avoir besoin d'inclure dans la notification des informations qui ne peuvent pas être transmises via l'infrastructure de notification Push standard.</span><span class="sxs-lookup"><span data-stu-id="674db-110">Due to regulatory or security constraints, sometimes an application might want to include something in the notification that cannot be transmitted through the standard push notification infrastructure.</span></span> <span data-ttu-id="674db-111">Ce didacticiel montre comment procéder en envoyant des informations sensibles par l'intermédiaire d'une connexion authentifiée sécurisée entre l'appareil client et le serveur principal de l'application.</span><span class="sxs-lookup"><span data-stu-id="674db-111">This tutorial describes how to achieve the same experience by sending sensitive information through a secure, authenticated connection between the client device and the app backend.</span></span>

<span data-ttu-id="674db-112">Globalement, le processus est le suivant :</span><span class="sxs-lookup"><span data-stu-id="674db-112">At a high level, the flow is as follows:</span></span>

1. <span data-ttu-id="674db-113">Le serveur principal de l'application :</span><span class="sxs-lookup"><span data-stu-id="674db-113">The app back-end:</span></span>
   * <span data-ttu-id="674db-114">stocke la charge utile sécurisée dans la base de données principale ;</span><span class="sxs-lookup"><span data-stu-id="674db-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="674db-115">envoie l'ID de cette notification à l'appareil (aucune information sécurisée n'est envoyée).</span><span class="sxs-lookup"><span data-stu-id="674db-115">Sends the ID of this notification to the device (no secure information is sent).</span></span>
2. <span data-ttu-id="674db-116">L'application qui se trouve sur l'appareil, lorsqu'elle reçoit la notification :</span><span class="sxs-lookup"><span data-stu-id="674db-116">The app on the device, when receiving the notification:</span></span>
   * <span data-ttu-id="674db-117">L'appareil contacte le serveur principal en demandant la charge utile sécurisée.</span><span class="sxs-lookup"><span data-stu-id="674db-117">The device contacts the back-end requesting the secure payload.</span></span>
   * <span data-ttu-id="674db-118">L'application peut afficher la charge utile sous la forme d'une notification sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="674db-118">The app can show the payload as a notification on the device.</span></span>

<span data-ttu-id="674db-119">Veuillez noter que dans le flux précédent (et dans ce didacticiel), nous partons du principe que l’appareil stocke un jeton d’authentification dans un stockage local, une fois l’utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="674db-119">It is important to note that in the preceding flow (and in this tutorial), we assume that the device stores an authentication token in local storage, after the user logs in.</span></span> <span data-ttu-id="674db-120">Cela simplifie nettement l’expérience, car l’appareil peut récupérer la charge utile sécurisée en utilisant ce jeton.</span><span class="sxs-lookup"><span data-stu-id="674db-120">This guarantees a completely seamless experience, as the device can retrieve the notification’s secure payload using this token.</span></span> <span data-ttu-id="674db-121">Si votre application ne stocke pas les jetons d'authentification sur l'appareil, ou si ces jetons sont susceptibles d'expirer, lorsque l'application sur l'appareil reçoit la notification, elle doit afficher une notification générique demandant à l'utilisateur de lancer l'application.</span><span class="sxs-lookup"><span data-stu-id="674db-121">If your application does not store authentication tokens on the device, or if these tokens can be expired, the device app, upon receiving the notification should display a generic notification prompting the user to launch the app.</span></span> <span data-ttu-id="674db-122">L'application authentifie alors l'utilisateur et affiche la charge utile de la notification.</span><span class="sxs-lookup"><span data-stu-id="674db-122">The app then authenticates the user and shows the notification payload.</span></span>

<span data-ttu-id="674db-123">Ce didacticiel sur les notifications Push sécurisées montre comment envoyer une notification Push en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="674db-123">This Secure Push tutorial shows how to send a push notification securely.</span></span> <span data-ttu-id="674db-124">Il s’appuie sur le didacticiel [Envoi de notifications à des utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md). Vous devez donc suivre ce dernier au préalable.</span><span class="sxs-lookup"><span data-stu-id="674db-124">The tutorial builds on the [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete the steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="674db-125">Ce didacticiel repose sur l'hypothèse que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="674db-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-the-ios-project"></a><span data-ttu-id="674db-126">Modification du projet iOS</span><span class="sxs-lookup"><span data-stu-id="674db-126">Modify the iOS project</span></span>
<span data-ttu-id="674db-127">Maintenant que vous avez modifié le serveur principal de votre application pour qu'il n'envoie que l' *id* des notifications, vous devez modifier votre application iOS pour gérer cette notification et rappeler votre serveur pour récupérer le message sécurisé à afficher.</span><span class="sxs-lookup"><span data-stu-id="674db-127">Now that you modified your app back-end to send just the *id* of a notification, you have to change your iOS app to handle that notification and call back your back-end to retrieve the secure message to be displayed.</span></span>

<span data-ttu-id="674db-128">Pour cela, nous devons écrire la logique permettant de récupérer le contenu sécurisé auprès du serveur principal de l'application.</span><span class="sxs-lookup"><span data-stu-id="674db-128">To achieve this goal, we have to write the logic to retrieve the secure content from the app back-end.</span></span>

1. <span data-ttu-id="674db-129">Dans **AppDelegate.m**, assurez-vous que l’application s’inscrit aux notifications sans assistance afin qu’elle traite l’ID de notification envoyé à partir du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="674db-129">In **AppDelegate.m**, make sure the app registers for silent notifications so it processes the notification id sent from the backend.</span></span> <span data-ttu-id="674db-130">Ajoutez l’option **UIRemoteNotificationTypeNewsstandContentAvailability** dans didFinishLaunchingWithOptions :</span><span class="sxs-lookup"><span data-stu-id="674db-130">Add the **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="674db-131">Dans **AppDelegate.m** , ajoutez une section d'implémentation au début, avec la déclaration qui suit :</span><span class="sxs-lookup"><span data-stu-id="674db-131">In your **AppDelegate.m** add an implementation section at the top with the following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="674db-132">Ensuite, ajoutez le code qui suit dans la section d’implémentation, en remplaçant l’espace réservé `{back-end endpoint}` par le point de terminaison de votre serveur principal que vous avez obtenu précédemment :</span><span class="sxs-lookup"><span data-stu-id="674db-132">Then add in the implementation section the following code, substituting the placeholder `{back-end endpoint}` with the endpoint for your back-end obtained previously:</span></span>

```
        NSString *const GetNotificationEndpoint = @"{back-end endpoint}/api/notifications";

        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        {
            // check if authenticated
            ANHViewController* rvc = (ANHViewController*) self.window.rootViewController;
            NSString* authenticationHeader = rvc.registerClient.authenticationHeader;
            if (!authenticationHeader) return;


            NSURLSession* session = [NSURLSession
                                     sessionWithConfiguration:[NSURLSessionConfiguration defaultSessionConfiguration]
                                     delegate:nil
                                     delegateQueue:nil];


            NSURL* requestURL = [NSURL URLWithString:[NSString stringWithFormat:@"%@/%d", GetNotificationEndpoint, payloadId]];
            NSMutableURLRequest* request = [NSMutableURLRequest requestWithURL:requestURL];
            [request setHTTPMethod:@"GET"];
            NSString* authorizationHeaderValue = [NSString stringWithFormat:@"Basic %@", authenticationHeader];
            [request setValue:authorizationHeaderValue forHTTPHeaderField:@"Authorization"];

            NSURLSessionDataTask* dataTask = [session dataTaskWithRequest:request completionHandler:^(NSData *data, NSURLResponse *response, NSError *error) {
                NSHTTPURLResponse* httpResponse = (NSHTTPURLResponse*) response;
                if (!error && httpResponse.statusCode == 200)
                {
                    NSLog(@"Received secure payload: %@", [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding]);

                    NSMutableDictionary *json = [NSJSONSerialization JSONObjectWithData:data options: NSJSONReadingMutableContainers error: &error];

                    completion([json objectForKey:@"Payload"], nil);
                }
                else
                {
                    NSLog(@"Error status: %ld, request: %@", (long)httpResponse.statusCode, error);
                    if (error)
                        completion(nil, error);
                    else {
                        completion(nil, [NSError errorWithDomain:@"APICall" code:httpResponse.statusCode userInfo:nil]);
                    }
                }
            }];
            [dataTask resume];
        }
```

    This method calls your app back-end to retrieve the notification content using the credentials stored in the shared preferences.

1. <span data-ttu-id="674db-133">Maintenant, nous devons gérer la notification entrante et utiliser la méthode ci-dessus pour récupérer le contenu à afficher.</span><span class="sxs-lookup"><span data-stu-id="674db-133">Now we have to handle the incoming notification and use the method above to retrieve the content to display.</span></span> <span data-ttu-id="674db-134">Nous devons tout d'abord permettre à l'application iOS de s'exécuter en arrière-plan lorsqu'elle reçoit une notification Push.</span><span class="sxs-lookup"><span data-stu-id="674db-134">First, we have to enable your iOS app to run in the background when receiving a push notification.</span></span> <span data-ttu-id="674db-135">Dans **XCode**, sélectionnez votre projet d’application dans le volet gauche, puis cliquez sur votre cible d’application principale dans la section **Cibles** du volet central.</span><span class="sxs-lookup"><span data-stu-id="674db-135">In **XCode**, select your app project on the left panel, then click your main app target in the **Targets** section from the central pane.</span></span>
2. <span data-ttu-id="674db-136">Cliquez ensuite sur l’onglet **Capacités** en haut du volet central et cochez la case **Notifications distantes**.</span><span class="sxs-lookup"><span data-stu-id="674db-136">Then click your **Capabilities** tab at the top of your central pane, and check the **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="674db-137">Dans **AppDelegate.m** , ajoutez la méthode suivante pour gérer les notifications Push :</span><span class="sxs-lookup"><span data-stu-id="674db-137">In **AppDelegate.m** add the following method to handle push notifications:</span></span>
   
        -(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler
        {
            NSLog(@"%@", userInfo);
   
            [self retrieveSecurePayloadWithId:[[userInfo objectForKey:@"secureId"] intValue] completion:^(NSString * payload, NSError *error) {
                if (!error) {
                    // show local notification
                    UILocalNotification* localNotification = [[UILocalNotification alloc] init];
                    localNotification.fireDate = [NSDate dateWithTimeIntervalSinceNow:0];
                    localNotification.alertBody = payload;
                    localNotification.timeZone = [NSTimeZone defaultTimeZone];
                    [[UIApplication sharedApplication] scheduleLocalNotification:localNotification];
   
                    completionHandler(UIBackgroundFetchResultNewData);
                } else {
                    completionHandler(UIBackgroundFetchResultFailed);
                }
            }];
   
        }
   
    <span data-ttu-id="674db-138">Notez qu'il est préférable de gérer les cas de refus ou les cas concernant les propriétés d'en-tête d'authentification manquantes au niveau du serveur.</span><span class="sxs-lookup"><span data-stu-id="674db-138">Note that it is preferable to handle the cases of missing authentication header property or rejection by the back-end.</span></span> <span data-ttu-id="674db-139">La gestion spécifique de ces cas dépend surtout de l'expérience utilisateur souhaitée.</span><span class="sxs-lookup"><span data-stu-id="674db-139">The specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="674db-140">Une possibilité est d'afficher une notification avec une invite générique demandant à l'utilisateur de s'authentifier afin de récupérer la notification elle-même.</span><span class="sxs-lookup"><span data-stu-id="674db-140">One option is to display a notification with a generic prompt for the user to authenticate to retrieve the actual notification.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="674db-141">Exécution de l'application</span><span class="sxs-lookup"><span data-stu-id="674db-141">Run the Application</span></span>
<span data-ttu-id="674db-142">Pour exécuter l'application, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="674db-142">To run the application, do the following:</span></span>

1. <span data-ttu-id="674db-143">Dans XCode, exécutez l’application sur un appareil iOS physique (les notifications Push ne fonctionnent pas dans le simulateur).</span><span class="sxs-lookup"><span data-stu-id="674db-143">In XCode, run the app on a physical iOS device (push notifications will not work in the simulator).</span></span>
2. <span data-ttu-id="674db-144">Dans l'interface utilisateur de l'application iOS, entrez un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="674db-144">In the iOS app UI, enter a username and password.</span></span> <span data-ttu-id="674db-145">La valeur peut être une chaîne quelconque, mais elle doit être identique pour les deux.</span><span class="sxs-lookup"><span data-stu-id="674db-145">These can be any string, but they must be the same value.</span></span>
3. <span data-ttu-id="674db-146">Dans l'interface utilisateur de l'application iOS, cliquez sur **Log in**.</span><span class="sxs-lookup"><span data-stu-id="674db-146">In the iOS app UI, click **Log in**.</span></span> <span data-ttu-id="674db-147">Cliquez ensuite sur **Send push**.</span><span class="sxs-lookup"><span data-stu-id="674db-147">Then click **Send push**.</span></span> <span data-ttu-id="674db-148">Vous devriez voir la notification sécurisée affichée dans le centre de notifications.</span><span class="sxs-lookup"><span data-stu-id="674db-148">You should see the secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
