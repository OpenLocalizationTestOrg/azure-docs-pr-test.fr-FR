---
title: aaaIntegrate Azure AD dans une application iOS | Documents Microsoft
description: "Comment toobuild une application iOS qui s’intègre à Azure AD pour se connecter et d’appels Azure AD protégé API à l’aide d’OAuth."
services: active-directory
documentationcenter: ios
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: 42303177-9566-48ed-8abb-279fcf1e6ddb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 6e05745b2b2b122995dcba896ab0f2ed32509e3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a>Intégrer Azure AD à une application iOS
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> Un aperçu de hello de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/iOS) qui vous permet d’obtenir en cours d’exécution avec Azure Active Directory en quelques minutes !  portail des développeurs Hello vous guide tout au long des processus de hello l’inscription d’une application et l’intégration d’Azure AD dans votre code.  Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre locataire et d’un serveur principal qui peut accepter des jetons et effectuer une validation. 
> 
> 

Azure Active Directory (Azure AD) fournit hello bibliothèque d’authentification Active Directory, ou la bibliothèque ADAL, pour les clients d’iOS qui doivent tooaccess des ressources protégées. La bibliothèque ADAL simplifie hello que votre application utilise des jetons d’accès tooobtain. toodemonstrate facilement est, dans cet article nous générer une application de liste de tâches objectif C :

* Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).
* recherche, dans un répertoire, d’utilisateurs correspondant à un alias donné ;

toobuild hello travail application complète, vous devez :

1. inscrire votre application auprès d’Azure AD ;
2. installer et configurer la bibliothèque ADAL ;
3. Utiliser des jetons tooget ADAL d’Azure AD.

tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip). Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application. Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).


> [!TIP]
> Un aperçu de hello de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/iOS) qui vous permet d’obtenir en cours d’exécution auprès d’Azure AD en quelques minutes. portail des développeurs Hello vous guide tout au long des processus de hello l’inscription d’une application et l’intégration d’Azure AD dans votre code. Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre locataire et d’un serveur principal qui peut accepter des jetons et effectuer une validation. 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a>1. Déterminer votre URI de redirection pour iOS
toosecurely démarrer vos applications dans certains scénarios d’authentification unique, vous devez créer un *URI de redirection* dans un format particulier. Une redirection URI est utilisé tooensure qui hello jetons toohello retour correct application demandé pour eux.


format d’iOS Hello pour une redirection URI est :

```
<app-scheme>://<bundle-id>
```

* **aap-scheme** : il est enregistré dans votre projet XCode. Cela permet aux autres applications de vous appeler. Vous trouverez cela sous Info.plist -> Types d’URL -> Identificateur d’URL. Vous devez en créer une si vous n’en avez pas encore au moins une configurée.
* **id d’offre groupée** -il s’agit de hello identificateur d’offre groupée se trouvant sous « identité » annule les paramètres de votre projet dans XCode.

Voici un exemple de code de démarrage rapide : ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***

## <a name="2-register-hello-directorysearcher-application"></a>2. Enregistrer l’application de DirectorySearcher hello
tooset des jetons de tooget de votre application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess d’autorisation Azure AD Graph API :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur la barre supérieure de hello, cliquez sur votre compte. Sous hello **répertoire** , choisissez client Active Directory de hello où vous souhaitez tooregister votre application.
3. Cliquez sur **plus Services** dans hello du volet de navigation de gauche, puis sélectionnez **Azure Active Directory**.
4. Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.
5. Suivez hello invite toocreate un nouveau **Application cliente Native**.
  * Hello **nom** Hello application décrit utilisateurs tooend de votre application.
  * Hello **Uri de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.  Entrez une valeur qui est l’application de tooyour spécifique et basée sur les informations de URI de redirection précédentes hello.
6. Une fois que vous avez terminé l’inscription de hello, Azure AD assigne à votre application un ID d’application unique.  Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.
7. À partir de hello **paramètres** page, sélectionnez **autorisations requises** , puis sélectionnez **ajouter**. Sélectionnez **Microsoft Graph** comme hello API, puis ajoutez hello **les données d’annuaire en lecture** autorisation sous **autorisations déléguées**.  Cela configure votre hello de tooquery d’application API Azure AD Graph pour les utilisateurs.

## <a name="3-install-and-configure-adal"></a>3. Installer et configurer la bibliothèque ADAL
Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.  Pour toocommunicate ADAL avec Azure AD, vous devez tooprovide avec des informations sur l’inscription de votre application.

1. Commencez par ajouter la bibliothèque ADAL toohello DirectorySearcher projet à l’aide de CocoaPods.

    ```
    $ vi Podfile
    ```
2. Ajoutez hello suivant toothis podfile :

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. Charger hello podfile à l’aide de CocoaPods. Cette étape crée un espace de travail XCode que vous allez charger.

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. Dans le projet de démarrage rapide de hello, ouvrir le fichier .plist de hello `settings.plist`.  Remplacez les valeurs hello d’éléments hello dans hello section tooreflect hello les valeurs que vous avez entré dans hello portail Azure. Votre code fait référence à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.
  * Hello `tenant` est domaine hello de votre client Azure AD, par exemple, contoso.onmicrosoft.com.
  * Hello `clientId` est l’ID de client hello de votre application que vous avez copié à partir du portail de hello.
  * Hello `redirectUri` est l’URL de redirection hello que vous avez enregistré dans le portail de hello.

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a>4.    Utiliser des jetons tooget ADAL d’Azure AD
Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que votre application a besoin d’un jeton d’accès, il appelle simplement un completionBlock `+(void) getToken : `, et la bibliothèque ADAL hello rest.  

1. Bonjour `QuickStart` projet, ouvrez `GraphAPICaller.m` et recherchez hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` commentaire haut hello.  Il s’agit où vous transmettez des coordonnées de la bibliothèque ADAL hello via un CompletionBlock, toocommunicate avec Azure AD et lui indiquer comment les jetons toocache.

    ```ObjC
    +(void) getToken : (BOOL) clearCache
               parent:(UIViewController*) parent
    completionHandler:(void (^) (NSString*, NSError*))completionBlock;
    {
        AppData* data = [AppData getInstance];
        if(data.userItem){
            completionBlock(data.userItem.accessToken, nil);
            return;
        }

        ADAuthenticationError *error;
        authContext = [ADAuthenticationContext authenticationContextWithAuthority:data.authority error:&error];
        authContext.parentController = parent;
        NSURL *redirectUri = [[NSURL alloc]initWithString:data.redirectUriString];

        [ADAuthenticationSettings sharedInstance].enableFullScreen = YES;
        [authContext acquireTokenWithResource:data.resourceId
                                     clientId:data.clientId
                                  redirectUri:redirectUri
                               promptBehavior:AD_PROMPT_AUTO
                                       userId:data.userItem.userInformation.userId
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy toodisplay hello correct mobile UX. You most likely won't need it in your code.
                             completionBlock:^(ADAuthenticationResult *result) {

                                  if (result.status != AD_SUCCEEDED)
                                  {
                                     completionBlock(nil, result.error);
                                  }
                                  else
                                  {
                                      data.userItem = result.tokenCacheStoreItem;
                                      completionBlock(result.tokenCacheStoreItem.accessToken, nil);
                                  }
                             }];
    }

    ```

2. Nous devons maintenant toouse ce jeton toosearch pour les utilisateurs dans le graphique de hello. Recherche hello `// TODO: implement SearchUsersList` commentaire. Cette méthode rend un tooquery toohello API Azure AD Graph de demande GET pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.  tooquery hello Azure AD Graph API, vous devez tooinclude un access_token Bonjour `Authorization` en-tête de demande de hello. C’est là où la bibliothèque ADAL entre en jeu.

    ```ObjC
    +(void) searchUserList:(NSString*)searchString
                    parent:(UIViewController*) parent
          completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
    {
        if (!loadedApplicationSettings)
       {
            [self readApplicationSettings];
        }
        
        AppData* data = [AppData getInstance];

        NSString *graphURL = [NSString stringWithFormat:@"%@%@/users?api-version=%@&$filter=startswith(userPrincipalName, '%@')", data.taskWebApiUrlString, data.tenant, data.apiversion, searchString];

        [self craftRequest:[self.class trimString:graphURL]
                    parent:parent
         completionHandler:^(NSMutableURLRequest *request, NSError *error) {

             if (error != nil)
             {
                 completionBlock(nil, error);
             }
             else
             {

                 NSOperationQueue *queue = [[NSOperationQueue alloc]init];

                 [NSURLConnection sendAsynchronousRequest:request queue:queue completionHandler:^(NSURLResponse *response, NSData *data, NSError *error) {

                     if (error == nil && data != nil){

                         NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:data options:0 error:nil];

                         // We can grab hello JSON node at hello top tooget our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by hello key name being "value". It really is hello name of the
                         // first node. :-)

                         // Each object is a key value pair
                         NSDictionary *keyValuePairs;
                         NSMutableArray* Users = [[NSMutableArray alloc]init];

                         for(int i =0; i < graphDataArray.count; i++)
                         {
                             keyValuePairs = [graphDataArray objectAtIndex:i];

                             User *s = [[User alloc]init];
                             s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                             s.name =[keyValuePairs valueForKey:@"givenName"];

                             [Users addObject:s];
                         }

                         completionBlock(Users, nil);
                     }
                     else
                     {
                         completionBlock(nil, error);
                     }

                }];
             }
         }];

    }

    ```


3. Lorsque votre application demande un jeton en appelant `getToken(...)`, la bibliothèque ADAL tente tooreturn un jeton sans demander hello pour les informations d’identification.  Si la bibliothèque ADAL détermine que l’utilisateur hello doit toosign dans tooget un jeton, s’afficher une boîte de dialogue pour la connexion, collecter des informations d’identification de l’utilisateur hello et puis retourne un jeton après une authentification réussie.  Si la bibliothèque ADAL n’est pas en mesure de tooreturn un jeton pour une raison quelconque, elle lève une `AdalException`.

> [!Note] 
> Hello `AuthenticationResult` objet contient un `tokenCacheStoreItem` objet qui peut être utilisé toocollect hello informations votre application. Bonjour démarrage rapide, `tokenCacheStoreItem` est toodetermine utilisé si l’authentification est déjà faite.
>
>

## <a name="5-build-and-run-hello-application"></a>5. Générer et exécuter l’application hello
Félicitations ! Vous disposez maintenant d’une application iOS de travail qui peut authentifier les utilisateurs, en toute sécurité appeler des API Web à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur de hello.  Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.  Démarrez votre application de démarrage rapide, puis connectez-vous à l’aide de l’un de ces utilisateurs.  Recherchez d’autres utilisateurs en fonction de leur UPN.  Fermez l’application hello et lancez à nouveau.  Notez que la session de l’utilisateur hello reste intacte.

ADAL rend facile tooincorporate toutes ces fonctionnalités d’identité commune dans votre application.  Il s’occupe de tout le travail dirty hello, tels que la gestion du cache, protocole prise en charge OAuth, afficher hello un toosign de l’interface utilisateur dans et l’actualisation des jetons expirés.  Vous devez vraiment tooknow est un simple appel d’API `getToken`.

Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni sur [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).  

## <a name="next-steps"></a>Étapes suivantes
Vous pouvez maintenant déplacer sur les scénarios de tooadditional.  Vous souhaiterez peut-être tootry :

* [Sécurisation d’une API web Node.js avec Azure AD](active-directory-devquickstarts-webapi-nodejs.md)
* En savoir plus [comment tooenable SSO inter-applications sur iOS à l’aide de la bibliothèque ADAL](active-directory-sso-ios.md)  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

