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
# <a name="use-notification-hubs-toosend-localized-breaking-news-tooios-devices"></a>Utiliser des périphériques de Notification Hubs toosend localisée rupture news tooiOS
> [!div class="op_single_selector"]
> * [Windows Store C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toouse hello [modèles](notification-hubs-templates-cross-platform-push-messages.md) fonctionnalité de toobroadcast Azure Notification Hubs avec rupture des notifications de news qui ont été localisées par langue et de périphérique. Dans ce didacticiel, vous démarrez avec une application iOS de hello créée dans [toosend utiliser Notification Hubs actualités]. Lorsque vous avez terminé, que vous serez en mesure de tooregister pour les catégories qui que vous intéressez, spécifiez une langue dans les notifications de hello tooreceive et recevoir des notifications push uniquement pour les catégories de hello sélectionné dans cette langue.

Voici un scénario de toothis deux parties :

* application iOS permet de client appareils toospecify une langue et toodifferent toosubscribe avec rupture des catégories d’informations ;
* notifications de hello, à l’aide de hello diffuse Hello principal **balise** et **modèle** profiter de Azure Notification Hubs.

## <a name="prerequisites"></a>Composants requis
Vous devez avoir déjà terminé hello [toosend utiliser Notification Hubs actualités] didacticiel et code hello disponible, car ce didacticiel s’appuie directement sur ce code.

Visual Studio 2012 ou une version ultérieure est facultative.

## <a name="template-concepts"></a>Concepts de modèle
Dans [toosend utiliser Notification Hubs actualités] vous avez créé une application qui a utilisé **balises** toonotifications toosubscribe pour les catégories d’informations différente.
Cependant, de nombreuses applications sont destinées à plusieurs marchés et doivent donc être localisées. Cela signifie que que le contenu des notifications hello eux-mêmes hello ont toobe localisée toohello livré corriger l’ensemble d’appareils.
Dans cette rubrique, nous allons montrer comment toouse hello **modèle** fonctionnalité de Notification Hubs tooeasily remettre localisée des notifications sur l’actualité.

Remarque : une façon toosend localisée notifications est toocreate plusieurs versions de ces balises. Par exemple, toosupport en anglais, Français et Mandarin, il nous faudrait trois balises différentes pour les nouvelles : « world_en », « world_fr » et « world_ch ». Nous devons à toosend ensuite une version localisée de hello world news tooeach de ces balises. Dans cette rubrique, nous utilisons prolifération de hello tooavoid modèles de balises et l’exigence de hello envoyer plusieurs messages.

À un niveau élevé, les modèles sont un moyen toospecify comment un périphérique spécifique doit recevoir une notification. modèle de Hello Spécifie le format de charge utile exacte de hello en vous reportant tooproperties qui font partie de message de type hello envoyée par votre serveur principal d’application. Aux fins de notre exemple, nous allons envoyer un message de paramètres régionaux contenant toutes les langues prises en charge :

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Ensuite, nous nous assurons qu’appareils auprès d’un modèle qui fait référence de propriété correcte de toohello. Par exemple, une application iOS qui souhaite tooregister news Français inscrira suivant de hello :

    {
        aps:{
            alert: "$(News_French)"
        }
    }

Les modèles sont une fonctionnalité très puissante sur laquelle vous pouvez obtenir plus d’informations en lisant notre article [Modèles](notification-hubs-templates-cross-platform-push-messages.md) .

## <a name="hello-app-user-interface"></a>interface utilisateur d’application Hello
Maintenant, nous allons modifier hello dernières nouvelles applications que vous avez créé dans la rubrique de hello [toosend utiliser Notification Hubs actualités] toosend localisée des informations de dernière minute à l’aide de modèles.

Dans votre MainStoryboard_iPhone.storyboard, ajoutez un contrôle segmenté avec les langages hello trois qui nous prendrons en charge : anglais, Français et Mandarin.

![][13]

Puis faire tooadd qu’un type IBOutlet dans votre ViewController.h comme indiqué ci-dessous :

![][14]

## <a name="building-hello-ios-app"></a>Application de construction hello iOS
1. Dans votre Notification.h ajouter hello *retrieveLocale* (méthode) et modification de la banque de hello et s’abonner des méthodes comme indiqué ci-dessous :
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet*) categories completion: (void (^)(NSError* error))completion;
   
        - (void) subscribeWithLocale:(int) locale categories:(NSSet*) categories completion:(void (^)(NSError *))completion;
   
        - (NSSet*) retrieveCategories;
   
        - (int) retrieveLocale;
   
    Dans votre Notification.m, modifiez hello *storeCategoriesAndSubscribe* (méthode), en ajoutant des paramètres régionaux de hello et stockage dans hello utilisateur par défaut :
   
        - (void) storeCategoriesAndSubscribeWithLocale:(int) locale categories:(NSSet *)categories completion:(void (^)(NSError *))completion {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
            [defaults setValue:[categories allObjects] forKey:@"BreakingNewsCategories"];
            [defaults setInteger:locale forKey:@"BreakingNewsLocale"];
            [defaults synchronize];
   
            [self subscribeWithLocale: locale categories:categories completion:completion];
        }
   
    Modifiez hello *s’abonner* paramètres régionaux de méthode tooinclude hello :
   
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
   
    Notez la façon dont nous utilisons maintenant méthode hello *registerTemplateWithDeviceToken*, au lieu de *registerNativeWithDeviceToken*. Lors de l’enregistrement d’un modèle nous qu’au modèle de json tooprovide hello et également un nom pour le modèle de hello (notre application pourriez tooregister des modèles différents). Assurez-vous que tooregister vos catégories sous forme de balises, comme nous voulons toomake vraiment tooreceive hello notifciations pour ces informations.
   
    Ajouter un paramètre régional de méthode tooretrieve hello hello utilisateur paramètres par défaut :
   
        - (int) retrieveLocale {
            NSUserDefaults* defaults = [NSUserDefaults standardUserDefaults];
   
            int locale = [defaults integerForKey:@"BreakingNewsLocale"];
   
            return locale < 0?0:locale;
        }
2. Maintenant que nous avons modifié notre classe Notifications, nous avons toomake assurer que notre ViewController rend utiliser Hello UISegmentControl de nouveau. Ajouter hello ligne Bonjour *viewDidLoad* méthode toomake vraiment tooshow hello paramètres régionaux actuellement sélectionné :
   
        self.Locale.selectedSegmentIndex = [notifications retrieveLocale];
   
    Ensuite, dans votre *s’abonner* (méthode), modifiez votre appel toohello *storeCategoriesAndSubscribe* toohello suivant :
   
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
3. Enfin, vous avez tooupdate hello *didRegisterForRemoteNotificationsWithDeviceToken* méthode dans votre AppDelegate.m, afin que vous pouvez actualiser correctement de votre inscription au démarrage de votre application. Modifiez votre appel toohello *s’abonner* méthode des notifications avec les éléments suivants de hello :
   
        NSSet* categories = [self.notifications retrieveCategories];
        int locale = [self.notifications retrieveLocale];
        [self.notifications subscribeWithLocale: locale categories:categories completion:^(NSError* error) {
            if (error != nil) {
                NSLog(@"Error registering for notifications: %@", error);
            }
        }];

## <a name="optional-send-localized-template-notifications-from-net-console-app"></a>(facultatif) Envoyer des notifications de modèle localisé à partir de l’application console .NET.
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

## <a name="optional-send-localized-template-notifications-from-hello-device"></a>(facultatif) Envoyer des notifications de modèles localisés à partir de l’appareil de hello
Si vous n’avez accès tooVisual Studio, voulez ou test toojust envoyer des notifications de modèle hello localisée directement à partir de l’application hello sur l’appareil de hello.  Vous pouvez simple ajouter hello localisée modèle paramètres toohello `SendNotificationRESTAPI` méthode que vous avez définies dans le cadre du didacticiel précédent hello.

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




## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur l’utilisation des modèles, consultez :

* [Notification des utilisateurs avec Notification Hubs : ASP.NET]
* [Notification des utilisateurs avec Notification Hubs : Mobile Services]

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
