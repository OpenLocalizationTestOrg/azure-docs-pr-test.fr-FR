---
title: "aaaAzure Mobile Engagement iOS procédure de mise à niveau de SDK | Documents Microsoft"
description: "Dernières mises à jour et procédures du Kit de développement logiciel (SDK) iOS pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 72a9e493-3f14-4e52-b6e2-0490fd04b184
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 12/13/2016
ms.author: piyushjo
ms.openlocfilehash: 5a81bcaaec72aec665b3334e6400d520454d56a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-procedures"></a>Procédures de mise à niveau
Si vous avez déjà intégré une version antérieure d’implication dans votre application, vous avez hello tooconsider hello Kit de développement logiciel de la mise à niveau les points suivants.

Pour chaque nouvelle version du Kit de développement logiciel de hello vous devez d’abord remplacer (supprimer et importer de nouveau dans xcode) hello dossiers EngagementSDK et EngagementReach.

## <a name="from-300-too400"></a>À partir de 3.0.0 too4.0.0
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

### <a name="usernotifications-framework"></a>Infrastructure UserNotifications
Vous devez tooadd hello `UserNotifications` framework dans les Phases de votre Build.

dans l’Explorateur de projets hello, ouvrir votre projet et sélectionnez cible hello. Ensuite, ouvrez hello **« Build phases »** onglet et Bonjour **« Binaire avec des bibliothèques de liens »** menu, ajoutez framework `UserNotifications.framework` -définir un lien hello en tant que`Optional`

### <a name="application-push-capability"></a>Fonctionnalité push de l’application
XCode 8 peut réinitialiser votre application push de capacité, vérifiez qu’il Bonjour `capability` onglet de votre cible sélectionné.

### <a name="add-hello-new-ios-10-notification-registration-code"></a>Ajouter du code d’enregistrement notification 10 iOS hello
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

### <a name="resolve-unusernotificationcenter-delegate-conflicts"></a>Résoudre les conflits de délégués UNUserNotificationCenter

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

## <a name="from-200-too300"></a>À partir de 2.0.0 too3.0.0
Prise en charge d’iOS 4.X abandonnée. À partir de cette cible de déploiement hello version de votre application doit être au moins iOS 6.

Si vous utilisez la portée de votre application, vous devez ajouter `remote-notification` valeur toohello `UIBackgroundModes` tableau dans votre fichier Info.plist dans les notifications de commande tooreceive à distance.

Hello méthode `application:didReceiveRemoteNotification:` doit toobe remplacé par `application:didReceiveRemoteNotification:fetchCompletionHandler:` dans votre délégué de l’application.

« AEPushDelegate.h » est déconseillée interface et que vous devez tooremove toutes les références. Cela inclut la suppression `[[EngagementAgent shared] setPushDelegate:self]` et hello déléguer des méthodes à partir de votre délégué de l’application :

    -(void)willRetrieveLaunchMessage;
    -(void)didFailToRetrieveLaunchMessage;
    -(void)didReceiveLaunchMessage:(AEPushMessage*)launchMessage;

## <a name="from-1160-too200"></a>À partir de 1.16.0 too2.0.0
Hello suivante décrit comment toomigrate une intégration du Kit de développement logiciel de hello Capptain service offert par Capptain SAS dans une application grâce à Azure Mobile Engagement.
Si vous effectuez une migration à partir d’une version antérieure, consultez hello Capptain site web toomigrate too1.16 tout d’abord, puis appliquer hello suivant la procédure.

> [!IMPORTANT]
> Capptain et Mobile Engagement sont hello pas les mêmes services et procédure hello fourni ci-dessous uniquement met en évidence comment toomigrate hello application cliente. Migration hello SDK dans l’application hello ne fait pas migrer vos données des hello Capptain toohello Mobile Engagement serveurs
> 
> 

### <a name="agent"></a>Agent
Hello méthode `registerApp:` a été remplacée par la nouvelle méthode de hello `init:`. Votre délégué d'application doit être mis à jour en conséquence et utiliser la chaîne de connexion :

            - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
            {
              [...]
              [EngagementAgent init:@"YOUR_CONNECTION_STRING"];
              [...]
            }

Suivi de SmartAd a été supprimé à partir du Kit de développement logiciel vous devez tooremove toutes les instances de `AETrackModule` classe

### <a name="class-name-changes"></a>Modifications de nom de classe
Dans le cadre de hello repositionnement, il existe deux classe/des noms de fichiers qui doivent toobe modifié.

Toutes les classes avec le préfixe « CP » sont renommées avec le préfixe « AE ».

Exemple :

* `CPModule.h`est renommé trop`AEModule.h`.

Toutes les classes avec le préfixe « Capptain » sont renommées avec le préfixe « Engagement ».

Exemples :

* Hello classe `CapptainAgent` est renommé trop`EngagementAgent`.
* Hello classe `CapptainTableViewController` est renommé trop`EngagementTableViewController`.
* Hello classe `CapptainUtils` est renommé trop`EngagementUtils`.
* Hello classe `CapptainViewController` est renommé trop`EngagementViewController`.

