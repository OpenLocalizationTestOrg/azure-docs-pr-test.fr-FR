---
title: "Didacticiel sur l’utilisation de Notification Hubs pour envoyer les dernières nouvelles localisées pour iOS"
description: "Découvrez comment utiliser Azure Service Bus Notification Hubs pour envoyer des notifications de dernières nouvelles localisées (iOS)."
services: notification-hubs
documentationcenter: ios
author: ysxu
manager: erikre
editor: 
ms.assetid: 484914b5-e081-4a05-a84a-798bbd89d428
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: fd2b7d9dfd4f432bbcbaa3ed76f8bec0b9677e17
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news-to-ios-devices"></a><span data-ttu-id="dbc4b-103">Utilisation de Notification Hubs pour envoyer les dernières nouvelles localisées vers des appareils iOS</span><span class="sxs-lookup"><span data-stu-id="dbc4b-103">Use Notification Hubs to send localized breaking news to iOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="dbc4b-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="dbc4b-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="dbc4b-105">iOS</span><span class="sxs-lookup"><span data-stu-id="dbc4b-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="dbc4b-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="dbc4b-106">Overview</span></span>
<span data-ttu-id="dbc4b-107">Cette rubrique montre comment utiliser la fonctionnalité de [modèles](notification-hubs-templates-cross-platform-push-messages.md) d’Azure Notification Hubs pour diffuser des notifications relatives aux dernières nouvelles qui ont été localisées par langue et par appareil.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-107">This topic shows you how to use the [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="dbc4b-108">Dans ce didacticiel, vous commencez avec l’application iOS que vous avez créée dans le cadre du didacticiel [Utilisation de Notifications Hubs pour envoyer les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="dbc4b-108">In this tutorial you start with the iOS app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="dbc4b-109">Lorsque vous aurez terminé, vous pourrez vous inscrire aux catégories qui vous intéressent, spécifier une langue dans laquelle recevoir les notifications et recevoir uniquement des notifications Push pour les catégories sélectionnées dans cette langue.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="dbc4b-110">Ce scénario comporte deux parties :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="dbc4b-111">L'application iOS permet aux appareils clients d'indiquer une langue et de s'abonner à différentes catégories de dernières nouvelles.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-111">iOS app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="dbc4b-112">Le serveur principal diffuse les notifications à l’aide des fonctionnalités de **balise** et de **modèle** d’Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbc4b-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dbc4b-113">Prerequisites</span></span>
<span data-ttu-id="dbc4b-114">Vous devez avoir suivi le didacticiel [Utilisation de Notifications Hubs pour envoyer les dernières nouvelles] et avoir le code à disposition, car le présent didacticiel est basé sur ce code.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="dbc4b-115">Visual Studio 2012 ou une version ultérieure est facultative.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="dbc4b-116">Concepts de modèle</span><span class="sxs-lookup"><span data-stu-id="dbc4b-116">Template concepts</span></span>
<span data-ttu-id="dbc4b-117">Dans le didacticiel [Utilisation de Notifications Hubs pour envoyer les dernières nouvelles] , vous avez créé une application qui se sert de **balises** pour s'abonner aux notifications relatives à différentes catégories de nouvelles.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="dbc4b-118">Cependant, de nombreuses applications sont destinées à plusieurs marchés et doivent donc être localisées.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="dbc4b-119">Cela signifie que le contenu des notifications proprement dites doit lui aussi être localisé et envoyé au bon ensemble d’appareils.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="dbc4b-120">Dans cette rubrique, nous allons vous montrer comment utiliser la fonctionnalité de **modèle** de Notification Hubs pour facilement envoyer des notifications de dernières nouvelles localisées.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="dbc4b-121">Remarque : pour envoyer des notifications localisées, vous pouvez notamment créer plusieurs versions de chaque balise.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="dbc4b-122">Par exemple, pour prendre en charge l'anglais, le français et le mandarin, nous aurions besoin de trois balises différentes pour les nouvelles internationales : « world_en », « world_fr » et « world_ch ».</span><span class="sxs-lookup"><span data-stu-id="dbc4b-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="dbc4b-123">Il faudrait ensuite que nous envoyions une version localisée des nouvelles internationales à chacune de ces balises.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="dbc4b-124">Dans cette rubrique, nous utilisons des modèles afin d'éviter la prolifération de balises et d'éliminer la nécessité d'envoyer plusieurs messages.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="dbc4b-125">À un haut niveau, les modèles permettent de spécifier comment un appareil particulier reçoit une notification.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="dbc4b-126">Le modèle spécifie le format de charge utile exact en se référant aux propriétés qui font partie du message envoyé par le serveur principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="dbc4b-127">Aux fins de notre exemple, nous allons envoyer un message de paramètres régionaux contenant toutes les langues prises en charge :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="dbc4b-128">Ensuite, nous allons nous assurer que les appareils s'inscrivent avec un modèle qui se réfère à la bonne propriété.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="dbc4b-129">Par exemple, une application iOS qui souhaite s’abonner aux nouvelles françaises inscrira ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-129">For instance,  an iOS app that wants to register for French news will register the following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="dbc4b-130">Les modèles sont une fonctionnalité très puissante sur laquelle vous pouvez obtenir plus d’informations en lisant notre article [Modèles](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="dbc4b-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="the-app-user-interface"></a><span data-ttu-id="dbc4b-131">Interface utilisateur de l’application</span><span class="sxs-lookup"><span data-stu-id="dbc4b-131">The app user interface</span></span>
<span data-ttu-id="dbc4b-132">Nous allons maintenant modifier l’application de dernières nouvelles que vous avez créée à la rubrique [Utilisation de Notifications Hubs pour envoyer les dernières nouvelles] pour envoyer les dernières nouvelles localisées à l’aide de modèles.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="dbc4b-133">Dans votre MainStoryboard_iPhone.storyboard, ajoutez un contrôle segmenté avec les trois langues que nous prendrons en charge : anglais, français et mandarin.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with the three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="dbc4b-134">Puis, assurez-vous d’ajouter un IBOutlet dans votre ViewController.h comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-134">Then make sure to add an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-the-ios-app"></a><span data-ttu-id="dbc4b-135">Création de l’application iOS</span><span class="sxs-lookup"><span data-stu-id="dbc4b-135">Building the iOS app</span></span>
1. <span data-ttu-id="dbc4b-136">Dans Notification.h, ajoutez la méthode *retrieveLocale* , puis modifiez le magasin et les méthodes d'abonnement comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-136">In your Notification.h add the *retrieveLocale* method, and modify the store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="dbc4b-137">Dans Notification.m, modifiez la méthode *storeCategoriesAndSubscribe* en ajoutant les paramètres régionaux et en les stockant dans les valeurs par défaut de l'utilisateur :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-137">In your Notification.m, modify the *storeCategoriesAndSubscribe* method, by adding the locale parameter and storing it in the user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="dbc4b-138">Puis, modifiez la méthode *subscribe* afin d'inclure les paramètres régionaux :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-138">Then modify the *subscribe* method to include the locale:</span></span>
   
        - (void) subscribeWithLocale: (int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion{
            SBNotificationHub* hub = [[SBNotificationHub alloc] initWithConnectionString:@"<connection string>" notificationHubPath:@"<hub name>"];
   
            NSString* localeString;
            switch (locale) {
                case 0:
                    localeString = @"English";
                    break;
                case 1:
                    localeString = @"French";
                    break;
                case 2:
                    localeString = @"Mandarin";
                    break;
            }
   
            NSString* template = [NSString stringWithFormat:@"{\"aps\":{\"alert\":\"$(News_%@)\"},\"inAppMessage\":\"$(News_%@)\"}", localeString, localeString];
   
            [hub registerTemplateWithDeviceToken:self.deviceToken name:@"localizednewsTemplate" jsonBodyTemplate:template expiryTemplate:@"0" tags:categories completion:completion];
        }
   
    <span data-ttu-id="dbc4b-139">Remarquez que nous utilisons à présent la méthode *registerTemplateWithDeviceToken* au lieu de *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-139">Note how we are now using the method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="dbc4b-140">Lorsque nous nous abonnons à un modèle, nous devons fournir le modèle json ainsi qu'un nom pour le modèle (car notre application peut vouloir s'abonner à différents modèles).</span><span class="sxs-lookup"><span data-stu-id="dbc4b-140">When we register for a template we have to provide the json template and also a name for the template (as our app might want to register different templates).</span></span> <span data-ttu-id="dbc4b-141">Assurez-vous d'abonner vos catégories sous la forme de balises, car nous voulons nous assurer de recevoir les notifications pour ces nouvelles.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-141">Make sure to register your categories as tags, as we want to make sure to receive the notifciations for those news.</span></span>
   
    <span data-ttu-id="dbc4b-142">Ajoutez une méthode pour extraire les paramètres régionaux des paramètres utilisateur par défaut :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-142">Add a method to retrieve the locale from the user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="dbc4b-143">Maintenant que nous avons modifié notre classe Notifications, nous devons nous assurer que notre paramètre ViewController utilise le nouveau paramètre UISegmentControl.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-143">Now that we modified our Notifications class, we have to make sure that our ViewController makes use of the new UISegmentControl.</span></span> <span data-ttu-id="dbc4b-144">Ajoutez la ligne suivante dans la méthode *viewDidLoad* pour garantir l'affichage des paramètres régionaux actuellement sélectionnés :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-144">Add the following line in the *viewDidLoad* method to make sure to show the locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="dbc4b-145">Puis, dans votre méthode *subscribe*, modifiez votre appel à *storeCategoriesAndSubscribe* comme suit :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-145">Then, in your *subscribe* method, change your call to the *storeCategoriesAndSubscribe* to the following:</span></span>
   
        [notifications storeCategoriesAndSubscribeWithLocale: self.Locale.selectedSegmentIndex categories:[NSSet setWithArray:categories] completion: ^(NSError* error) {
            if (!error) {
                UIAlertView *alert = [[UIAlertView alloc] initWithTitle:@"Notification" message:
                                      @"Subscribed!" delegate:nil cancelButtonTitle:
                                      @"OK" otherButtonTitles:nil, nil];
                [alert show];
            } else {
                NSLog(@"Error subscribing: %@", error);
            }
        }];
3. <span data-ttu-id="dbc4b-146">Enfin, vous devez mettre à jour la méthode *didRegisterForRemoteNotificationsWithDeviceToken* dans votre AppDelegate.m afin que vous puissiez correctement actualiser votre abonnement lorsque votre application démarre.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-146">Finally, you have to update the *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="dbc4b-147">Modifiez votre appel sur la méthode *subscribe* de notifications comme suit :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-147">Change your call to the *subscribe* method of notifications with the following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="dbc4b-148">(facultatif) Envoyer des notifications de modèle localisé à partir de l’application console .NET.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-the-device"></a><span data-ttu-id="dbc4b-149">(facultatif) Envoyer des notifications de modèle localisé à partir de l’appareil</span><span class="sxs-lookup"><span data-stu-id="dbc4b-149">(optional) Send localized template notifications from the device</span></span>
<span data-ttu-id="dbc4b-150">Si vous n’avez pas accès à Visual Studio ou si vous souhaitez simplement essayer d’envoyer les notification de modèle localisé directement depuis l’application sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-150">If you don't have access to Visual Studio, or want to just test sending the localized template notifications directly from the app on the device.</span></span>  <span data-ttu-id="dbc4b-151">Vous pouvez simplement ajouter les paramètres de modèle localisé à la méthode `SendNotificationRESTAPI` que vous avez défini précédemment, dans le didacticiel.</span><span class="sxs-lookup"><span data-stu-id="dbc4b-151">You can simple add the localized template parameters to the `SendNotificationRESTAPI` method you defined in the previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct the messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated the token to be used in the authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create the request to add the template notification message to the hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add the category as a tag
            [request setValue:categoryTag forHTTPHeaderField:@"ServiceBusNotification-Tags"];

            // Template notification
            json = [NSString stringWithFormat:@"{\"messageParam\":\"Breaking %@ News : %@\","
                    \"News_English\":\"Breaking %@ News in English : %@\","
                    \"News_French\":\"Breaking %@ News in French : %@\","
                    \"News_Mandarin\":\"Breaking %@ News in Mandarin : %@\","
                    categoryTag, self.notificationMessage.text,
                    categoryTag, self.notificationMessage.text,  // insert English localized news here
                    categoryTag, self.notificationMessage.text,  // insert French localized news here
                    categoryTag, self.notificationMessage.text]; // insert Mandarin localized news here

            // Signify template notification format
            [request setValue:@"template" forHTTPHeaderField:@"ServiceBusNotification-Format"];

            // JSON Content-Type
            [request setValue:@"application/json;charset=utf-8" forHTTPHeaderField:@"Content-Type"];

            //Authenticate the notification message POST request with the SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add the notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send the REST request
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




## <a name="next-steps"></a><span data-ttu-id="dbc4b-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="dbc4b-152">Next Steps</span></span>
<span data-ttu-id="dbc4b-153">Pour plus d’informations sur l’utilisation des modèles, consultez :</span><span class="sxs-lookup"><span data-stu-id="dbc4b-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="dbc4b-154">[Notification des utilisateurs avec Notification Hubs : ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="dbc4b-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="dbc4b-155">[Notification des utilisateurs avec Notification Hubs : Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="dbc4b-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
<span data-ttu-id="dbc4b-156">[Utilisation de Notifications Hubs pour envoyer les dernières nouvelles]: /manage/services/notification-hubs/breaking-news-ios</span><span class="sxs-lookup"><span data-stu-id="dbc4b-156">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-ios</span></span>
[Mobile Service]: /develop/mobile/tutorials/get-started
<span data-ttu-id="dbc4b-157">[Notification des utilisateurs avec Notification Hubs : ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span><span class="sxs-lookup"><span data-stu-id="dbc4b-157">[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet</span></span>
<span data-ttu-id="dbc4b-158">[Notification des utilisateurs avec Notification Hubs : Mobile Services]: /manage/services/notification-hubs/notify-users</span><span class="sxs-lookup"><span data-stu-id="dbc4b-158">[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users</span></span>
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
