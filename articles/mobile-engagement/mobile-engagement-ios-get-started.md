---
title: "aaaGet main d’Azure Mobile Engagement pour iOS dans Objective C | Documents Microsoft"
description: "Découvrez comment toouse Azure Mobile Engagement avec analytique et des notifications push pour les applications iOS."
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 117b5742-522b-41de-98c5-f432da2d98f8
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: hero-article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 51a5013f23d2d04a7b9b30c83b47017898b2bb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-ios-apps-in-objective-c"></a>Prise en main d’Azure Mobile Engagement pour les applications iOS dans Objective C
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Cette rubrique vous montre comment toouse Azure Mobile Engagement toounderstand votre utilisation de l’application et l’envoi de notifications toosegmented utilisateurs tooan iOS application push.
Dans ce didacticiel, vous créez une application iOS vide qui collecte des données de base et reçoit des notifications push à l'aide du service APN (Apple Push Notification Service).

Ce didacticiel requiert hello qui suit :

* XCode 8, que vous pouvez installer depuis l’App Store de votre MAC
* Hello [Mobile Engagement iOS SDK]

Vous devez suivre ce didacticiel pour avoir accès à tous les autres didacticiels Mobile Engagement pour applications iOS.

> [!NOTE]
> toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif. Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes. Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-ios-get-started).
>
>

## <a id="setup-azme"></a>Configuration de Mobile Engagement pour votre application iOS
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
Ce didacticiel présente une « intégration de base », qui est hello minimal requis toocollect données et envoyer une notification push. Vous trouverez la documentation sur l’intégration complète Hello dans hello [intégration du Kit de développement logiciel iOS Mobile Engagement](mobile-engagement-ios-sdk-overview.md)

Nous allons créer une application de base avec l’intégration de hello toodemonstrate XCode.

### <a name="create-a-new-ios-project"></a>Création d’un projet iOS
[!INCLUDE [Create a new iOS Project](../../includes/mobile-engagement-create-new-ios-app.md)]

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Se connecter à votre serveur principal d’application toohello Mobile Engagement
1. Télécharger hello [Mobile Engagement iOS SDK].
2. Extraire hello. tar.gz fichier tooa dossier sur votre ordinateur.
3. Projet de hello d’avec le bouton droit et sélectionnez **ajouter des fichiers à**.

    ![][1]
4. Exploration du dossier toohello où vous avez extrait hello SDK, sélectionnez hello `EngagementSDK` dossier, cliquez sur **Options** hello coin inférieur gauche et assurez-vous que cette case à cocher hello **copier des éléments si nécessaire** et hello case à cocher pour votre cible sont cochées, puis appuyez sur **OK**.

    ![][2]
5. Ouvrez hello **générer les Phases** onglet et Bonjour **binaire avec des bibliothèques de liens** menu, ajouter des infrastructures de hello comme indiqué ci-dessous :

    ![][3]
6. Revenir en arrière toohello portail Azure dans votre application **informations de connexion** page et copie la chaîne de connexion hello.

    ![][4]
7. Ajouter hello suivant la ligne de code dans votre **AppDelegate.m** fichier.

        #import "EngagementAgent.h"
8. Collez maintenant la chaîne de connexion hello Bonjour `didFinishLaunchingWithOptions` déléguer.

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
              [...]   
              [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
              [...]
        }
9. `setTestLogEnabled`est une instruction facultative qui active les journaux du Kit de développement logiciel pour vous tooidentify problèmes.

## <a id="monitor"></a>Activation de l’analyse en temps réel
Dans l’ordre toostart envoi de données et en garantissant que les utilisateurs de hello sont actifs, vous devez envoyer au moins un principal de Mobile Engagement toohello écran (activité).

1. Ouvrez hello **ViewController.h** de fichier et importer **EngagementViewController.h**:

    `#import "EngagementViewController.h"`
2. Maintenant remplacer superclasse de hello Hello **ViewController** par l’interface `EngagementViewController`:

    `@interface ViewController : EngagementViewController`

## <a id="monitor"></a>Connexion d’application avec l’analyse en temps réel
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Activation des notifications push et de la messagerie in-app
Mobile Engagement vous permet de toointeract avec vos utilisateurs et portée avec des notifications push et les messages dans le contexte de hello de campagnes dans l’application. Ce module est appelé portée dans le portail Mobile Engagement de hello.
Hello sections suivantes configurer votre application tooreceive les.

### <a name="enable-your-app-tooreceive-silent-push-notifications"></a>Activer votre tooreceive d’application en mode silencieux des Notifications Push
[!INCLUDE [mobile-engagement-ios-silent-push](../../includes/mobile-engagement-ios-silent-push.md)]

### <a name="add-hello-reach-library-tooyour-project"></a>Ajouter un projet de hello portée bibliothèque tooyour
1. Cliquez avec le bouton droit sur votre projet.
2. Sélectionnez **Add file to**.
3. Parcourir le dossier toohello où vous avez extrait hello SDK.
4. Sélectionnez hello `EngagementReach` dossier.
5. Cliquez sur **Add**.

### <a name="modify-your-application-delegate"></a>Modifier votre délégué d'Application
1. Dans les **AppDeletegate.m** de fichiers, importez le module d’Engagement atteindre hello.

        #import "AEReachModule.h"
        #import <UserNotifications/UserNotifications.h>
2. À l’intérieur hello `application:didFinishLaunchingWithOptions` (méthode), créer un module de couverture et passer en ligne de l’initialisation Engagement tooyour existante :

        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
            AEReachModule * reach = [AEReachModule moduleWithNotificationIcon:[UIImage imageNamed:@"icon.png"]];
            [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}" modules:reach, nil];
            [...]
            return YES;
        }

### <a name="enable-your-app-tooreceive-apns-push-notifications"></a>Activer votre tooreceive application APNS les Notifications Push
1. Ajouter hello suivant ligne toohello `application:didFinishLaunchingWithOptions` méthode :

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
2. Ajouter hello `application:didRegisterForRemoteNotificationsWithDeviceToken` méthode comme suit :

        - (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken
        {
             [[EngagementAgent shared] registerDeviceToken:deviceToken];
            NSLog(@"Registered Token: %@", deviceToken);
        }
3. Ajouter hello `didFailToRegisterForRemoteNotificationsWithError` méthode comme suit :

        - (void)application:(UIApplication*)application didFailToRegisterForRemoteNotificationsWithError:(NSError*)error
        {
           NSLog(@"Failed tooget token, error: %@", error);
        }
4. Ajouter hello `didReceiveRemoteNotification:fetchCompletionHandler` méthode comme suit :

        - (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult result))handler
        {
            [[EngagementAgent shared] applicationDidReceiveRemoteNotification:userInfo fetchCompletionHandler:handler];
        }

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- URLs. -->
[Mobile Engagement iOS SDK]: http://aka.ms/qk2rnj

<!-- Images. -->
[1]: ./media/mobile-engagement-ios-get-started/xcode-add-files.png
[2]: ./media/mobile-engagement-ios-get-started/xcode-select-engagement-sdk.png
[3]: ./media/mobile-engagement-ios-get-started/xcode-build-phases.png
[4]: ./media/mobile-engagement-ios-get-started/app-connection-info-page.png
