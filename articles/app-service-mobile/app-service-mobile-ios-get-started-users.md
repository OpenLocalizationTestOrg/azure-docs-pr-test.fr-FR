---
title: "aaaAdd d’authentification sur iOS avec les applications mobiles Azure"
description: "Découvrez comment toouse Azure Mobile Apps tooauthenticate les utilisateurs de votre application iOS via une variété de fournisseurs d’identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: ef3d3cbe-e7ca-45f9-987f-80c44209dc06
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: glenga
ms.openlocfilehash: df129e1c7517582db0e4705e0a6e98345ac8a48c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-ios-app"></a>Ajouter une application de l’authentification tooyour iOS
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Dans ce didacticiel, vous ajoutez l’authentification toohello [iOS rapides Démarrer] de projet à l’aide d’un fournisseur d’identité pris en charge. Ce didacticiel est basé sur hello [iOS rapides Démarrer] didacticiel, vous devez effectuer en premier.

## <a name="register"></a>Inscrire votre application pour l’authentification et de configurer hello du Service d’applications
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application

L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.  Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.  Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.  Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.  Il doit être unique tooyour des applications mobiles.  redirection de hello tooenable côté serveur de th :

1. Bonjour [portail Azure], sélectionnez votre application de Service.

2. Cliquez sur hello **l’authentification / autorisation** option de menu.

3. Cliquez sur **Azure Active Directory** sous hello **fournisseurs d’authentification** section.

4. Ensemble hello **mode de gestion** trop**avancé**.

5. Bonjour **autorisé des URL de redirection externe**, entrez `appname://easyauth.callback`.  Hello _appname_ dans cette chaîne est hello le modèle d’URL pour votre application mobile.  Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).  Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.

6. Cliquez sur **OK**.

7. Cliquez sur **Enregistrer**.

## <a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Dans Xcode, appuyez sur **exécuter** toostart hello application. Une exception est levée, car l’application hello tente tooaccess le serveur principal en tant qu’un utilisateur non authentifié, mais hello *TodoItem* table requiert l’authentification.

## <a name="add-authentication"></a>Ajouter l’authentification tooapp
**Objective-C**:

1. Sur votre Mac, ouvrez *QSTodoListViewController.m* dans Xcode et ajoutez hello suivant de méthode :

    ```Objective-C
    - (void)loginAndGetData
    {
        QSAppDelegate *appDelegate = (QSAppDelegate *)[UIApplication sharedApplication].delegate;
        appDelegate.qsTodoService = self.todoService;

        [self.todoService.client loginWithProvider:@"google" urlScheme:@"appname" controller:self animated:YES completion:^(MSUser * _Nullable user, NSError * _Nullable error) {
            if (error) {
                NSLog(@"Login failed with error: %@, %@", error, [error userInfo]);
            }
            else {
                self.todoService.client.currentUser = user;
                NSLog(@"User logged in: %@", user.userId);

                [self refresh];
            }
        }];
    }
    ```

    Modification *google* trop*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* si vous n’utilisez pas de Google comme fournisseur d’identité. Si vous utilisez Facebook, vous devrez [autoriser les domaines Facebook][1] dans votre application.

    Remplacez hello **urlScheme** avec un nom unique pour votre application.  Hello urlScheme doit être hello même comme hello protocole de modèle d’URL que vous avez spécifié dans hello **autorisé des URL de redirection externe** champ hello portail Azure. Hello urlScheme est utilisé par hello authentification rappel tooswitch tooyour arrière application une fois la demande d’authentification est terminée.

2. Remplacez `[self refresh]` dans `viewDidLoad` dans *QSTodoListViewController.m* avec hello suivant de code :

    ```Objective-C
    [self loginAndGetData];
    ```

3. Ouvrez hello `QSAppDelegate.h` et ajoutez hello suivant de code :

    ```Objective-C
    #import "QSTodoService.h"

    @property (strong, nonatomic) QSTodoService *qsTodoService;
    ```

4. Ouvrez hello `QSAppDelegate.m` et ajoutez hello suivant de code :

    ```Objective-C
    - (BOOL)application:(UIApplication *)application openURL:(NSURL *)url options:(NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options
    {
        if ([[url.scheme lowercaseString] isEqualToString:@"appname"]) {
            // Resume login flow
            return [self.qsTodoService.client resumeWithURL:url];
        }
        else {
            return NO;
        }
    }
    ```

   Ajoutez ce code juste avant la lecture de ligne hello `#pragma mark - Core Data stack`.  Remplacez le _appname_ permanence hello urlScheme valeur que vous avez utilisé à l’étape 1.

5. Ouvrez hello `AppName-Info.plist` (en remplaçant AppName avec nom hello de votre application) et ajoutez hello suivant de code :

    ```XML
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Ce code doit être placé à l’intérieur de hello `<dict>` élément.  Remplacez hello _appname_ chaîne (dans le tableau pour **CFBundleURLSchemes**) avec le nom de l’application hello choisi à l’étape 1.  Vous pouvez également apporter ces modifications dans hello plist éditeur - cliquez sur hello `AppName-Info.plist` fichier dans XCode tooopen hello plist éditeur.

    Remplacez hello `com.microsoft.azure.zumo` de chaîne pour **CFBundleURLName** avec votre Apple identificateur d’offres groupées.

6. Appuyez sur *exécuter* toostart hello app, puis connectez-vous. Lorsque vous êtes connecté, vous devez être en mesure de tooview hello Todo liste et effectuer des mises à jour.

**Swift**:

1. Sur votre Mac, ouvrez *ToDoTableViewController.swift* dans Xcode et ajoutez hello suivant de méthode :

    ```swift
    func loginAndGetData() {

        guard let client = self.table?.client, client.currentUser == nil else {
            return
        }

        let appDelegate = UIApplication.shared.delegate as! AppDelegate
        appDelegate.todoTableViewController = self

        let loginBlock: MSClientLoginBlock = {(user, error) -> Void in
            if (error != nil) {
                print("Error: \(error?.localizedDescription)")
            }
            else {
                client.currentUser = user
                print("User logged in: \(user?.userId)")
            }
        }

        client.login(withProvider:"google", urlScheme: "appname", controller: self, animated: true, completion: loginBlock)

    }
    ```

    Modification *google* trop*microsoftaccount*, *twitter*, *facebook*, ou *windowsazureactivedirectory* si vous n’utilisez pas de Google comme fournisseur d’identité. Si vous utilisez Facebook, vous devrez [autoriser les domaines Facebook][1] dans votre application.

    Remplacez hello **urlScheme** avec un nom unique pour votre application.  Hello urlScheme doit être hello même comme hello protocole de modèle d’URL que vous avez spécifié dans hello **autorisé des URL de redirection externe** champ hello portail Azure. Hello urlScheme est utilisé par hello authentification rappel tooswitch tooyour arrière application une fois la demande d’authentification est terminée.

2. Supprimer les lignes hello `self.refreshControl?.beginRefreshing()` et `self.onRefresh(self.refreshControl)` à la fin de `viewDidLoad()` dans *ToDoTableViewController.swift*. Ajoutez un appel trop`loginAndGetData()` à leur place :

    ```swift
    loginAndGetData()
    ```

3. Ouvrez hello `AppDelegate.swift` et ajoutez hello suivant ligne toohello `AppDelegate` classe :

    ```swift
    var todoTableViewController: ToDoTableViewController?

    func application(_ application: UIApplication, openURL url: NSURL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
        if url.scheme?.lowercased() == "appname" {
            return (todoTableViewController!.table?.client.resume(with: url as URL))!
        }
        else {
            return false
        }
    }
    ```

    Remplacez hello _appname_ permanence hello urlScheme valeur que vous avez utilisé à l’étape 1.

4. Ouvrez hello `AppName-Info.plist` (en remplaçant AppName avec nom hello de votre application) et ajoutez hello suivant de code :

    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLName</key>
            <string>com.microsoft.azure.zumo</string>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>appname</string>
            </array>
        </dict>
    </array>
    ```

    Ce code doit être placé à l’intérieur de hello `<dict>` élément.  Remplacez hello _appname_ chaîne (dans le tableau pour **CFBundleURLSchemes**) avec le nom de l’application hello choisi à l’étape 1.  Vous pouvez également apporter ces modifications dans hello plist éditeur - cliquez sur hello `AppName-Info.plist` fichier dans XCode tooopen hello plist éditeur.

    Remplacez hello `com.microsoft.azure.zumo` de chaîne pour **CFBundleURLName** avec votre Apple identificateur d’offres groupées.

5. Appuyez sur *exécuter* toostart hello app, puis connectez-vous. Lorsque vous êtes connecté, vous devez être en mesure de tooview hello Todo liste et effectuer des mises à jour.

L’authentification App Service utilise la communication inter-application d’Apple.  Pour plus d’informations sur ce sujet, consultez toohello [Documentation Apple][2]
<!-- URLs. -->

[1]: https://developers.facebook.com/docs/ios/ios9#whitelist
[2]: https://developer.apple.com/library/content/documentation/iPhone/Conceptual/iPhoneOSProgrammingGuide/Inter-AppCommunication/Inter-AppCommunication.html
[portail Azure]: https://portal.azure.com

[iOS rapides Démarrer]: app-service-mobile-ios-get-started.md

