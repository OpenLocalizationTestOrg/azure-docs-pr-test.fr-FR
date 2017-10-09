---
title: aaaAzure Notification Hubs Secure Push.
description: "Découvrez comment toosend sécurisée push notifications tooan iOS application à partir d’Azure. Code samples written in Objective-C and C#."
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
ms.openlocfilehash: 86dd8d7042e5b9e55d2d7ff41cb42f23831fc575
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a><span data-ttu-id="6711c-104">Notifications Push sécurisées avec Azure Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="6711c-104">Azure Notification Hubs Secure Push</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6711c-105">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="6711c-105">Windows Universal</span></span>](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [<span data-ttu-id="6711c-106">iOS</span><span class="sxs-lookup"><span data-stu-id="6711c-106">iOS</span></span>](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [<span data-ttu-id="6711c-107">Android</span><span class="sxs-lookup"><span data-stu-id="6711c-107">Android</span></span>](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="6711c-108">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="6711c-108">Overview</span></span>
<span data-ttu-id="6711c-109">Prise en charge des notifications push dans Microsoft Azure vous permet de tooaccess une infrastructure push facile à utiliser, multiplateforme, à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.</span><span class="sxs-lookup"><span data-stu-id="6711c-109">Push notification support in Microsoft Azure enables you tooaccess an easy-to-use, multiplatform, scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span>

<span data-ttu-id="6711c-110">En raison de contraintes de sécurité ou tooregulatory, une application peut parfois tooinclude quelque chose dans la notification hello ne peut pas être transmis au moyen de l’infrastructure de notification push standard hello.</span><span class="sxs-lookup"><span data-stu-id="6711c-110">Due tooregulatory or security constraints, sometimes an application might want tooinclude something in hello notification that cannot be transmitted through hello standard push notification infrastructure.</span></span> <span data-ttu-id="6711c-111">Ce didacticiel explique comment tooachieve hello la même expérience en envoyant des informations sensibles via une connexion sécurisée, authentifiée entre le périphérique de hello client et serveur principal d’application hello.</span><span class="sxs-lookup"><span data-stu-id="6711c-111">This tutorial describes how tooachieve hello same experience by sending sensitive information through a secure, authenticated connection between hello client device and hello app backend.</span></span>

<span data-ttu-id="6711c-112">À un niveau élevé, les flux hello sont comme suit :</span><span class="sxs-lookup"><span data-stu-id="6711c-112">At a high level, hello flow is as follows:</span></span>

1. <span data-ttu-id="6711c-113">Hello serveur principal d’application :</span><span class="sxs-lookup"><span data-stu-id="6711c-113">hello app back-end:</span></span>
   * <span data-ttu-id="6711c-114">stocke la charge utile sécurisée dans la base de données principale ;</span><span class="sxs-lookup"><span data-stu-id="6711c-114">Stores secure payload in back-end database.</span></span>
   * <span data-ttu-id="6711c-115">Envoie un ID hello de cet appareil toohello de notification (aucune information sécurisée est envoyée).</span><span class="sxs-lookup"><span data-stu-id="6711c-115">Sends hello ID of this notification toohello device (no secure information is sent).</span></span>
2. <span data-ttu-id="6711c-116">application Hello sur périphérique hello, lors de la réception de notification de hello :</span><span class="sxs-lookup"><span data-stu-id="6711c-116">hello app on hello device, when receiving hello notification:</span></span>
   * <span data-ttu-id="6711c-117">Appareil de Hello contacte hello principal demande hello sécurisé charge utile.</span><span class="sxs-lookup"><span data-stu-id="6711c-117">hello device contacts hello back-end requesting hello secure payload.</span></span>
   * <span data-ttu-id="6711c-118">application Hello peut afficher la charge utile de hello en tant que notification sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="6711c-118">hello app can show hello payload as a notification on hello device.</span></span>

<span data-ttu-id="6711c-119">Il est important de toonote que Bonjour précédant le flux (et, dans ce didacticiel), nous supposons que cet appareil hello stocke un jeton d’authentification dans le stockage local, une fois hello utilisateur se connecte.</span><span class="sxs-lookup"><span data-stu-id="6711c-119">It is important toonote that in hello preceding flow (and in this tutorial), we assume that hello device stores an authentication token in local storage, after hello user logs in.</span></span> <span data-ttu-id="6711c-120">Cela garantit une expérience entièrement transparente, comme périphérique de hello peut récupérer de données de la notification hello sécurisé à l’aide de ce jeton.</span><span class="sxs-lookup"><span data-stu-id="6711c-120">This guarantees a completely seamless experience, as hello device can retrieve hello notification’s secure payload using this token.</span></span> <span data-ttu-id="6711c-121">Si votre application n’enregistre pas les jetons d’authentification sur l’appareil de hello, ou si ces jetons peuvent avoir expiré, hello application d’appareil, à la réception de notification de hello doit afficher une notification générique invitant hello utilisateur toolaunch hello application.</span><span class="sxs-lookup"><span data-stu-id="6711c-121">If your application does not store authentication tokens on hello device, or if these tokens can be expired, hello device app, upon receiving hello notification should display a generic notification prompting hello user toolaunch hello app.</span></span> <span data-ttu-id="6711c-122">application Hello puis authentifie l’utilisateur de hello et montre la charge utile de notification hello.</span><span class="sxs-lookup"><span data-stu-id="6711c-122">hello app then authenticates hello user and shows hello notification payload.</span></span>

<span data-ttu-id="6711c-123">Ce didacticiel de Push de sécuriser montre comment toosend une notification push en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="6711c-123">This Secure Push tutorial shows how toosend a push notification securely.</span></span> <span data-ttu-id="6711c-124">didacticiel de Hello s’appuie sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) (didacticiel), donc vous devez effectuer les étapes de hello tout d’abord dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="6711c-124">hello tutorial builds on hello [Notify Users](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) tutorial, so you should complete hello steps in that tutorial first.</span></span>

> [!NOTE]
> <span data-ttu-id="6711c-125">Ce didacticiel repose sur l'hypothèse que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6711c-125">This tutorial assumes that you have created and configured your notification hub as described in [Getting Started with Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).</span></span>
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a><span data-ttu-id="6711c-126">Modifier le projet iOS de hello</span><span class="sxs-lookup"><span data-stu-id="6711c-126">Modify hello iOS project</span></span>
<span data-ttu-id="6711c-127">Maintenant que vous avez modifié votre hello simplement d’application back-end toosend *id* d’une notification, vous avez toochange votre toohandle d’application iOS notification et rappeler votre hello principal tooretrieve secure toobe message affiché.</span><span class="sxs-lookup"><span data-stu-id="6711c-127">Now that you modified your app back-end toosend just hello *id* of a notification, you have toochange your iOS app toohandle that notification and call back your back-end tooretrieve hello secure message toobe displayed.</span></span>

<span data-ttu-id="6711c-128">tooachieve cet objectif, nous avons toowrite hello logique tooretrieve hello contenu sécurisé de hello du serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="6711c-128">tooachieve this goal, we have toowrite hello logic tooretrieve hello secure content from hello app back-end.</span></span>

1. <span data-ttu-id="6711c-129">Dans **AppDelegate.m**, assurez-vous que registres d’application hello pour les notifications en mode silencieux afin qu’il traite les id de notification hello envoyé à partir de hello principal.</span><span class="sxs-lookup"><span data-stu-id="6711c-129">In **AppDelegate.m**, make sure hello app registers for silent notifications so it processes hello notification id sent from hello backend.</span></span> <span data-ttu-id="6711c-130">Ajouter hello **UIRemoteNotificationTypeNewsstandContentAvailability** option dans didFinishLaunchingWithOptions :</span><span class="sxs-lookup"><span data-stu-id="6711c-130">Add hello **UIRemoteNotificationTypeNewsstandContentAvailability** option in didFinishLaunchingWithOptions:</span></span>
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. <span data-ttu-id="6711c-131">Dans votre **AppDelegate.m** ajouter une section d’implémentation haut hello avec hello suit déclaration :</span><span class="sxs-lookup"><span data-stu-id="6711c-131">In your **AppDelegate.m** add an implementation section at hello top with hello following declaration:</span></span>
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. <span data-ttu-id="6711c-132">Puis ajoutez Bonjour de section hello implémentation suivante de code, en remplaçant les espaces réservés de hello `{back-end endpoint}` avec point de terminaison hello pour votre serveur principal obtenu précédemment :</span><span class="sxs-lookup"><span data-stu-id="6711c-132">Then add in hello implementation section hello following code, substituting hello placeholder `{back-end endpoint}` with hello endpoint for your back-end obtained previously:</span></span>

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

    This method calls your app back-end tooretrieve hello notification content using hello credentials stored in hello shared preferences.

1. <span data-ttu-id="6711c-133">Maintenant nous qu’une notification de toohandle hello entrants et utiliser la méthode hello ci-dessus toodisplay de contenu tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="6711c-133">Now we have toohandle hello incoming notification and use hello method above tooretrieve hello content toodisplay.</span></span> <span data-ttu-id="6711c-134">Tout d’abord, nous avons tooenable votre toorun d’application iOS en arrière-plan de hello lors de la réception d’une notification push.</span><span class="sxs-lookup"><span data-stu-id="6711c-134">First, we have tooenable your iOS app toorun in hello background when receiving a push notification.</span></span> <span data-ttu-id="6711c-135">Dans **XCode**, sélectionnez votre projet d’application sur le panneau gauche hello, puis cliquez sur la cible de votre application principale Bonjour **cibles** section à partir du volet central de hello.</span><span class="sxs-lookup"><span data-stu-id="6711c-135">In **XCode**, select your app project on hello left panel, then click your main app target in hello **Targets** section from hello central pane.</span></span>
2. <span data-ttu-id="6711c-136">Puis cliquez sur votre **fonctionnalités** haut hello de votre volet central et vérifiez hello **des Notifications à distance** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="6711c-136">Then click your **Capabilities** tab at hello top of your central pane, and check hello **Remote Notifications** checkbox.</span></span>
   
    ![][IOS1]
3. <span data-ttu-id="6711c-137">Dans **AppDelegate.m** ajouter hello suivant des notifications push de méthode toohandle :</span><span class="sxs-lookup"><span data-stu-id="6711c-137">In **AppDelegate.m** add hello following method toohandle push notifications:</span></span>
   
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
   
    <span data-ttu-id="6711c-138">Notez qu’il s’agit de cas de hello toohandle préférable de propriété d’en-tête d’authentification manquante ou du rejet par hello back-end.</span><span class="sxs-lookup"><span data-stu-id="6711c-138">Note that it is preferable toohandle hello cases of missing authentication header property or rejection by hello back-end.</span></span> <span data-ttu-id="6711c-139">gestion spécifique de Hello de ces cas dépendent principalement de votre expérience d’utilisateur cible.</span><span class="sxs-lookup"><span data-stu-id="6711c-139">hello specific handling of these cases depend mostly on your target user experience.</span></span> <span data-ttu-id="6711c-140">Une option consiste à toodisplay une notification avec un message générique pour hello tooauthenticate tooretrieve hello réel notification à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="6711c-140">One option is toodisplay a notification with a generic prompt for hello user tooauthenticate tooretrieve hello actual notification.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="6711c-141">Exécutez hello Application</span><span class="sxs-lookup"><span data-stu-id="6711c-141">Run hello Application</span></span>
<span data-ttu-id="6711c-142">toorun hello application, procédez comme hello suivant :</span><span class="sxs-lookup"><span data-stu-id="6711c-142">toorun hello application, do hello following:</span></span>

1. <span data-ttu-id="6711c-143">Dans XCode, exécutez l’application hello sur un appareil iOS physiques (push notifications ne fonctionnera pas dans le simulateur de hello).</span><span class="sxs-lookup"><span data-stu-id="6711c-143">In XCode, run hello app on a physical iOS device (push notifications will not work in hello simulator).</span></span>
2. <span data-ttu-id="6711c-144">Dans une application iOS de hello l’interface utilisateur, entrez un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="6711c-144">In hello iOS app UI, enter a username and password.</span></span> <span data-ttu-id="6711c-145">Il peuvent être n’importe quelle chaîne, mais ils doivent être hello la même valeur.</span><span class="sxs-lookup"><span data-stu-id="6711c-145">These can be any string, but they must be hello same value.</span></span>
3. <span data-ttu-id="6711c-146">Dans une application iOS de hello l’interface utilisateur, cliquez sur **connecter**.</span><span class="sxs-lookup"><span data-stu-id="6711c-146">In hello iOS app UI, click **Log in**.</span></span> <span data-ttu-id="6711c-147">Cliquez ensuite sur **Send push**.</span><span class="sxs-lookup"><span data-stu-id="6711c-147">Then click **Send push**.</span></span> <span data-ttu-id="6711c-148">Vous devez voir les notification sécurisée hello s’affiche dans le centre de notification.</span><span class="sxs-lookup"><span data-stu-id="6711c-148">You should see hello secure notification being displayed in your notification center.</span></span>

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
