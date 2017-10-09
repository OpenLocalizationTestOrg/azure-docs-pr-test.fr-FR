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
# <a name="azure-notification-hubs-secure-push"></a>Notifications Push sécurisées avec Azure Notification Hubs
> [!div class="op_single_selector"]
> * [Windows Universal](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Prise en charge des notifications push dans Microsoft Azure vous permet de tooaccess une infrastructure push facile à utiliser, multiplateforme, à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.

En raison de contraintes de sécurité ou tooregulatory, une application peut parfois tooinclude quelque chose dans la notification hello ne peut pas être transmis au moyen de l’infrastructure de notification push standard hello. Ce didacticiel explique comment tooachieve hello la même expérience en envoyant des informations sensibles via une connexion sécurisée, authentifiée entre le périphérique de hello client et serveur principal d’application hello.

À un niveau élevé, les flux hello sont comme suit :

1. Hello serveur principal d’application :
   * stocke la charge utile sécurisée dans la base de données principale ;
   * Envoie un ID hello de cet appareil toohello de notification (aucune information sécurisée est envoyée).
2. application Hello sur périphérique hello, lors de la réception de notification de hello :
   * Appareil de Hello contacte hello principal demande hello sécurisé charge utile.
   * application Hello peut afficher la charge utile de hello en tant que notification sur l’appareil de hello.

Il est important de toonote que Bonjour précédant le flux (et, dans ce didacticiel), nous supposons que cet appareil hello stocke un jeton d’authentification dans le stockage local, une fois hello utilisateur se connecte. Cela garantit une expérience entièrement transparente, comme périphérique de hello peut récupérer de données de la notification hello sécurisé à l’aide de ce jeton. Si votre application n’enregistre pas les jetons d’authentification sur l’appareil de hello, ou si ces jetons peuvent avoir expiré, hello application d’appareil, à la réception de notification de hello doit afficher une notification générique invitant hello utilisateur toolaunch hello application. application Hello puis authentifie l’utilisateur de hello et montre la charge utile de notification hello.

Ce didacticiel de Push de sécuriser montre comment toosend une notification push en toute sécurité. didacticiel de Hello s’appuie sur hello [avertir les utilisateurs](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) (didacticiel), donc vous devez effectuer les étapes de hello tout d’abord dans ce didacticiel.

> [!NOTE]
> Ce didacticiel repose sur l'hypothèse que vous avez créé et configuré votre hub de notification comme décrit dans [Prise en main de Notification Hubs (iOS)](notification-hubs-ios-apple-push-notification-apns-get-started.md).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-ios-project"></a>Modifier le projet iOS de hello
Maintenant que vous avez modifié votre hello simplement d’application back-end toosend *id* d’une notification, vous avez toochange votre toohandle d’application iOS notification et rappeler votre hello principal tooretrieve secure toobe message affiché.

tooachieve cet objectif, nous avons toowrite hello logique tooretrieve hello contenu sécurisé de hello du serveur principal d’application.

1. Dans **AppDelegate.m**, assurez-vous que registres d’application hello pour les notifications en mode silencieux afin qu’il traite les id de notification hello envoyé à partir de hello principal. Ajouter hello **UIRemoteNotificationTypeNewsstandContentAvailability** option dans didFinishLaunchingWithOptions :
   
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: UIRemoteNotificationTypeAlert | UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeNewsstandContentAvailability];
2. Dans votre **AppDelegate.m** ajouter une section d’implémentation haut hello avec hello suit déclaration :
   
        @interface AppDelegate ()
        - (void) retrieveSecurePayloadWithId:(int)payloadId completion: (void(^)(NSString*, NSError*)) completion;
        @end
3. Puis ajoutez Bonjour de section hello implémentation suivante de code, en remplaçant les espaces réservés de hello `{back-end endpoint}` avec point de terminaison hello pour votre serveur principal obtenu précédemment :

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

1. Maintenant nous qu’une notification de toohandle hello entrants et utiliser la méthode hello ci-dessus toodisplay de contenu tooretrieve hello. Tout d’abord, nous avons tooenable votre toorun d’application iOS en arrière-plan de hello lors de la réception d’une notification push. Dans **XCode**, sélectionnez votre projet d’application sur le panneau gauche hello, puis cliquez sur la cible de votre application principale Bonjour **cibles** section à partir du volet central de hello.
2. Puis cliquez sur votre **fonctionnalités** haut hello de votre volet central et vérifiez hello **des Notifications à distance** case à cocher.
   
    ![][IOS1]
3. Dans **AppDelegate.m** ajouter hello suivant des notifications push de méthode toohandle :
   
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
   
    Notez qu’il s’agit de cas de hello toohandle préférable de propriété d’en-tête d’authentification manquante ou du rejet par hello back-end. gestion spécifique de Hello de ces cas dépendent principalement de votre expérience d’utilisateur cible. Une option consiste à toodisplay une notification avec un message générique pour hello tooauthenticate tooretrieve hello réel notification à l’utilisateur.

## <a name="run-hello-application"></a>Exécutez hello Application
toorun hello application, procédez comme hello suivant :

1. Dans XCode, exécutez l’application hello sur un appareil iOS physiques (push notifications ne fonctionnera pas dans le simulateur de hello).
2. Dans une application iOS de hello l’interface utilisateur, entrez un nom d’utilisateur et un mot de passe. Il peuvent être n’importe quelle chaîne, mais ils doivent être hello la même valeur.
3. Dans une application iOS de hello l’interface utilisateur, cliquez sur **connecter**. Cliquez ensuite sur **Send push**. Vous devez voir les notification sécurisée hello s’affiche dans le centre de notification.

[IOS1]: ./media/notification-hubs-aspnet-backend-ios-secure-push/secure-push-ios-1.png
