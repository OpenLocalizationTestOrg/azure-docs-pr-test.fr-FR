---
title: "aaaNotification concentrateurs localisée des didacticiel actualités importantes pour iOS"
description: "Découvrez comment toouse concentrateurs de Notification Azure Service Bus toosend localisée des notifications sur l’actualité (iOS)."
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
ms.openlocfilehash: 9fe88c0440e93b72d349574160ddcd85a7ba0be0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a><span data-ttu-id="87dd9-103">Utiliser des périphériques de Notification Hubs toosend localisée rupture news tooiOS</span><span class="sxs-lookup"><span data-stu-id="87dd9-103">Use Notification Hubs toosend localized breaking news tooiOS devices</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="87dd9-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="87dd9-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="87dd9-105">iOS</span><span class="sxs-lookup"><span data-stu-id="87dd9-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="87dd9-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="87dd9-106">Overview</span></span>
<span data-ttu-id="87dd9-107">Cette rubrique vous montre comment toouse hello [modèles](notification-hubs-templates-cross-platform-push-messages.md) fonctionnalité de toobroadcast Azure Notification Hubs avec rupture des notifications de news qui ont été localisées par langue et de périphérique.</span><span class="sxs-lookup"><span data-stu-id="87dd9-107">This topic shows you how toouse hello [templates](notification-hubs-templates-cross-platform-push-messages.md) feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="87dd9-108">Dans ce didacticiel, vous démarrez avec une application iOS de hello créée dans [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="87dd9-108">In this tutorial you start with hello iOS app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="87dd9-109">Lorsque vous avez terminé, que vous serez en mesure de tooregister pour les catégories qui que vous intéressez, spécifiez une langue dans les notifications de hello tooreceive et recevoir des notifications push uniquement pour les catégories de hello sélectionné dans cette langue.</span><span class="sxs-lookup"><span data-stu-id="87dd9-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="87dd9-110">Voici un scénario de toothis deux parties :</span><span class="sxs-lookup"><span data-stu-id="87dd9-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="87dd9-111">application iOS permet de client appareils toospecify une langue et toodifferent toosubscribe avec rupture des catégories d’informations ;</span><span class="sxs-lookup"><span data-stu-id="87dd9-111">iOS app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="87dd9-112">notifications de hello, à l’aide de hello diffuse Hello principal **balise** et **modèle** profiter de Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="87dd9-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87dd9-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="87dd9-113">Prerequisites</span></span>
<span data-ttu-id="87dd9-114">Vous devez avoir déjà terminé hello [toosend utiliser Notification Hubs actualités] didacticiel et code hello disponible, car ce didacticiel s’appuie directement sur ce code.</span><span class="sxs-lookup"><span data-stu-id="87dd9-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="87dd9-115">Visual Studio 2012 ou une version ultérieure est facultative.</span><span class="sxs-lookup"><span data-stu-id="87dd9-115">Visual Studio 2012 or later is optional.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="87dd9-116">Concepts de modèle</span><span class="sxs-lookup"><span data-stu-id="87dd9-116">Template concepts</span></span>
<span data-ttu-id="87dd9-117">Dans [toosend utiliser Notification Hubs actualités] vous avez créé une application qui a utilisé **balises** toonotifications toosubscribe pour les catégories d’informations différente.</span><span class="sxs-lookup"><span data-stu-id="87dd9-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="87dd9-118">Cependant, de nombreuses applications sont destinées à plusieurs marchés et doivent donc être localisées.</span><span class="sxs-lookup"><span data-stu-id="87dd9-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="87dd9-119">Cela signifie que que le contenu des notifications hello eux-mêmes hello ont toobe localisée toohello livré corriger l’ensemble d’appareils.</span><span class="sxs-lookup"><span data-stu-id="87dd9-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="87dd9-120">Dans cette rubrique, nous allons montrer comment toouse hello **modèle** fonctionnalité de Notification Hubs tooeasily remettre localisée des notifications sur l’actualité.</span><span class="sxs-lookup"><span data-stu-id="87dd9-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="87dd9-121">Remarque : une façon toosend localisée notifications est toocreate plusieurs versions de ces balises.</span><span class="sxs-lookup"><span data-stu-id="87dd9-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="87dd9-122">Par exemple, toosupport en anglais, Français et Mandarin, il nous faudrait trois balises différentes pour les nouvelles : « world_en », « world_fr » et « world_ch ».</span><span class="sxs-lookup"><span data-stu-id="87dd9-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="87dd9-123">Nous devons à toosend ensuite une version localisée de hello world news tooeach de ces balises.</span><span class="sxs-lookup"><span data-stu-id="87dd9-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="87dd9-124">Dans cette rubrique, nous utilisons prolifération de hello tooavoid modèles de balises et l’exigence de hello envoyer plusieurs messages.</span><span class="sxs-lookup"><span data-stu-id="87dd9-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="87dd9-125">À un niveau élevé, les modèles sont un moyen toospecify comment un périphérique spécifique doit recevoir une notification.</span><span class="sxs-lookup"><span data-stu-id="87dd9-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="87dd9-126">modèle de Hello Spécifie le format de charge utile exacte de hello en vous reportant tooproperties qui font partie de message de type hello envoyée par votre serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="87dd9-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="87dd9-127">Aux fins de notre exemple, nous allons envoyer un message de paramètres régionaux contenant toutes les langues prises en charge :</span><span class="sxs-lookup"><span data-stu-id="87dd9-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="87dd9-128">Ensuite, nous nous assurons qu’appareils auprès d’un modèle qui fait référence de propriété correcte de toohello.</span><span class="sxs-lookup"><span data-stu-id="87dd9-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="87dd9-129">Par exemple, une application iOS qui souhaite tooregister news Français inscrira suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="87dd9-129">For instance,  an iOS app that wants tooregister for French news will register hello following:</span></span>

    {
        aps:{
            alert: "$(News_French)"
        }
    }

<span data-ttu-id="87dd9-130">Les modèles sont une fonctionnalité très puissante sur laquelle vous pouvez obtenir plus d’informations en lisant notre article [Modèles](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="87dd9-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span>

## <a name="hello-app-user-interface"></a><span data-ttu-id="87dd9-131">interface utilisateur d’application Hello</span><span class="sxs-lookup"><span data-stu-id="87dd9-131">hello app user interface</span></span>
<span data-ttu-id="87dd9-132">Maintenant, nous allons modifier hello dernières nouvelles applications que vous avez créé dans la rubrique de hello [toosend utiliser Notification Hubs actualités] toosend localisée des informations de dernière minute à l’aide de modèles.</span><span class="sxs-lookup"><span data-stu-id="87dd9-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="87dd9-133">Dans votre MainStoryboard_iPhone.storyboard, ajoutez un contrôle segmenté avec les langages hello trois qui nous prendrons en charge : anglais, Français et Mandarin.</span><span class="sxs-lookup"><span data-stu-id="87dd9-133">In your MainStoryboard_iPhone.storyboard, add a Segmented Control with hello three languages which we will support: English, French, and Mandarin.</span></span>

![][13]

<span data-ttu-id="87dd9-134">Puis faire tooadd qu’un type IBOutlet dans votre ViewController.h comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="87dd9-134">Then make sure tooadd an IBOutlet in your ViewController.h as shown below:</span></span>

![][14]

## <a name="building-hello-ios-app"></a><span data-ttu-id="87dd9-135">Application de construction hello iOS</span><span class="sxs-lookup"><span data-stu-id="87dd9-135">Building hello iOS app</span></span>
1. <span data-ttu-id="87dd9-136">Dans votre Notification.h ajouter hello *retrieveLocale* (méthode) et modification de la banque de hello et s’abonner des méthodes comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="87dd9-136">In your Notification.h add hello *retrieveLocale* method, and modify hello store and subscribe methods as shown below:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    <span data-ttu-id="87dd9-137">Dans votre Notification.m, modifiez hello *storeCategoriesAndSubscribe* (méthode), en ajoutant des paramètres régionaux de hello et stockage dans hello utilisateur par défaut :</span><span class="sxs-lookup"><span data-stu-id="87dd9-137">In your Notification.m, modify hello *storeCategoriesAndSubscribe* method, by adding hello locale parameter and storing it in hello user defaults:</span></span>
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    <span data-ttu-id="87dd9-138">Modifiez hello *s’abonner* paramètres régionaux de méthode tooinclude hello :</span><span class="sxs-lookup"><span data-stu-id="87dd9-138">Then modify hello *subscribe* method tooinclude hello locale:</span></span>
   
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
   
    <span data-ttu-id="87dd9-139">Notez la façon dont nous utilisons maintenant méthode hello *registerTemplateWithDeviceToken*, au lieu de *registerNativeWithDeviceToken*.</span><span class="sxs-lookup"><span data-stu-id="87dd9-139">Note how we are now using hello method *registerTemplateWithDeviceToken*, instead of *registerNativeWithDeviceToken*.</span></span> <span data-ttu-id="87dd9-140">Lors de l’enregistrement d’un modèle nous qu’au modèle de json tooprovide hello et également un nom pour le modèle de hello (notre application pourriez tooregister des modèles différents).</span><span class="sxs-lookup"><span data-stu-id="87dd9-140">When we register for a template we have tooprovide hello json template and also a name for hello template (as our app might want tooregister different templates).</span></span> <span data-ttu-id="87dd9-141">Assurez-vous que tooregister vos catégories sous forme de balises, comme nous voulons toomake vraiment tooreceive hello notifciations pour ces informations.</span><span class="sxs-lookup"><span data-stu-id="87dd9-141">Make sure tooregister your categories as tags, as we want toomake sure tooreceive hello notifciations for those news.</span></span>
   
    <span data-ttu-id="87dd9-142">Ajouter un paramètre régional de méthode tooretrieve hello hello utilisateur paramètres par défaut :</span><span class="sxs-lookup"><span data-stu-id="87dd9-142">Add a method tooretrieve hello locale from hello user default settings:</span></span>
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. <span data-ttu-id="87dd9-143">Maintenant que nous avons modifié notre classe Notifications, nous avons toomake assurer que notre ViewController rend utiliser Hello UISegmentControl de nouveau.</span><span class="sxs-lookup"><span data-stu-id="87dd9-143">Now that we modified our Notifications class, we have toomake sure that our ViewController makes use of hello new UISegmentControl.</span></span> <span data-ttu-id="87dd9-144">Ajouter hello ligne Bonjour *viewDidLoad* méthode toomake vraiment tooshow hello paramètres régionaux actuellement sélectionné :</span><span class="sxs-lookup"><span data-stu-id="87dd9-144">Add hello following line in hello *viewDidLoad* method toomake sure tooshow hello locale that is currently selected:</span></span>
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    <span data-ttu-id="87dd9-145">Ensuite, dans votre *s’abonner* (méthode), modifiez votre appel toohello *storeCategoriesAndSubscribe* toohello suivant :</span><span class="sxs-lookup"><span data-stu-id="87dd9-145">Then, in your *subscribe* method, change your call toohello *storeCategoriesAndSubscribe* toohello following:</span></span>
   
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
3. <span data-ttu-id="87dd9-146">Enfin, vous avez tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* méthode dans votre AppDelegate.m, afin que vous pouvez actualiser correctement de votre inscription au démarrage de votre application.</span><span class="sxs-lookup"><span data-stu-id="87dd9-146">Finally, you have tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* method in your AppDelegate.m, so that you can correctly refresh your registration when your app starts.</span></span> <span data-ttu-id="87dd9-147">Modifiez votre appel toohello *s’abonner* méthode des notifications avec les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="87dd9-147">Change your call toohello *subscribe* method of notifications with hello following:</span></span>
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a><span data-ttu-id="87dd9-148">(facultatif) Envoyer des notifications de modèle localisé à partir de l’application console .NET.</span><span class="sxs-lookup"><span data-stu-id="87dd9-148">(optional) Send localized template notifications from .NET console app.</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a><span data-ttu-id="87dd9-149">(facultatif) Envoyer des notifications de modèles localisés à partir de l’appareil de hello</span><span class="sxs-lookup"><span data-stu-id="87dd9-149">(optional) Send localized template notifications from hello device</span></span>
<span data-ttu-id="87dd9-150">Si vous n’avez accès tooVisual Studio, voulez ou test toojust envoyer des notifications de modèle hello localisée directement à partir de l’application hello sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="87dd9-150">If you don't have access tooVisual Studio, or want toojust test sending hello localized template notifications directly from hello app on hello device.</span></span>  <span data-ttu-id="87dd9-151">Vous pouvez simple ajouter hello localisée modèle paramètres toohello `SendNotificationRESTAPI` méthode que vous avez définies dans le cadre du didacticiel précédent hello.</span><span class="sxs-lookup"><span data-stu-id="87dd9-151">You can simple add hello localized template parameters toohello `SendNotificationRESTAPI` method you defined in hello previous tutorial.</span></span>

        - (void)SendNotificationRESTAPI:(NSString*)categoryTag
        {
            NSURLSession* session = [NSURLSession sessionWithConfiguration:[NSURLSessionConfiguration
                                     defaultSessionConfiguration] delegate:nil delegateQueue:nil];

            NSString *json;

            // Construct hello messages REST endpoint
            NSURL* url = [NSURL URLWithString:[NSString stringWithFormat:@"%@%@/messages/%@", HubEndpoint,
                                               HUBNAME, API_VERSION]];

            // Generated hello token toobe used in hello authorization header.
            NSString* authorizationToken = [self generateSasToken:[url absoluteString]];

            //Create hello request tooadd hello template notification message toohello hub
            NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url];
            [request setHTTPMethod:@"POST"];

            // Add hello category as a tag
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

            //Authenticate hello notification message POST request with hello SaS token
            [request setValue:authorizationToken forHTTPHeaderField:@"Authorization"];

            //Add hello notification message body
            [request setHTTPBody:[json dataUsingEncoding:NSUTF8StringEncoding]];

            // Send hello REST request
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




## <a name="next-steps"></a><span data-ttu-id="87dd9-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="87dd9-152">Next Steps</span></span>
<span data-ttu-id="87dd9-153">Pour plus d’informations sur l’utilisation des modèles, consultez :</span><span class="sxs-lookup"><span data-stu-id="87dd9-153">For more information on using templates, see:</span></span>

* <span data-ttu-id="87dd9-154">[Notification des utilisateurs avec Notification Hubs : ASP.NET]</span><span class="sxs-lookup"><span data-stu-id="87dd9-154">[Notify users with Notification Hubs: ASP.NET]</span></span>
* <span data-ttu-id="87dd9-155">[Notification des utilisateurs avec Notification Hubs : Mobile Services]</span><span class="sxs-lookup"><span data-stu-id="87dd9-155">[Notify users with Notification Hubs: Mobile Services]</span></span>

<!-- Images. -->

[13]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized1.png
[14]: ./media/notification-hubs-ios-send-localized-breaking-news/ios_localized2.png






<!-- URLs. -->
[How To: Service Bus Notification Hubs (iOS Apps)]: http://msdn.microsoft.com/library/jj927168.aspx
[toosend utiliser Notification Hubs actualités]: /manage/services/notification-hubs/breaking-news-ios
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification des utilisateurs avec Notification Hubs : ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notification des utilisateurs avec Notification Hubs : Mobile Services]: /manage/services/notification-hubs/notify-users
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-ios
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-ios
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-users-ios
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[JavaScript and HTML]: ../get-started-with-push-js.md

[Windows Developer Preview registration steps for Mobile Services]: ../mobile-services-windows-developer-preview-registration.md
[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
