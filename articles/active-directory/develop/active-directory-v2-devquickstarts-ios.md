---
title: "à l’aide d’aaaAdd tooan connexion iOS application hello point de terminaison Azure AD v2.0 | Documents Microsoft"
description: "Comment toobuild une application iOS qui se connecte aux utilisateurs avec les deux compte personnel de Microsoft et comptes professionnels ou scolaires à l’aide des bibliothèques tierces."
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: fd3603c0-42f7-438c-87b5-a52d20d6344b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 01/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: a384062e6e4bd398a2b12318800728e627e05c32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a>Ajouter une application iOS de tooan connectez-vous à l’aide d’une bibliothèque tierce avec l’API Graph à l’aide du point de terminaison hello v2.0
plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect. Les développeurs peuvent utiliser n’importe quelle bibliothèque qu’ils souhaitent toointegrate avec nos services. les développeurs de toohelp utilisent notre plateforme avec d’autres bibliothèques, nous avons comment écrit quelques procédures pas à pas, comme cette une toodemonstrate plateforme d’identité tooconnect toohello Microsoft tooconfigure des bibliothèques tierces. La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) peut se connecter de plateforme d’identité Microsoft toohello.

Avec l’application hello qui crée de cette procédure pas à pas, les utilisateurs peuvent se connecter tootheir organisation et puis rechercher d’autres utilisateurs dans leur organisation à l’aide de l’API Graph de hello.

Si vous êtes de nouveau tooOAuth2 ou OpenID Connect, une grande partie de cet exemple de configuration peut ne pas effectuer tooyou de sens. Nous vous recommandons de lire [Protocoles v2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md) pour l’arrière-plan.

> [!NOTE]
> Certaines fonctionnalités de notre plateforme qui n’ont pas une expression dans hello OAuth2 ou OpenID Connect des normes, telles que l’accès conditionnel et de gestion des stratégies Intune, requièrent vous toouse open source bibliothèques d’identité Microsoft Azure.
> 
> 

point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory.

> [!NOTE]
> toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).
> 
> 

## <a name="download-code-from-github"></a>Télécharger le code à partir de GitHub
code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).  toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou un clone hello squelette :

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

Vous pouvez également simplement télécharger l’exemple hello et démarrer immédiatement :

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a>Inscription d’une application
Créer une application à hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez hello étapes détaillées à [comment tooregister une application avec un point de terminaison hello v2.0](active-directory-v2-app-registration.md).  Veillez à respecter les points suivants :

* Hello de copie **Id d’Application** qui est attribué tooyour application, car vous en aurez besoin plus rapidement.
* Ajouter hello **Mobile** plate-forme pour votre application.
* Hello de copie **URI de redirection** à partir du portail de hello. Vous devez utiliser la valeur par défaut hello `urn:ietf:wg:oauth:2.0:oob`.

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a>Télécharger la bibliothèque de NXOAuth2 hello tierce et créer un espace de travail
Pour cette procédure pas à pas, vous allez utiliser hello OAuth2Client à partir de GitHub, qui est une bibliothèque OAuth2 pour Mac OS X et iOS (/ Cocoa et/Cocoa touch). Cette bibliothèque est basée sur le projet 10 des spécifications de OAuth2 hello. Il implémente le profil d’application native hello et prend en charge le point de terminaison hello d’autorisation d’utilisateur de hello. Il s’agit de tous les éléments de hello, vous devez toointegrate avec la plateforme d’identité Microsoft hello.

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a>Ajouter un projet de bibliothèque de tooyour hello à l’aide de CocoaPods
CocoaPods est un gestionnaire de dépendances pour les projets Xcode. Il gère automatiquement les étapes d’installation précédente hello.

```
$ vi Podfile
```
1. Ajoutez hello suivant toothis podfile :
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. Podfile hello de charge à l’aide de CocoaPods. Cette opération crée un nouvel espace de travail Xcode que vous allez charger.
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a>Explorer la structure hello du projet de hello
Hello suivant la structure est définie pour notre projet dans le squelette de hello :

* Une vue principale avec une recherche de noms UPN
* Un affichage des détails sur l’utilisateur sélectionné de hello pour les données de salutation
* Une vue de la connexion où un utilisateur peut se connecter dans le graphique de hello toohello application tooquery

Il déplace des fichiers toovarious dans l’authentification de squelette tooadd hello. Autres parties de code hello, tel que le code de visual hello, ne concernent pas tooidentity mais sont fournies pour vous.

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a>Configurer le fichier settings.plst de hello dans la bibliothèque de hello
* Dans le projet de démarrage rapide de hello, ouvrez hello `settings.plist` fichier. Remplacez les valeurs hello d’éléments hello dans hello section tooreflect hello les valeurs que vous avez utilisé dans hello portail Azure. Votre code fait référence à ces valeurs chaque fois qu’il utilise hello bibliothèque d’authentification Active Directory.
  * Hello `clientId` est l’ID de client hello de votre application que vous avez copié à partir du portail de hello.
  * Hello `redirectUri` est URL de redirection hello ce portail hello fourni.

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a>Configurer la bibliothèque de NXOAuth2Client hello dans votre LoginViewController
la bibliothèque de NXOAuth2Client Hello requiert certains tooget valeurs configuré. Après avoir effectué cette tâche, vous pouvez utiliser Bonjour toocall jeton acquis Bonjour API Graph. Étant donné que `LoginView` sera appelée dès que nous devons tooauthenticate, il est judicieux tooput les valeurs de configuration dans le fichier de toothat.

* Nous allons ajouter certains toohello valeurs `LoginViewController.m` de contexte du fichier tooset hello pour l’authentification et d’autorisation. Pour plus d’informations sur les valeurs hello suivent les code hello.
  
    ```objc
    NSString *scopes = @"openid offline_access User.Read";
    NSString *authURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/authorize";
    NSString *loginURL = @"https://login.microsoftonline.com/common/login";
    NSString *bhh = @"urn:ietf:wg:oauth:2.0:oob?code=";
    NSString *tokenURL = @"https://login.microsoftonline.com/common/oauth2/v2.0/token";
    NSString *keychain = @"com.microsoft.azureactivedirectory.samples.graph.QuickStart";
    static NSString * const kIDMOAuth2SuccessPagePrefix = @"session_state=";
    NSURL *myRequestedUrl;
    NSURL *myLoadedUrl;
    bool loginFlow = FALSE;
    bool isRequestBusy;
    NSURL *authcode;
    ```

Examinons plus d’informations sur le code de hello.

première chaîne de Hello est pour `scopes`.  Hello `User.Read` valeur vous permet de profil de base hello tooread Hello utilisateur connecté.

Plus d’informations sur toutes les étendues disponibles hello à [étendues d’autorisation Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).

Pour `authURL`, `loginURL`, `bhh`, et `tokenURL`, vous devez utiliser les valeurs hello fournis précédemment. Si vous utilisez ouvrir la source de hello bibliothèques d’identité Microsoft Azure, nous extraire ces données vers le bas pour vous à l’aide de notre point de terminaison de métadonnées. Nous avons travail hello d’extraction de ces valeurs pour vous.

Hello `keychain` valeur est le conteneur hello hello NXOAuth2Client bibliothèque utilisera toocreate un toostore trousseau vos jetons. Si vous souhaitez que tooget-session unique (SSO) entre plusieurs applications, vous pouvez spécifier hello même trousseau dans chacun de vos applications et utiliser ce trousseau dans vos droits Xcode hello. Cela est expliqué dans hello documentation Apple.

autres Hello ces valeurs toouse requis hello bibliothèque et créer des emplacements pour vous contexte de toohello toocarry valeurs.

### <a name="create-a-url-cache"></a>Créer un cache d’URL
À l’intérieur de `(void)viewDidLoad()`, qui est toujours appelée après le chargée de la vue de hello, un cache pour une utilisation primes hello de code suivant.

Ajoutez hello suivant de code :

```objc
- (void)viewDidLoad {
    [super viewDidLoad];
    self.loginView.delegate = self;
    [self setupOAuth2AccountStore];
    [self requestOAuth2Access];
    NSURLCache *URLCache = [[NSURLCache alloc] initWithMemoryCapacity:4 * 1024 * 1024
                                                         diskCapacity:20 * 1024 * 1024
                                                             diskPath:nil];
    [NSURLCache setSharedURLCache:URLCache];

}
```

### <a name="create-a-webview-for-sign-in"></a>Créer une WebView pour la connexion
Un affichage Web peut inviter l’utilisateur hello autres facteurs tels que le message texte SMS (si configuré) ou erreur messages toohello utilisateur. Vous allez définir ici des hello WebView et puis plus tard écriture hello code toohandle hello rappels qui se produira Bonjour WebView à partir des services d’identité hello.

```objc
-(void)requestOAuth2Access {
    //toosign in tooMicrosoft APIs using OAuth2, we must show an embedded browser (UIWebView)
    [[NXOAuth2AccountStore sharedStore] requestAccessToAccountWithType:@"myGraphService"
                                   withPreparedAuthorizationURLHandler:^(NSURL *preparedURL) {
                                       //navigate toohello URL returned by NXOAuth2Client

                                       NSURLRequest *r = [NSURLRequest requestWithURL:preparedURL];
                                       [self.loginView loadRequest:r];
                                   }];
}
```

### <a name="override-hello-webview-methods-toohandle-authentication"></a>Remplacer l’authentification de hello WebView méthodes toohandle
tootell hello WebView que se passe-t-il lorsqu’un utilisateur doit toosign dans comme indiqué précédemment, vous pouvez coller hello suivant de code.

```objc
- (void)resolveUsingUIWebView:(NSURL *)URL {

    // We get hello auth token from a redirect so we need toohandle that in hello webview.

    if (![NSThread isMainThread]) {
        [self performSelectorOnMainThread:@selector(resolveUsingUIWebView:) withObject:URL waitUntilDone:YES];
        return;
    }

    NSURLRequest *hostnameURLRequest = [NSURLRequest requestWithURL:URL cachePolicy:NSURLRequestUseProtocolCachePolicy timeoutInterval:10.0f];
    isRequestBusy = YES;
    [self.loginView loadRequest:hostnameURLRequest];

    NSLog(@"resolveUsingUIWebView ready (status: UNKNOWN, URL: %@)", self.loginView.request.URL);
}

- (BOOL)webView:(UIWebView *)webView shouldStartLoadWithRequest:(NSURLRequest *)request navigationType:(UIWebViewNavigationType)navigationType {

    NSLog(@"webView:shouldStartLoadWithRequest: %@ (%li)", request.URL, (long)navigationType);

    // hello webview is where all hello communication happens. Slightly complicated.

    myLoadedUrl = [webView.request mainDocumentURL];
    NSLog(@"***Loaded url: %@", myLoadedUrl);

    //if hello UIWebView is showing our authorization URL or consent URL, show hello UIWebView control
    if ([request.URL.absoluteString rangeOfString:authURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:loginURL options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = NO;
    } else if ([request.URL.absoluteString rangeOfString:bhh options:NSCaseInsensitiveSearch].location != NSNotFound) {
        //otherwise hide hello UIWebView, we've left hello authorization flow
        self.loginView.hidden = YES;
        [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }
    else {
        self.loginView.hidden = NO;
        //read hello Location from hello UIWebView, this is how Microsoft APIs is returning the
        //authentication code and relation information. This is controlled by hello redirect URL we chose toouse from Microsoft APIs
        //continue hello OAuth2 flow
       // [[NXOAuth2AccountStore sharedStore] handleRedirectURL:request.URL];
    }

    return YES;

}
```

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a>Écrire du code toohandle hello de résultats de requête de OAuth2 hello
Hello de code suivant gère redirectURL hello qui renvoie à partir de hello WebView. Si l’authentification a échoué, code de hello tentera à nouveau. Pendant ce temps, la bibliothèque de hello fournira erreur hello que vous pouvez voir dans la console hello ou gérer de façon asynchrone.

```objc
- (void)handleOAuth2AccessResult:(NSString *)accessResult {

    AppData* data = [AppData getInstance];

    //parse hello response for success or failure
     if (accessResult)
    //if success, complete hello OAuth2 flow by handling hello redirect URL and obtaining a token
     {
         [[NXOAuth2AccountStore sharedStore] handleRedirectURL:accessResult];
    } else {
        //start over
        [self requestOAuth2Access];
    }
}
```

### <a name="set-up-hello-oauth-context-called-account-store"></a>Configurer hello contexte OAuth (appelé compte magasin)
Ici, vous pouvez appeler `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` sur le magasin de comptes partagés hello pour chaque service que vous souhaitez hello application toobe en mesure de tooaccess. type de compte Hello est une chaîne qui est utilisée comme identificateur pour un certain service. Étant donné que vous accédez à l’API Graph de hello, code de hello fait référence tooit comme `"myGraphService"`. Ensuite, vous configurer un observateur qui vous indique lorsque quelque chose change avec le jeton de hello. Après avoir obtenu le jeton de hello, vous retournez toohello arrière de hello utilisateur `masterView`.

```objc
- (void)setupOAuth2AccountStore {


        AppData* data = [AppData getInstance];

    [[NXOAuth2AccountStore sharedStore] setClientID:data.clientId
                                             secret:data.secret
                                              scope:[NSSet setWithObject:scopes]
                                   authorizationURL:[NSURL URLWithString:authURL]
                                           tokenURL:[NSURL URLWithString:tokenURL]
                                        redirectURL:[NSURL URLWithString:data.redirectUriString]
                                      keyChainGroup: keychain
                                     forAccountType:@"myGraphService"];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreAccountsDidChangeNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      if (aNotification.userInfo) {
                                                          //account added, we have access
                                                          //we can now request protected data
                                                          NSLog(@"Success!! We have an access token.");
                                                          dispatch_async(dispatch_get_main_queue(),^ {

                                                              MasterViewController* masterViewController = [self.storyboard instantiateViewControllerWithIdentifier:@"masterView"];
                                                              [self.navigationController pushViewController:masterViewController animated:YES];
                                                          });
                                                      } else {
                                                          //account removed, we lost access
                                                      }
                                                  }];

    [[NSNotificationCenter defaultCenter] addObserverForName:NXOAuth2AccountStoreDidFailToRequestAccessNotification
                                                      object:[NXOAuth2AccountStore sharedStore]
                                                       queue:nil
                                                  usingBlock:^(NSNotification *aNotification) {
                                                      NSError *error = [aNotification.userInfo objectForKey:NXOAuth2AccountStoreErrorKey];
                                                      NSLog(@"Error!! %@", error.localizedDescription);
                                                  }];
}
```

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a>Définir hello mode Masque toosearch et afficher les utilisateurs hello hello API Graph
Une application principale-View-Controller (MVC) qui affiche hello a retourné des données dans la grille de hello est abordée dans cette procédure pas à pas hello et plusieurs didacticiels en ligne expliquent comment toobuild une. Ce code est dans le fichier squelette de hello. Toutefois, vous devez toodeal avec quelques éléments dans cette application MVC :

* Intercept lorsqu’un utilisateur tape quelque chose dans le champ de recherche hello
* Fournir un objet de toohello de données précédent MasterView afin d’afficher les résultats de hello dans la grille de hello

Nous effectuerons ces actions ci-dessous.

### <a name="add-a-check-toosee-if-youre-logged-in"></a>Ajouter un toosee à cocher si vous êtes connecté
application Hello ne peu si hello utilisateur n’est pas connecté, il est toocheck active si un jeton est déjà dans le cache de hello. Si non, vous redirigez toohello LoginView pour hello utilisateur toosign dans. Si vous vous souvenez, hello meilleure manière toodo actions lors de la charge d’une vue est toouse hello `viewDidLoad()` méthode nous fournit par Apple.

```objc
- (void)viewDidLoad {
    [super viewDidLoad];


    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];

        if (accounts.count == 0) {

        dispatch_async(dispatch_get_main_queue(),^ {

            LoginViewController* userSelectController = [self.storyboard instantiateViewControllerWithIdentifier:@"LoginUserView"];
            [self.navigationController pushViewController:userSelectController animated:YES];
        });
        }
```

### <a name="update-hello-table-view-when-data-is-received"></a>Mettre à jour hello vue Table lors de la réception de données
Hello API Graph renvoie des données, vous devez les données de salutation toodisplay. Par souci de simplicité, voici la table de hello tooupdate de code hello tous les. Vous pouvez simplement Coller les valeurs hello dans votre code réutilisable MVC.

```objc
#pragma mark - Table View

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {

        return [upnArray count];
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"TaskPrototypeCell" forIndexPath:indexPath];

    if ( cell == nil ) {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleDefault reuseIdentifier:@"TaskPrototypeCell"];
    }

    User *user = nil;
     user = [upnArray objectAtIndex:indexPath.row];


    // Configure hello cell
    cell.textLabel.text = user.name;
    [cell setAccessoryType:UITableViewCellAccessoryDisclosureIndicator];

    return cell;
}

```

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a>Fournir un Bonjour toocall de façon API Graph lorsqu’un utilisateur tape dans le champ de recherche hello
Lorsqu’un utilisateur tape une recherche dans la zone de hello, vous devez tooshove sur toohello API Graph. Hello `GraphAPICaller` (classe), que vous allez générer Bonjour suivant de code, la fonctionnalité de recherche hello sépare présentation de hello. Pour l’instant, nous allons écrire le code hello qui alimente les toohello de caractères recherche API Graph. Pour ce faire, nous en fournissant une méthode appelée `lookupInGraph`, qui accepte la chaîne hello que nous souhaitons toosearch pour.

```objc

-(void)lookupInGraph:(NSString *)searchText {
if (searchText.length > 0) {

    };



        [GraphAPICaller searchUserList:searchText completionBlock:^(NSMutableArray* returnedUpns, NSError* error) {
            if (returnedUpns) {


                upnArray = returnedUpns;


            }
            else
            {
                UIAlertView *alertView = [[UIAlertView alloc]initWithTitle:nil message:[[NSString alloc]initWithFormat:@"Error : %@", error.localizedDescription] delegate:nil cancelButtonTitle:@"Retry" otherButtonTitles:@"Cancel", nil];

                [alertView setDelegate:self];

                dispatch_async(dispatch_get_main_queue(),^ {
                    [alertView show];
                });
            }


        }];


}
```

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a>Écrire un Bonjour de tooaccess de classe d’assistance Graph API
Il s’agit de noyau de hello de notre application. Alors que le reste de hello a été insertion de code dans le modèle MVC par défaut hello auprès d’Apple, vous ici graphique de code tooquery hello comme utilisateur de hello types et puis de renvoyer ces données. Voici le code de hello et suit une explication détaillée.

### <a name="create-a-new-objective-c-header-file"></a>Créer un nouveau fichier d’en-tête Objective C
Nom de fichier hello `GraphAPICaller.h`et ajoutez hello suivant de code.

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

Vous voyez ici qu’une méthode prend une chaîne et retourne un completionBlock. Cette completionBlock, comme vous l’avez peut-être deviné, met à jour la table de hello en fournissant un objet avec des données remplie en temps réel comme hello recherche de l’utilisateur.

### <a name="create-a-new-objective-c-file"></a>Créer un nouveau fichier Objective C
Nom de fichier hello `GraphAPICaller.m`et ajoutez hello suivant de méthode.

```objc
+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray* Users, NSError* error)) completionBlock
{
    if (!loadedApplicationSettings)
    {
        [self readApplicationSettings];
    }

    AppData* data = [AppData getInstance];

    NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];

    NXOAuth2AccountStore *store = [NXOAuth2AccountStore sharedStore];
    NSDictionary* params = [self convertParamsToDictionary:searchString];

    NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


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

```

Examinons cette méthode en détail.

core Hello de ce code est Bonjour `NXOAuth2Request`, méthode qui prend des paramètres de hello que vous avez déjà définies dans le fichier de settings.plist hello.

première étape de Hello est appel d’API Graph right tooconstruct hello. Étant donné que vous appelez `/users`, vous spécifiez qui en l’ajoutant toohello des ressources de l’API Graph en même temps que la version de hello. Rend sens tooput dans un fichier de paramètres externe, car ceux-ci peuvent modifier que hello API évolue.

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

Ensuite, vous devez toospecify les paramètres que vous fournissez également appel d’API Graph toohello. Il s’agit de *très important* que vous ne placez pas les paramètres hello dans le point de terminaison de ressource hello car qui est monté pour tous les caractères conforme non-URI lors de l’exécution. Tout code de requête doit être fourni dans les paramètres de hello.

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

Vous remarquerez peut-être que cela appelle une méthode `convertParamsToDictionary` que vous n’avez pas encore écrite. Nous allons faire maintenant à fin hello du fichier de hello :

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
Ensuite, nous allons utiliser hello `NXOAuth2Request` méthode tooget données sauvegarder à partir de hello API au format JSON.

```objc
NSArray *accounts = [store accountsWithAccountType:@"myGraphService"];
    [NXOAuth2Request performMethod:@"GET"
                        onResource:[NSURL URLWithString:graphURL]
                   usingParameters:params
                       withAccount:accounts[0]
               sendProgressHandler:^(unsigned long long bytesSend, unsigned long long bytesTotal) {
                   // e.g., update a progress indicator
               }
                   responseHandler:^(NSURLResponse *response, NSData *responseData, NSError *error) {
                       // Process hello response
                       if (responseData) {
                           NSError *error;
                           NSDictionary *dataReturned = [NSJSONSerialization JSONObjectWithData:responseData options:0 error:nil];
                           NSLog(@"Graph Response was: %@", dataReturned);

                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];
```

Enfin, nous allons voir comment vous retournez hello données toohello MasterViewController. les données de salutation retourne comme sérialisé et doit toobe désérialisé et chargées dans un objet qui hello MainViewController peut consommer. Pour cela, le squelette de hello a un `User.m/h` fichier qui crée un objet utilisateur. Vous devez remplir avec les informations du graphique de hello de cet objet utilisateur.

```objc
                           // We can grab hello top most JSON node tooget our graph data.
                           NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                           // Don't be thrown off by hello key name being "value". It really is hello name of the
                           // first node. :-)

                           //each object is a key value pair
                           NSDictionary *keyValuePairs;
                           NSMutableArray* Users = [[NSMutableArray alloc]init];

                           for(int i =0; i < graphDataArray.count; i++)
                           {
                               keyValuePairs = [graphDataArray objectAtIndex:i];

                               User *s = [[User alloc]init];
                               s.upn = [keyValuePairs valueForKey:@"userPrincipalName"];
                               s.name =[keyValuePairs valueForKey:@"displayName"];
                               s.mail =[keyValuePairs valueForKey:@"mail"];
                               s.businessPhones =[keyValuePairs valueForKey:@"businessPhones"];
                               s.mobilePhones =[keyValuePairs valueForKey:@"mobilePhone"];


                               [Users addObject:s];
```


## <a name="run-hello-sample"></a>Exécuter l’exemple hello
Si vous avez utilisé le squelette de hello ou suivi, ainsi que la procédure pas à pas hello votre application doit maintenant s’exécuter. Démarrer le simulateur de hello et cliquez sur **connectez-vous** application hello de toouse.

## <a name="get-security-updates-for-our-product"></a>Obtenir des mises à jour de sécurité pour notre produit
Nous vous conseillons de notifications tooget les incidents de sécurité se produire en visitant hello [TechCenter sur la sécurité](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.

