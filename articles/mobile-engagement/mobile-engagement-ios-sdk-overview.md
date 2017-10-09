---
title: "aaaAzure Mobile Engagement iOS présentation du kit SDK | Documents Microsoft"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3a03bbd6-bcf8-436c-9775-5a8188629252
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 38f0da2f84df9c62f8fbca233bfda8b9936fdc0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-sdk-for-azure-mobile-engagement"></a>Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement
Mise en route tooget tous les détails de hello sur la façon de toointegrate Azure Mobile Engagement dans une application iOS. Si vous souhaitez que toogive il essayer en premier lieu, assurez-vous que vous faire nos [didacticiel de 15 minutes](mobile-engagement-ios-get-started.md).

Cliquez sur toosee hello [contenu du Kit de développement logiciel](mobile-engagement-ios-sdk-content.md)

## <a name="integration-procedures"></a>Procédures d'intégration
1. Démarrez ici : [comment toointegrate Mobile Engagement dans votre application iOS](mobile-engagement-ios-integrate-engagement.md)
2. Pour les Notifications : [comment toointegrate portée (Notifications) dans votre application iOS](mobile-engagement-ios-integrate-engagement-reach.md)
3. Implémentation d’un plan de la balise : [comment toouse hello avancé Mobile Engagement marquage API dans votre application iOS](mobile-engagement-ios-use-engagement-api.md)

## <a name="release-notes"></a>Notes de publication
### <a name="410-07172017"></a>4.1.0 (07/17/2017)
* Correction des badges effacés en arrière-plan.
* Correction des avertissements sur XCode 9 à propos des API qui ne sont pas appelées dans la file d’attente principale.
* Correction d’une fuite de mémoire dans les sondages Reach.
* Fin de la prise en charge d’iOS 6.X. À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 7.

Pour les versions antérieures, consultez hello [terminer les notes de publication](mobile-engagement-ios-release-notes.md)

## <a name="upgrade-procedures"></a>Procédures de mise à niveau
Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Vous avez peut-être toofollow plusieurs procédures issue de plusieurs versions de hello SDK Voir hello complète [mise à niveau des procédures](mobile-engagement-ios-upgrade-procedure.md).

Pour chaque nouvelle version du Kit de développement logiciel de hello vous devez d’abord remplacer (supprimer et importer de nouveau dans xcode) hello dossiers EngagementSDK et EngagementReach.

### <a name="from-300-too400"></a>À partir de 3.0.0 too4.0.0
### <a name="xcode-8"></a>XCode 8
XCode 8 est obligatoire à partir de la version 4.0.0 Hello SDK.

> [!NOTE]
> Si vous dépendez vraiment de XCode 7, vous pouvez utiliser hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh). Il existe un bogue connu sur le module de couverture hello de cette version précédente lors de l’exécution sur les appareils iOS 10 : notifications système ne sont pas activées. toofix avoir tooimplement hello déconseillé API `application:didReceiveRemoteNotification:` dans votre application déléguer comme suit :
>
>

    - (void)application:(UIApplication*)application
    didReceiveRemoteNotification:(NSDictionary*)userInfo
    {
        [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:nil];
    }

> [!IMPORTANT]
> **Nous ne recommandons pas cette solution de contournement** : ce comportement peut changer dans une prochaine mise à niveau (même mineure) de la version iOS car cette API iOS est déconseillée. Vous devez basculer tooXCode 8 dès que possible.
>
>

#### <a name="usernotifications-framework"></a>Infrastructure UserNotifications
Vous devez tooadd hello `UserNotifications` framework dans les Phases de votre Build.

dans l’Explorateur de projets hello, ouvrir votre projet et sélectionnez cible hello. Ensuite, ouvrez hello **« Build phases »** onglet et Bonjour **« Binaire avec des bibliothèques de liens »** menu, ajoutez framework `UserNotifications.framework` -définir un lien hello en tant que`Optional`

#### <a name="application-push-capability"></a>Fonctionnalité push de l’application
XCode 8 peut réinitialiser votre application push de capacité, vérifiez qu’il Bonjour `capability` onglet de votre cible sélectionné.

#### <a name="add-hello-new-ios-10-notification-registration-code"></a>Ajouter du code d’enregistrement notification 10 iOS hello
Hello plus anciens code extrait tooregister application hello toonotifications fonctionne toujours, mais utilise les API déconseillées lors de l’exécution sur iOS 10.

Hello d’importation `User Notification` framework :

        #import <UserNotifications/UserNotifications.h>

Dans la méthode `application:didFinishLaunchingWithOptions` de votre délégué d’application remplacez :

        if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
            [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert) categories:nil]];
            [application registerForRemoteNotifications];
        }
        else {

            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

par :

        if (NSFoundationVersionNumber >= NSFoundationVersionNumber_iOS_8_0)
        {
            if (NSFoundationVersionNumber > NSFoundationVersionNumber_iOS_9_x_Max)
            {
                [UNUserNotificationCenter.currentNotificationCenter requestAuthorizationWithOptions:(UNAuthorizationOptionBadge | UNAuthorizationOptionSound | UNAuthorizationOptionAlert) completionHandler:^(BOOL granted, NSError * _Nullable error) {}];
            }else
            {
                [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)   categories:nil]];
            }
            [application registerForRemoteNotifications];
        }
        else
        {
            [application registerForRemoteNotificationTypes:(UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
        }

#### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Résoudre les conflits de délégués UNUserNotificationCenter

*Si, ni votre application ni l’une des bibliothèques tierces n’implémente un `UNUserNotificationCenterDelegate`, vous pouvez ignorer cette partie.*

A `UNUserNotificationCenter` délégué est utilisé par le cycle de vie hello SDK toomonitor hello de notifications d’Engagement sur les appareils qui exécutent sur iOS ou supérieure à 10. Hello SDK possède sa propre implémentation de hello `UNUserNotificationCenterDelegate` de protocole, mais il peut y avoir qu’un seul `UNUserNotificationCenter` déléguer par application. Tout autre délégué ajouté toohello `UNUserNotificationCenter` objet est en conflit avec hello Engagement une. Si hello SDK détecte le délégué de votre ou de plusieurs autres tiers alors qu’il n’utilise pas sa propre implémentation toogive vous une chance tooresolve hello est en conflit. Vous devez tooadd hello Engagement logique tooyour possèdent des conflits de hello tooresolve délégué dans l’ordre.

Il existe deux façons tooachieve cela.

Proposition de 1, simplement en transfert votre délégué appelle toohello SDK :

    #import <UIKit/UIKit.h>
    #import "EngagementAgent.h"
    #import <UserNotifications/UserNotifications.h>


    @interface MyAppDelegate : NSObject <UIApplicationDelegate, UNUserNotificationCenterDelegate>
    @end

    @implementation MyAppDelegate

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterWillPresentNotification:notification withCompletionHandler:completionHandler]
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [[EngagementAgent shared] userNotificationCenterDidReceiveNotificationResponse:response withCompletionHandler:completionHandler]
    }
    @end

Ou 2, en héritant de hello `AEUserNotificationHandler` classe

    #import "AEUserNotificationHandler.h"
    #import "EngagementAgent.h"

    @interface CustomUserNotificationHandler :AEUserNotificationHandler
    @end

    @implementation CustomUserNotificationHandler

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center willPresentNotification:notification withCompletionHandler:completionHandler];
    }

    - (void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse: UNNotificationResponse *)response withCompletionHandler:(void(^)())completionHandler
    {
      // Your own logic.

      [super userNotificationCenter:center didReceiveNotificationResponse:response withCompletionHandler:completionHandler];
    }

    @end

> [!NOTE]
> Vous pouvez déterminer si une notification d’Engagement ou non, en passant son `userInfo` dictionnaire toohello Agent `isEngagementPushPayload:` méthode de classe.

Vérifiez que hello `UNUserNotificationCenter` délégué de l’objet a la valeur délégué tooyour dans soit hello `application:willFinishLaunchingWithOptions:` ou hello `application:didFinishLaunchingWithOptions:` méthode du délégué de votre application.
Par exemple, si vous avez implémenté hello ci-dessus proposition 1 :

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
        // Any other code

        [UNUserNotificationCenter currentNotificationCenter].delegate = self;
        return YES;
      }
