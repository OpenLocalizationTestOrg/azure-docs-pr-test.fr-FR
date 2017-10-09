---
title: aaaHow tooUse SDK iOS pour les applications mobiles Azure
description: Comment tooUse SDK iOS pour les applications mobiles Azure
services: app-service\mobile
documentationcenter: ios
author: ysxu
manager: yochayk
editor: 
ms.assetid: 4e8e45df-c36a-4a60-9ad4-393ec10b7eb9
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 10/01/2016
ms.author: yuaxu
ms.openlocfilehash: fa299ab3f152bad12d821832fa9fb5495d1fa296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ios-client-library-for-azure-mobile-apps"></a>Comment tooUse iOS bibliothèque cliente pour les applications mobiles Azure
[!INCLUDE [app-service-mobile-selector-client-library](../../includes/app-service-mobile-selector-client-library.md)]

Ce guide vous explique tooperform des scénarios courants utilisant hello dernières [e/s des applications mobiles Azure SDK][1]. Si vous êtes tooAzure Mobile de nouvelles applications, d’abord terminer [démarrage rapide d’Azure Mobile Apps] toocreate un service principal, créez une table et télécharger un projet de Xcode avant génération iOS. Dans ce guide, nous concentrer sur hello côté client iOS SDK. toolearn savoir plus sur hello du Kit de développement logiciel côté serveur pour hello principal, consultez hello serveur SDK la.

## <a name="reference-documentation"></a>Documentation de référence
Hello documentation de référence pour le client d’iOS hello SDK se trouve ici : [e/s des applications mobiles Azure Client référence][2].

## <a name="supported-platforms"></a>Plateformes prises en charge
Hello, iOS SDK prend en charge les projets Objective-C, les projets Swift 2.2 ou Swift 2.3 pour iOS version 8.0 ou ultérieure.

l’authentification de « flux de serveur » Hello utilise un WebView hello affiche l’interface utilisateur.  Si l’appareil de hello n’est pas en mesure de toopresent un UI WebView, une autre méthode d’authentification est requise, qui est extérieur étendue hello du produit de hello.  
Ce SDK ne convient donc pas au type Watch ou d’autres appareils restreints similaires.

## <a name="Setup"></a>Configuration et conditions préalables
Ce guide part du principe que vous avez créé un serveur principal avec une table. Ce guide part du principe que la table hello a le même schéma que les tables hello dans ces didacticiels. Ce guide suppose également que dans votre code, vous référencez `MicrosoftAzureMobile.framework` et importez `MicrosoftAzureMobile/MicrosoftAzureMobile.h`.

## <a name="create-client"></a>Création du client
tooaccess un serveur d’applications mobiles Azure principal dans votre projet, créez un `MSClient`. Remplacez `AppUrl` avec l’URL de l’application hello. Vous pouvez laisser `gatewayURLString` et `applicationKey` vides. Si vous configurez une passerelle pour l’authentification, remplir `gatewayURLString` avec l’URL de la passerelle hello.

**Objective-C**:

```
MSClient *client = [MSClient clientWithApplicationURLString:@"AppUrl"];
```

**Swift**:

```
let client = MSClient(applicationURLString: "AppUrl")
```


## <a name="table-reference"></a>Procédure : création d'une référence de table
tooaccess ou mise à jour des données, créez une table de serveur principal de référence toohello. Remplacez `TodoItem` par nom de hello de votre table

**Objective-C**:

```
MSTable *table = [client tableWithName:@"TodoItem"];
```

**Swift**:

```
let table = client.tableWithName("TodoItem")
```


## <a name="querying"></a>Procédure : interrogation des données
toocreate une requête de base de données, hello de requête `MSTable` objet. Hello requête suivante obtient tous les éléments hello dans `TodoItem` et journaux hello texte de chaque élément.

**Objective-C**:

```
[table readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) { // error is nil if no error occured
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) { // items is NSArray of records that match query
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
table.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="filtering"></a>Procédure : filtrage des données renvoyées
résultats de toofilter, il existe de nombreuses options disponibles.

toofilter à l’aide d’un prédicat, utilisez un `NSPredicate` et `readWithPredicate`. suivant de Hello filtre les éléments de données retournées toofind uniquement incomplètes Todo.

**Objective-C**:

```
// Create a predicate that finds items where complete is false
NSPredicate * predicate = [NSPredicate predicateWithFormat:@"complete == NO"];
// Query hello TodoItem table
[table readWithPredicate:predicate completion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
// Create a predicate that finds items where complete is false
let predicate =  NSPredicate(format: "complete == NO")
// Query hello TodoItem table
table.readWithPredicate(predicate) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```

## <a name="query-object"></a>Procédure : utilisation de MSQuery
tooperform une requête complexe (y compris le tri et la pagination), créer un `MSQuery` de l’objet, directement ou à l’aide d’un prédicat :

**Objective-C**:

```
MSQuery *query = [table query];
MSQuery *query = [table queryWithPredicate: [NSPredicate predicateWithFormat:@"complete == NO"]];
```

**Swift**:

```
let query = table.query()
let query = table.queryWithPredicate(NSPredicate(format: "complete == NO"))
```

`MSQuery` vous permet de contrôler plusieurs comportements de requête.

* Spécifier l’ordre des résultats
* Limite les champs tooreturn
* Limiter le nombre d’enregistrements tooreturn
* Spécifier le nombre total dans la réponse
* Spécifier des paramètres de chaîne de requête personnalisés dans la requête
* Appliquer des fonctions supplémentaires

Exécuter un `MSQuery` requête en appelant `readWithCompletion` sur l’objet de hello.

## <a name="sorting"></a>Procédure : trier des données avec MSQuery
résultats de toosort, examinons un exemple. toosort par ordre croissant de 'text' de champ, puis par ordre décroissant de « complète », appelez `MSQuery` comme suit :

**Objective-C**:

```
[query orderByAscending:@"text"];
[query orderByDescending:@"complete"];
[query readWithCompletion:^(MSQueryResult *result, NSError *error) {
        if(error) {
                NSLog(@"ERROR %@", error);
        } else {
                for(NSDictionary *item in result.items) {
                        NSLog(@"Todo Item: %@", [item objectForKey:@"text"]);
                }
        }
}];
```

**Swift**:

```
query.orderByAscending("text")
query.orderByDescending("complete")
query.readWithCompletion { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let items = result?.items {
        for item in items {
            print("Todo Item: ", item["text"])
        }
    }
}
```


## <a name="selecting"></a><a name="parameters"></a>Procédure : limitation des champs et développement des paramètres de chaîne de requête avec MSQuery
toolimit toobe de champs renvoyé dans une requête, spécifiez les noms de champs de hello hello dans hello **selectFields** propriété. Cet exemple retourne uniquement le texte hello et champs terminés :

**Objective-C**:

```
query.selectFields = @[@"text", @"complete"];
```

**Swift**:

```
query.selectFields = ["text", "complete"]
```

paramètres de chaîne de requête supplémentaire de tooinclude dans hello server demande (par exemple, parce qu’un script côté serveur personnalisé utilise les), remplir `query.parameters` comme suit :

**Objective-C**:

```
query.parameters = @{
    @"myKey1" : @"value1",
    @"myKey2" : @"value2",
};
```

**Swift**:

```
query.parameters = ["myKey1": "value1", "myKey2": "value2"]
```

## <a name="paging"></a>Procédure : configuration du format de page
Avec les applications mobiles Azure, les contrôles de taille de page hello hello nombre d’enregistrements qui sont extraites à la fois à partir des tables de back-end hello. Un appel trop`pull` données puis de lots des données, en fonction de cette taille de page, jusqu'à ce qu’il n’y a aucun plus toopull d’enregistrements.

Il s’agit d’une taille de page à l’aide de tooconfigure possible **MSPullSettings** comme indiqué ci-dessous. taille de page Hello par défaut est 50, et exemple hello ci-dessous modifie too3.

Vous pouvez configurer un autre format de page pour des raisons de performances. Si vous avez un grand nombre d’enregistrements de données de petite taille, une taille de page élevée allège hello d’allers-retours de serveur.

Ce paramètre contrôle uniquement hello taille de la page côté client de hello. Si hello client demande une plus grande taille de page que prend en charge les principaux des applications mobiles hello, taille de la page hello est limitée à hello hello maximale principal est toosupport configuré.

Ce paramètre est également hello *nombre* d’enregistrements de données, pas hello *taille en octets*.

Si vous augmentez la taille de la page hello client, vous devez également augmenter la taille de page de hello sur le serveur hello. Consultez [« Comment : ajuster la taille de la pagination de table hello »](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour hello étapes toodo.

**Objective-C**:

```
  MSPullSettings *pullSettings = [[MSPullSettings alloc] initWithPageSize:3];
  [table  pullWithQuery:query queryId:@nil settings:pullSettings
                        completion:^(NSError * _Nullable error) {
                               if(error) {
                    NSLog(@"ERROR %@", error);
                }
                           }];
```


**Swift**:

```
let pullSettings = MSPullSettings(pageSize: 3)
table.pullWithQuery(query, queryId:nil, settings: pullSettings) { (error) in
    if let err = error {
        print("ERROR ", err)
    }
}
```

## <a name="inserting"></a>Procédure : insertion de données
tooinsert une nouvelle ligne de table, créer un `NSDictionary` et appeler `table insert`. Si [le schéma dynamique] est activé, service principal de Service d’applications Azure mobile hello génère automatiquement de nouvelles colonnes selon hello `NSDictionary`.

Si `id` n’est pas fourni, hello principal génère automatiquement un nouvel ID unique. Fournissez votre propre `id` toouse adresses de messagerie, les noms d’utilisateur ou vos propres valeurs en tant que code. Fournir son propre ID peut faciliter les jointures et la logique de base de données orientée métier.

Hello `result` contient hello nouvel élément a été inséré. Selon la logique du serveur, peut-être supplémentaires, ou des données modifiées comparées toowhat a été transmise toohello server.

**Objective-C**:

```
NSDictionary *newItem = @{@"id": @"custom-id", @"text": @"my new item", @"complete" : @NO};
[table insert:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
let newItem = ["id": "custom-id", "text": "my new item", "complete": false]
table.insert(newItem) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

## <a name="modifying"></a>Procédure : modification des données
tooupdate une ligne existante, modifier un élément et l’appel `update`:

**Objective-C**:

```
NSMutableDictionary *newItem = [oldItem mutableCopy]; // oldItem is NSDictionary
[newItem setValue:@"Updated text" forKey:@"text"];
[table update:newItem completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
if let newItem = oldItem.mutableCopy() as? NSMutableDictionary {
    newItem["text"] = "Updated text"
    table2.update(newItem as [NSObject: AnyObject], completion: { (result, error) -> Void in
        if let err = error {
            print("ERROR ", err)
        } else if let item = result {
            print("Todo Item: ", item["text"])
        }
    })
}
```

Vous pouvez également fournir les ID de ligne hello et champ de hello mis à jour :

**Objective-C**:

```
[table update:@{@"id":@"custom-id", @"text":"my EDITED item"} completion:^(NSDictionary *result, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item: %@", [result objectForKey:@"text"]);
    }
}];
```

**Swift**:

```
table.update(["id": "custom-id", "text": "my EDITED item"]) { (result, error) in
    if let err = error {
        print("ERROR ", err)
    } else if let item = result {
        print("Todo Item: ", item["text"])
    }
}
```

Au minimum, hello `id` attribut doit être défini lors de la mise à jour.

## <a name="deleting"></a>Procédure : suppression de données
toodelete un élément, appelez `delete` avec l’élément de hello :

**Objective-C**:

```
[table delete:item completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.delete(newItem as [NSObject: AnyObject]) { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Vous pouvez également effectuer la suppression en fournissant un ID de ligne :

**Objective-C**:

```
[table deleteWithId:@"37BBF396-11F0-4B39-85C8-B319C729AF6D" completion:^(id itemId, NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    } else {
        NSLog(@"Todo Item ID: %@", itemId);
    }
}];
```

**Swift**:

```
table.deleteWithId("37BBF396-11F0-4B39-85C8-B319C729AF6D") { (itemId, error) in
    if let err = error {
        print("ERROR ", err)
    } else {
        print("Todo Item ID: ", itemId)
    }
}
```

Au minimum, hello `id` attribut doit être défini lors de la fabrication supprime.

## <a name="customapi"></a>Procédure : appel d’une API personnalisée
Une API personnalisée vous permet d’exposer toutes les fonctionnalités du serveur principal. Il n’a d’opération de table toomap tooa. Non seulement avoir davantage de contrôle sur la messagerie, vous pouvez même en lecture/jeu d’en-têtes et de modifier le format du corps de réponse hello. toolearn comment toocreate une API personnalisée sur le serveur principal hello, lire [API personnalisées](app-service-mobile-node-backend-how-to-use-server-sdk.md#work-easy-apis)

toocall une API personnalisée, appelez `MSClient.invokeAPI`. demande de Hello et contenu de réponse sont traités en tant que JSON. toouse autres types de médias, [utilisez hello autre surcharge de `invokeAPI` ] [ 5].  toomake un `GET` demande au lieu d’un `POST` demande, le paramètre de jeu de `HTTPMethod` trop`"GET"` et paramètre `body` trop`nil` (étant donné que les demandes GET ne disposez pas des corps de message.) Si votre API personnalisée prend en charge les autres verbes HTTP, modifiez `HTTPMethod` en conséquence.

**Objective-C**:

```
[self.client invokeAPI:@"sendEmail"
                  body:@{ @"contents": @"Hello world!" }
            HTTPMethod:@"POST"
            parameters:@{ @"to": @"bill@contoso.com", @"subject" : @"Hi!" }
               headers:nil
            completion: ^(NSData *result, NSHTTPURLResponse *response, NSError *error) {
                if(error) {
                    NSLog(@"ERROR %@", error);
                } else {
                    // Do something with result
                }
            }];
```

**Swift**:

```
client.invokeAPI("sendEmail",
            body: [ "contents": "Hello World" ],
            HTTPMethod: "POST",
            parameters: [ "to": "bill@contoso.com", "subject" : "Hi!" ],
            headers: nil)
            {
                (result, response, error) -> Void in
                if let err = error {
                    print("ERROR ", err)
                } else if let res = result {
                          // Do something with result
                }
        }
```

## <a name="templates"></a>Comment : notifications de Registre push modèles toosend inter-plateformes
modèles de tooregister, passer des modèles avec votre **client.push registerDeviceToken** méthode dans votre application cliente.

**Objective-C**:

```
[client.push registerDeviceToken:deviceToken template:iOSTemplate completion:^(NSError *error) {
    if(error) {
        NSLog(@"ERROR %@", error);
    }
}];
```

**Swift**:

```
    client.push?.registerDeviceToken(NSData(), template: iOSTemplate, completion: { (error) in
        if let err = error {
            print("ERROR ", err)
        }
    })
```

Vos modèles sont de type NSDictionary et peuvent contenir plusieurs modèles Bonjour suivant le format :

**Objective-C**:

```
NSDictionary *iOSTemplate = @{ @"templateName": @{ @"body": @{ @"aps": @{ @"alert": @"$(message)" } } } };
```

**Swift**:

```
let iOSTemplate = ["templateName": ["body": ["aps": ["alert": "$(message)"]]]]
```

Toutes les balises sont supprimés de la demande de hello pour la sécurité.  les balises tooadd tooinstallations ou modèles dans les installations, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][4].  notifications de toosend à l’aide de ces modèles enregistrés, travailler avec [API de concentrateurs de Notification][3].

## <a name="errors"></a>Procédure : gestion des erreurs
Lorsque vous appelez un serveur principal de Service d’applications Azure mobile, bloc de fin hello contient un `NSError` paramètre. Si une erreur se produit, ce paramètre est non-nil. Dans votre code, vous devez vérifier ce paramètre et gérer l’erreur hello selon vos besoins, comme illustré dans hello précédant les extraits de code.

fichier de Hello [ `<WindowsAzureMobileServices/MSError.h>` ] [ 6] définit des constantes hello `MSErrorResponseKey`, `MSErrorRequestKey`, et `MSErrorServerItemKey`. tooget toohello erreur liée à plus de données :

**Objective-C**:

```
NSDictionary *serverItem = [error.userInfo objectForKey:MSErrorServerItemKey];
```

**Swift**:

```
let serverItem = error.userInfo[MSErrorServerItemKey]
```

En outre, les fichiers hello définit des constantes pour chaque code d’erreur :

**Objective-C**:

```
if (error.code == MSErrorPreconditionFailed) {
```

**Swift**:

```
if (error.code == MSErrorPreconditionFailed) {
```

## <a name="adal"></a>Comment : authentifier les utilisateurs avec hello bibliothèque d’authentification Active Directory
Vous pouvez utiliser les utilisateurs de toosign hello Active Directory Authentication Library (ADAL) dans votre application à l’aide d’Azure Active Directory. L’authentification du client flux à l’aide d’un fournisseur d’identité SDK est préférable toousing hello `loginWithProvider:completion:` (méthode).  L’authentification par client flux offre une interface UX native plus simple et permet une personnalisation supplémentaire.

1. Configurer le service principal de votre application mobile pour la connexion d’AAD par hello suivant [comment tooconfigure application de Service pour la connexion Active Directory] [ 7] didacticiel. Assurez-vous qu’étape facultative toocomplete hello d’inscription d’une application cliente native. Pour iOS, nous vous recommandons ce hello URI de redirection est sous forme de hello `<app-scheme>://<bundle-id>`. Pour plus d’informations, consultez hello [ADAL iOS quickstart][8].
2. Installez la bibliothèque ADAL à l’aide de Cocoapods. Modifier votre hello de tooinclude Podfile définition, en remplaçant **votre projet** avec nom hello de votre projet Xcode :

        source 'https://github.com/CocoaPods/Specs.git'
        link_with ['YOUR-PROJECT']
        xcodeproj 'YOUR-PROJECT'

   et hello Pod :

        pod 'ADALiOS'
3. À l’aide de hello Terminal Server, exécutez `pod install` à partir du répertoire de hello contenant votre projet, puis ouvrez espace de travail Xcode hello généré (pas le projet hello).
4. Ajoutez hello après application de code tooyour, selon le langage toohello que vous utilisez. Vérifiez à chaque fois ces remplacements :

   * Remplacez **INSERT-autorité-ici** avec nom hello du client hello dans lequel vous avez configuré votre application. Le format doit être https://login.microsoftonline.com/contoso.onmicrosoft.com. Cette valeur peut être copiée à partir de l’onglet du domaine hello dans Azure Active Directory Bonjour [portail Azure classic].
   * Remplacez **INSERT-RESOURCE-ID-ici** avec l’ID de client hello pour le service principal de votre application mobile. Vous pouvez obtenir l’ID de client à partir de hello **avancé** onglet sous **paramètres Azure Active Directory** dans le portail de hello.
   * Remplacez **INSERT-CLIENT-ID-ici** avec l’ID de client hello copié à partir de l’application cliente native de hello.
   * Remplacez **INSERT-REDIRECT-URI-ici** avec de votre site */.auth/login/done* point de terminaison, à l’aide du schéma HTTPS de hello. Cette valeur doit être similaire trop*https://contoso.azurewebsites.net/.auth/login/done*.

**Objective-C**:

    #import <ADALiOS/ADAuthenticationContext.h>
    #import <ADALiOS/ADAuthenticationSettings.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*))completionBlock;
    {
        NSString *authority = @"INSERT-AUTHORITY-HERE";
        NSString *resourceId = @"INSERT-RESOURCE-ID-HERE";
        NSString *clientId = @"INSERT-CLIENT-ID-HERE";
        NSURL *redirectUri = [[NSURL alloc]initWithString:@"INSERT-REDIRECT-URI-HERE"];
        ADAuthenticationError *error;
        ADAuthenticationContext *authContext = [ADAuthenticationContext authenticationContextWithAuthority:authority error:&error];
        authContext.parentController = parent;
        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:resourceId
                                     clientId:clientId
                                  redirectUri:redirectUri
                              completionBlock:^(ADAuthenticationResult *result) {
                                  if (result.status != AD_SUCCEEDED)
                                  {
                                      completionBlock(nil, result.error);;
                                  }
                                  else
                                  {
                                      NSDictionary *payload = @{
                                                                @"access_token" : result.tokenCacheStoreItem.accessToken
                                                                };
                                      [client loginWithProvider:@"aad" token:payload completion:completionBlock];
                                  }
                              }];
    }


**Swift**:

    // add hello following imports tooyour bridging header:
    //        #import <ADALiOS/ADAuthenticationContext.h>
    //        #import <ADALiOS/ADAuthenticationSettings.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let authority = "INSERT-AUTHORITY-HERE"
        let resourceId = "INSERT-RESOURCE-ID-HERE"
        let clientId = "INSERT-CLIENT-ID-HERE"
        let redirectUri = NSURL(string: "INSERT-REDIRECT-URI-HERE")
        var error: AutoreleasingUnsafeMutablePointer<ADAuthenticationError?> = nil
        let authContext = ADAuthenticationContext(authority: authority, error: error)
        authContext.parentController = parent
        ADAuthenticationSettings.sharedInstance().enableFullScreen = true
        authContext.acquireTokenWithResource(resourceId, clientId: clientId, redirectUri: redirectUri) { (result) in
                if result.status != AD_SUCCEEDED {
                    completion(nil, result.error)
                }
                else {
                    let payload: [String: String] = ["access_token": result.tokenCacheStoreItem.accessToken]
                    client.loginWithProvider("aad", token: payload, completion: completion)
                }
            }
    }

## <a name="facebook-sdk"></a>Comment : authentifier les utilisateurs avec hello SDK Facebook pour iOS
Vous pouvez utiliser hello SDK Facebook pour les utilisateurs iOS toosign dans votre application à l’aide de Facebook.  À l’aide d’une authentification de flux client est préférable toousing hello `loginWithProvider:completion:` (méthode).  l’authentification du client flux Hello fournit un aspect d’expérience utilisateur plus natif et permet une personnalisation supplémentaire.

1. Configurez votre serveur principal d’application mobile pour la connexion à Facebook à l’aide du [comment tooconfigure application de Service pour le compte de connexion Facebook] [ 9] didacticiel.
2. Installer hello SDK Facebook pour iOS en suivant hello [SDK Facebook pour iOS - mise en route] [ 10] documentation. Au lieu de créer une application, vous pouvez ajouter une inscription existante hello iOS plateforme tooyour.
3. Documentation de Facebook inclut du code Objective-C Bonjour délégué de l’application. Si vous utilisez **Swift**, vous pouvez utiliser hello suivant des traductions pour AppDelegate.swift :

        // Add hello following import tooyour bridging header:
        //        #import <FBSDKCoreKit/FBSDKCoreKit.h>

        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            FBSDKApplicationDelegate.sharedInstance().application(application, didFinishLaunchingWithOptions: launchOptions)
            // Add any custom logic here.
            return true
        }

        func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?, annotation: AnyObject?) -> Bool {
            let handled = FBSDKApplicationDelegate.sharedInstance().application(application, openURL: url, sourceApplication: sourceApplication, annotation: annotation)
            // Add any custom logic here.
            return handled
        }
4. En outre tooadding `FBSDKCoreKit.framework` tooyour de projet, ajoutez également une référence de trop`FBSDKLoginKit.framework` Bonjour identique.
5. Ajoutez hello après application de code tooyour, selon le langage toohello que vous utilisez.

**Objective-C**:

    #import <FBSDKLoginKit/FBSDKLoginKit.h>
    #import <FBSDKCoreKit/FBSDKAccessToken.h>
    // ...
    - (void) authenticate:(UIViewController*) parent
               completion:(void (^) (MSUser*, NSError*)) completionBlock;
    {        
        FBSDKLoginManager *loginManager = [[FBSDKLoginManager alloc] init];
        [loginManager
         logInWithReadPermissions: @[@"public_profile"]
         fromViewController:parent
         handler:^(FBSDKLoginManagerLoginResult *result, NSError *error) {
             if (error) {
                 completionBlock(nil, error);
             } else if (result.isCancelled) {
                 completionBlock(nil, error);
             } else {
                 NSDictionary *payload = @{
                                           @"access_token":result.token.tokenString
                                           };
                 [client loginWithProvider:@"facebook" token:payload completion:completionBlock];
             }
         }];
    }

**Swift**:

    // Add hello following imports tooyour bridging header:
    //        #import <FBSDKLoginKit/FBSDKLoginKit.h>
    //        #import <FBSDKCoreKit/FBSDKAccessToken.h>

    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let loginManager = FBSDKLoginManager()
        loginManager.logInWithReadPermissions(["public_profile"], fromViewController: parent) { (result, error) in
            if (error != nil) {
                completion(nil, error)
            }
            else if result.isCancelled {
                completion(nil, error)
            }
            else {
                let payload: [String: String] = ["access_token": result.token.tokenString]
                client.loginWithProvider("facebook", token: payload, completion: completion)
            }
        }
    }

## <a name="twitter-fabric"></a>Procédure : authentifier les utilisateurs avec Twitter Fabric pour iOS
Vous pouvez utiliser l’infrastructure pour les utilisateurs iOS toosign dans votre application à l’aide de Twitter. Flux de l’authentification du client est préférable toousing hello `loginWithProvider:completion:` de la méthode, il fournit un aspect d’expérience utilisateur plus natif et permet la personnalisation supplémentaire.

1. Configurer le service principal de votre application mobile pour la connexion à Twitter en suivant les hello [comment tooconfigure application de Service pour le compte de connexion Twitter](app-service-mobile-how-to-configure-twitter-authentication.md) didacticiel.
2. Ajouter l’ensemble fibre optique tooyour projet hello suivant [l’ensemble fibre optique pour iOS - mise en route] documentation et la configuration TwitterKit.

   > [!NOTE]
   > Par défaut, Fabric crée une application Twitter pour vous. Vous pouvez éviter la création d’une application en enregistrant hello clé de consommateur et Secret de consommateur que vous avez créé précédemment à l’aide de hello suivant des extraits de code.    Sinon, vous pouvez remplacer la clé de consommateur de hello et valeurs de question secrète du client, vous devez fournir les valeurs tooApp Service avec hello que vous consultez Bonjour [tableau de bord de l’ensemble fibre optique]. Si vous choisissez cette option, être vraiment tooset hello rappel URL tooa valeur d’espace réservé, tel que `https://<yoursitename>.azurewebsites.net/.auth/login/twitter/callback`.
   >
   >

    Si vous choisissez toouse secrets hello que vous avez créé précédemment, ajoutez hello suivant code tooyour délégué de l’application :

    **Objective-C**:

        #import <Fabric/Fabric.h>
        #import <TwitterKit/TwitterKit.h>
        // ...
        - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
        {
            [[Twitter sharedInstance] startWithConsumerKey:@"your_key" consumerSecret:@"your_secret"];
            [Fabric with:@[[Twitter class]]];
            // Add any custom logic here.
            return YES;
        }

    **Swift**:

        import Fabric
        import TwitterKit
        // ...
        func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject : AnyObject]?) -> Bool {
            Twitter.sharedInstance().startWithConsumerKey("your_key", consumerSecret: "your_secret")
            Fabric.with([Twitter.self])
            // Add any custom logic here.
            return true
        }
3. Ajoutez hello après application de code tooyour, selon le langage toohello que vous utilisez.

**Objective-C**:

    #import <TwitterKit/TwitterKit.h>
    // ...
    - (void)authenticate:(UIViewController*)parent completion:(void (^) (MSUser*, NSError*))completionBlock
    {
        [[Twitter sharedInstance] logInWithCompletion:^(TWTRSession *session, NSError *error) {
            if (session) {
                NSDictionary *payload = @{
                                            @"access_token":session.authToken,
                                            @"access_token_secret":session.authTokenSecret
                                        };
                [client loginWithProvider:@"twitter" token:payload completion:completionBlock];
            } else {
                completionBlock(nil, error);
            }
        }];
    }

**Swift**:

    import TwitterKit
    // ...
    func authenticate(parent: UIViewController, completion: (MSUser?, NSError?) -> Void) {
        let client = self.table!.client
        Twitter.sharedInstance().logInWithCompletion { session, error in
            if (session != nil) {
                let payload: [String: String] = ["access_token": session!.authToken, "access_token_secret": session!.authTokenSecret]
                client.loginWithProvider("twitter", token: payload, completion: completion)
            } else {
                completion(nil, error)
            }
        }
    }

## <a name="google-sdk"></a>Comment : authentifier les utilisateurs avec hello Google connectez-vous SDK pour iOS
Vous pouvez utiliser hello Google connectez-vous Kit de développement logiciel pour les utilisateurs iOS toosign dans votre application à l’aide d’un compte Google.  Google a récemment annoncé que les modifications des stratégies de sécurité tootheir OAuth.  Ces modifications de stratégie requiert utilisation hello du SDK Google Bonjour futures.

1. Configurer le service principal de votre application mobile pour la connexion à Google par hello suivant [comment tooconfigure application de Service pour le compte de connexion Google](app-service-mobile-how-to-configure-google-authentication.md) didacticiel.
2. Installer hello Google SDK pour iOS en suivant hello [Google Sign-In pour iOS - démarrer l’intégration](https://developers.google.com/identity/sign-in/ios/start-integrating) documentation. Vous pouvez ignorer la section de hello « S’authentifier avec un serveur principal ».
3. Ajouter hello suivant du délégué tooyour `signIn:didSignInForUser:withError:` méthode, selon le langage de toohello vous utilisez.

**Objective-C**:

        NSDictionary *payload = @{
                                  @"id_token":user.authentication.idToken,
                                  @"authorization_code":user.serverAuthCode
                                  };

        [client loginWithProvider:@"google" token:payload completion:^(MSUser *user, NSError *error) {
            // ...
        }];

**Swift**:

        let payload: [String: String] = ["id_token": user.authentication.idToken, "authorization_code": user.serverAuthCode]
        client.loginWithProvider("google", token: payload) { (user, error) in
            // ...
        }

1. Veillez à ajouter également hello suivant trop`application:didFinishLaunchingWithOptions:` dans votre application délégué, en remplaçant « SERVER_CLIENT_ID » avec hello même ID que vous avez utilisé tooconfigure du Service d’applications à l’étape 1.

**Objective-C**:

         [GIDSignIn sharedInstance].serverClientID = @"SERVER_CLIENT_ID";

 **Swift**:

        GIDSignIn.sharedInstance().serverClientID = "SERVER_CLIENT_ID"


1. Ajouter hello suite de l’application tooyour de code dans un UIViewController qui implémente hello `GIDSignInUIDelegate` protocole, selon le langage de toohello vous utilisez.  Vous êtes déconnecté avant le fait d’être connecté à nouveau, et bien que vous n’avez pas besoin tooenter vos informations d’identification à nouveau, vous voyez une boîte de dialogue de consentement.  Uniquement appeler cette méthode lorsque le jeton de session hello a expiré.

   **Objective-C**:

       #import <Google/SignIn.h>
       // ...
       - (void)authenticate
       {
               [GIDSignIn sharedInstance].uiDelegate = self;
               [[GIDSignIn sharedInstance] signOut];
               [[GIDSignIn sharedInstance] signIn];
        }

   **Swift**:

       // ...
       func authenticate() {
           GIDSignIn.sharedInstance().uiDelegate = self
           GIDSignIn.sharedInstance().signOut()
           GIDSignIn.sharedInstance().signIn()
       }

<!-- Anchors. -->

[What is Mobile Services]: #what-is
[Concepts]: #concepts
[Setup and Prerequisites]: #Setup
[How to: Create hello Mobile Services client]: #create-client
[How to: Create a table reference]: #table-reference
[How to: Query data from a mobile service]: #querying
[Filter returned data]: #filtering
[Sort returned data]: #sorting
[Return data in pages]: #paging
[Select specific columns]: #selecting
[How to: Bind data toohello user interface]: #binding
[How to: Insert data into a mobile service]: #inserting
[How to: Modify data in a mobile service]: #modifying
[How to: Authenticate users]: #authentication
[Cache authentication tokens]: #caching-tokens
[How to: Upload images and large files]: #blobs
[How to: Handle errors]: #errors
[How to: Design unit tests]: #unit-testing
[How to: Customize hello client]: #customizing
[Customize request headers]: #custom-headers
[Customize data type serialization]: #custom-serialization
[Next Steps]: #next-steps
[How to: Use MSQuery]: #query-object

<!-- Images. -->

<!-- URLs. -->
[démarrage rapide d’Azure Mobile Apps]: app-service-mobile-ios-get-started.md

[Add Mobile Services tooExisting App]: /develop/mobile/tutorials/get-started-data
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started-ios
[Validate and modify data in Mobile Services by using server scripts]: /develop/mobile/tutorials/validate-modify-and-augment-data-ios
[Mobile Services SDK]: https://go.microsoft.com/fwLink/p/?LinkID=266533
[Authentication]: /develop/mobile/tutorials/get-started-with-users-ios
[iOS SDK]: https://developer.apple.com/xcode

[Handling Expired Tokens]: http://go.microsoft.com/fwlink/p/?LinkId=301955
[Live Connect SDK]: http://go.microsoft.com/fwlink/p/?LinkId=301960
[Permissions]: http://msdn.microsoft.com/library/windowsazure/jj193161.aspx
[Service-side Authorization]: mobile-services-javascript-backend-service-side-authorization.md
[Use scripts tooauthorize users]: /develop/mobile/tutorials/authorize-users-in-scripts-ios
[le schéma dynamique]: http://go.microsoft.com/fwlink/p/?LinkId=296271
[How to: access custom parameters]: /develop/mobile/how-to-guides/work-with-server-scripts#access-headers
[Create a table]: http://msdn.microsoft.com/library/windowsazure/jj193162.aspx
[NSDictionary object]: http://go.microsoft.com/fwlink/p/?LinkId=301965
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[CLI toomanage Mobile Services tables]: /cli/azure/get-started-with-az-cli2
[Conflict-Handler]: mobile-services-ios-handling-conflicts-offline-data.md#add-conflict-handling

[tableau de bord de l’ensemble fibre optique]: https://www.fabric.io/home
[l’ensemble fibre optique pour iOS - mise en route]: https://docs.fabric.io/ios/fabric/getting-started.html
[1]: https://github.com/Azure/azure-mobile-apps-ios-client/blob/master/README.md#ios-client-sdk
[2]: http://azure.github.io/azure-mobile-apps-ios-client/
[3]: https://msdn.microsoft.com/library/azure/dn495101.aspx
[4]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#tags
[5]: http://azure.github.io/azure-mobile-services/iOS/v3/Classes/MSClient.html#//api/name/invokeAPI:data:HTTPMethod:parameters:headers:completion:
[6]: https://github.com/Azure/azure-mobile-services/blob/master/sdk/iOS/src/MSError.h
[7]: app-service-mobile-how-to-configure-active-directory-authentication.md
[8]: ../active-directory/active-directory-devquickstarts-ios.md
[9]: app-service-mobile-how-to-configure-facebook-authentication.md
[10]: https://developers.facebook.com/docs/ios/getting-started
