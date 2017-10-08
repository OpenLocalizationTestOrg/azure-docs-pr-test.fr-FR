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
# <a name="add-sign-in-tooan-ios-app-using-a-third-party-library-with-graph-api-using-hello-v20-endpoint"></a><span data-ttu-id="f06ad-103">Ajouter une application iOS de tooan connectez-vous à l’aide d’une bibliothèque tierce avec l’API Graph à l’aide du point de terminaison hello v2.0</span><span class="sxs-lookup"><span data-stu-id="f06ad-103">Add sign-in tooan iOS app using a third-party library with Graph API using hello v2.0 endpoint</span></span>
<span data-ttu-id="f06ad-104">plateforme d’identité Microsoft Hello utilise des normes ouvertes telles que OAuth2 et OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="f06ad-104">hello Microsoft identity platform uses open standards such as OAuth2 and OpenID Connect.</span></span> <span data-ttu-id="f06ad-105">Les développeurs peuvent utiliser n’importe quelle bibliothèque qu’ils souhaitent toointegrate avec nos services.</span><span class="sxs-lookup"><span data-stu-id="f06ad-105">Developers can use any library they want toointegrate with our services.</span></span> <span data-ttu-id="f06ad-106">les développeurs de toohelp utilisent notre plateforme avec d’autres bibliothèques, nous avons comment écrit quelques procédures pas à pas, comme cette une toodemonstrate plateforme d’identité tooconnect toohello Microsoft tooconfigure des bibliothèques tierces.</span><span class="sxs-lookup"><span data-stu-id="f06ad-106">toohelp developers use our platform with other libraries, we've written a few walkthroughs like this one toodemonstrate how tooconfigure third-party libraries tooconnect toohello Microsoft identity platform.</span></span> <span data-ttu-id="f06ad-107">La plupart des bibliothèques qui implémentent [les spécifications hello RFC6749 OAuth2](https://tools.ietf.org/html/rfc6749) peut se connecter de plateforme d’identité Microsoft toohello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-107">Most libraries that implement [hello RFC6749 OAuth2 spec](https://tools.ietf.org/html/rfc6749) can connect toohello Microsoft identity platform.</span></span>

<span data-ttu-id="f06ad-108">Avec l’application hello qui crée de cette procédure pas à pas, les utilisateurs peuvent se connecter tootheir organisation et puis rechercher d’autres utilisateurs dans leur organisation à l’aide de l’API Graph de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-108">With hello application that this walkthrough creates, users can sign in tootheir organization and then search for others in their organization by using hello Graph API.</span></span>

<span data-ttu-id="f06ad-109">Si vous êtes de nouveau tooOAuth2 ou OpenID Connect, une grande partie de cet exemple de configuration peut ne pas effectuer tooyou de sens.</span><span class="sxs-lookup"><span data-stu-id="f06ad-109">If you're new tooOAuth2 or OpenID Connect, much of this sample configuration may not make sense tooyou.</span></span> <span data-ttu-id="f06ad-110">Nous vous recommandons de lire [Protocoles v2.0 - Flux du Code d’autorisation OAuth 2.0](active-directory-v2-protocols-oauth-code.md) pour l’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="f06ad-110">We recommend that you read  [v2.0 Protocols - OAuth 2.0 Authorization Code Flow](active-directory-v2-protocols-oauth-code.md) for background.</span></span>

> [!NOTE]
> <span data-ttu-id="f06ad-111">Certaines fonctionnalités de notre plateforme qui n’ont pas une expression dans hello OAuth2 ou OpenID Connect des normes, telles que l’accès conditionnel et de gestion des stratégies Intune, requièrent vous toouse open source bibliothèques d’identité Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="f06ad-111">Some features of our platform that do have an expression in hello OAuth2 or OpenID Connect standards, such as Conditional Access and Intune policy management, require you toouse our open source Microsoft Azure Identity Libraries.</span></span>
> 
> 

<span data-ttu-id="f06ad-112">point de terminaison Hello v2.0 ne prend pas en charge toutes les fonctionnalités et scénarios d’Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f06ad-112">hello v2.0 endpoint does not support all Azure Active Directory scenarios and features.</span></span>

> [!NOTE]
> <span data-ttu-id="f06ad-113">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="f06ad-113">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="download-code-from-github"></a><span data-ttu-id="f06ad-114">Télécharger le code à partir de GitHub</span><span class="sxs-lookup"><span data-stu-id="f06ad-114">Download code from GitHub</span></span>
<span data-ttu-id="f06ad-115">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span><span class="sxs-lookup"><span data-stu-id="f06ad-115">hello code for this tutorial is maintained [on GitHub](https://github.com/Azure-Samples/active-directory-ios-native-nxoauth2-v2).</span></span>  <span data-ttu-id="f06ad-116">toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="f06ad-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

```
git clone --branch skeleton git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

<span data-ttu-id="f06ad-117">Vous pouvez également simplement télécharger l’exemple hello et démarrer immédiatement :</span><span class="sxs-lookup"><span data-stu-id="f06ad-117">You can also just download hello sample and get started right away:</span></span>

```
git clone git@github.com:Azure-Samples/active-directory-ios-native-nxoauth2-v2.git
```

## <a name="register-an-app"></a><span data-ttu-id="f06ad-118">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="f06ad-118">Register an app</span></span>
<span data-ttu-id="f06ad-119">Créer une application à hello [portail de l’enregistrement d’Application](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez hello étapes détaillées à [comment tooregister une application avec un point de terminaison hello v2.0](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="f06ad-119">Create a new app at hello [Application registration portal](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow hello detailed steps at  [How tooregister an app with hello v2.0 endpoint](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="f06ad-120">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="f06ad-120">Make sure to:</span></span>

* <span data-ttu-id="f06ad-121">Hello de copie **Id d’Application** qui est attribué tooyour application, car vous en aurez besoin plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="f06ad-121">Copy hello **Application Id** that's assigned tooyour app because you'll need it soon.</span></span>
* <span data-ttu-id="f06ad-122">Ajouter hello **Mobile** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="f06ad-122">Add hello **Mobile** platform for your app.</span></span>
* <span data-ttu-id="f06ad-123">Hello de copie **URI de redirection** à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-123">Copy hello **Redirect URI** from hello portal.</span></span> <span data-ttu-id="f06ad-124">Vous devez utiliser la valeur par défaut hello `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="f06ad-124">You must use hello default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="download-hello-third-party-nxoauth2-library-and-create-a-workspace"></a><span data-ttu-id="f06ad-125">Télécharger la bibliothèque de NXOAuth2 hello tierce et créer un espace de travail</span><span class="sxs-lookup"><span data-stu-id="f06ad-125">Download hello third-party NXOAuth2 library and create a workspace</span></span>
<span data-ttu-id="f06ad-126">Pour cette procédure pas à pas, vous allez utiliser hello OAuth2Client à partir de GitHub, qui est une bibliothèque OAuth2 pour Mac OS X et iOS (/ Cocoa et/Cocoa touch).</span><span class="sxs-lookup"><span data-stu-id="f06ad-126">For this walkthrough, you will use hello OAuth2Client from GitHub, which is an OAuth2 library for Mac OS X and iOS (Cocoa and Cocoa touch).</span></span> <span data-ttu-id="f06ad-127">Cette bibliothèque est basée sur le projet 10 des spécifications de OAuth2 hello. Il implémente le profil d’application native hello et prend en charge le point de terminaison hello d’autorisation d’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-127">This library is based on draft 10 of hello OAuth2 spec. It implements hello native application profile and supports hello authorization endpoint of hello user.</span></span> <span data-ttu-id="f06ad-128">Il s’agit de tous les éléments de hello, vous devez toointegrate avec la plateforme d’identité Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-128">These are all hello things you'll need toointegrate with hello Microsoft identity platform.</span></span>

### <a name="add-hello-library-tooyour-project-by-using-cocoapods"></a><span data-ttu-id="f06ad-129">Ajouter un projet de bibliothèque de tooyour hello à l’aide de CocoaPods</span><span class="sxs-lookup"><span data-stu-id="f06ad-129">Add hello library tooyour project by using CocoaPods</span></span>
<span data-ttu-id="f06ad-130">CocoaPods est un gestionnaire de dépendances pour les projets Xcode.</span><span class="sxs-lookup"><span data-stu-id="f06ad-130">CocoaPods is a dependency manager for Xcode projects.</span></span> <span data-ttu-id="f06ad-131">Il gère automatiquement les étapes d’installation précédente hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-131">It manages hello previous installation steps automatically.</span></span>

```
$ vi Podfile
```
1. <span data-ttu-id="f06ad-132">Ajoutez hello suivant toothis podfile :</span><span class="sxs-lookup"><span data-stu-id="f06ad-132">Add hello following toothis podfile:</span></span>
   
    ```
     platform :ios, '8.0'
   
     target 'QuickStart' do
   
     pod 'NXOAuth2Client'
   
     end
    ```
2. <span data-ttu-id="f06ad-133">Podfile hello de charge à l’aide de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="f06ad-133">Load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="f06ad-134">Cette opération crée un nouvel espace de travail Xcode que vous allez charger.</span><span class="sxs-lookup"><span data-stu-id="f06ad-134">This will create a new Xcode workspace that you will load.</span></span>
   
    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

## <a name="explore-hello-structure-of-hello-project"></a><span data-ttu-id="f06ad-135">Explorer la structure hello du projet de hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-135">Explore hello structure of hello project</span></span>
<span data-ttu-id="f06ad-136">Hello suivant la structure est définie pour notre projet dans le squelette de hello :</span><span class="sxs-lookup"><span data-stu-id="f06ad-136">hello following structure is set up for our project in hello skeleton:</span></span>

* <span data-ttu-id="f06ad-137">Une vue principale avec une recherche de noms UPN</span><span class="sxs-lookup"><span data-stu-id="f06ad-137">A Master View with a UPN Search</span></span>
* <span data-ttu-id="f06ad-138">Un affichage des détails sur l’utilisateur sélectionné de hello pour les données de salutation</span><span class="sxs-lookup"><span data-stu-id="f06ad-138">A Detail View for hello data about hello selected user</span></span>
* <span data-ttu-id="f06ad-139">Une vue de la connexion où un utilisateur peut se connecter dans le graphique de hello toohello application tooquery</span><span class="sxs-lookup"><span data-stu-id="f06ad-139">A Login View where a user can sign in toohello app tooquery hello graph</span></span>

<span data-ttu-id="f06ad-140">Il déplace des fichiers toovarious dans l’authentification de squelette tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-140">We will move toovarious files in hello skeleton tooadd authentication.</span></span> <span data-ttu-id="f06ad-141">Autres parties de code hello, tel que le code de visual hello, ne concernent pas tooidentity mais sont fournies pour vous.</span><span class="sxs-lookup"><span data-stu-id="f06ad-141">Other parts of hello code, such as hello visual code, do not pertain tooidentity but are provided for you.</span></span>

## <a name="set-up-hello-settingsplst-file-in-hello-library"></a><span data-ttu-id="f06ad-142">Configurer le fichier settings.plst de hello dans la bibliothèque de hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-142">Set up hello settings.plst file in hello library</span></span>
* <span data-ttu-id="f06ad-143">Dans le projet de démarrage rapide de hello, ouvrez hello `settings.plist` fichier.</span><span class="sxs-lookup"><span data-stu-id="f06ad-143">In hello QuickStart project, open hello `settings.plist` file.</span></span> <span data-ttu-id="f06ad-144">Remplacez les valeurs hello d’éléments hello dans hello section tooreflect hello les valeurs que vous avez utilisé dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f06ad-144">Replace hello values of hello elements in hello section tooreflect hello values that you used in hello Azure portal.</span></span> <span data-ttu-id="f06ad-145">Votre code fait référence à ces valeurs chaque fois qu’il utilise hello bibliothèque d’authentification Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f06ad-145">Your code will reference these values whenever it uses hello Active Directory Authentication Library.</span></span>
  * <span data-ttu-id="f06ad-146">Hello `clientId` est l’ID de client hello de votre application que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-146">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="f06ad-147">Hello `redirectUri` est URL de redirection hello ce portail hello fourni.</span><span class="sxs-lookup"><span data-stu-id="f06ad-147">hello `redirectUri` is hello redirect URL that hello portal provided.</span></span>

## <a name="set-up-hello-nxoauth2client-library-in-your-loginviewcontroller"></a><span data-ttu-id="f06ad-148">Configurer la bibliothèque de NXOAuth2Client hello dans votre LoginViewController</span><span class="sxs-lookup"><span data-stu-id="f06ad-148">Set up hello NXOAuth2Client library in your LoginViewController</span></span>
<span data-ttu-id="f06ad-149">la bibliothèque de NXOAuth2Client Hello requiert certains tooget valeurs configuré.</span><span class="sxs-lookup"><span data-stu-id="f06ad-149">hello NXOAuth2Client library requires some values tooget set up.</span></span> <span data-ttu-id="f06ad-150">Après avoir effectué cette tâche, vous pouvez utiliser Bonjour toocall jeton acquis Bonjour API Graph.</span><span class="sxs-lookup"><span data-stu-id="f06ad-150">After you complete that task, you can use hello acquired token toocall hello Graph API.</span></span> <span data-ttu-id="f06ad-151">Étant donné que `LoginView` sera appelée dès que nous devons tooauthenticate, il est judicieux tooput les valeurs de configuration dans le fichier de toothat.</span><span class="sxs-lookup"><span data-stu-id="f06ad-151">Because `LoginView` will be called any time we need tooauthenticate, it makes sense tooput configuration values in toothat file.</span></span>

* <span data-ttu-id="f06ad-152">Nous allons ajouter certains toohello valeurs `LoginViewController.m` de contexte du fichier tooset hello pour l’authentification et d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="f06ad-152">Let's add some values toohello  `LoginViewController.m` file tooset hello context for authentication and authorization.</span></span> <span data-ttu-id="f06ad-153">Pour plus d’informations sur les valeurs hello suivent les code hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-153">Details about hello values follow hello code.</span></span>
  
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

<span data-ttu-id="f06ad-154">Examinons plus d’informations sur le code de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-154">Let's look at details about hello code.</span></span>

<span data-ttu-id="f06ad-155">première chaîne de Hello est pour `scopes`.</span><span class="sxs-lookup"><span data-stu-id="f06ad-155">hello first string is for `scopes`.</span></span>  <span data-ttu-id="f06ad-156">Hello `User.Read` valeur vous permet de profil de base hello tooread Hello utilisateur connecté.</span><span class="sxs-lookup"><span data-stu-id="f06ad-156">hello `User.Read` value allows you tooread hello basic profile of hello signed in user.</span></span>

<span data-ttu-id="f06ad-157">Plus d’informations sur toutes les étendues disponibles hello à [étendues d’autorisation Microsoft Graph](https://graph.microsoft.io/docs/authorization/permission_scopes).</span><span class="sxs-lookup"><span data-stu-id="f06ad-157">You can learn more about all hello available scopes at [Microsoft Graph permission scopes](https://graph.microsoft.io/docs/authorization/permission_scopes).</span></span>

<span data-ttu-id="f06ad-158">Pour `authURL`, `loginURL`, `bhh`, et `tokenURL`, vous devez utiliser les valeurs hello fournis précédemment.</span><span class="sxs-lookup"><span data-stu-id="f06ad-158">For `authURL`, `loginURL`, `bhh`, and `tokenURL`, you should use hello values provided previously.</span></span> <span data-ttu-id="f06ad-159">Si vous utilisez ouvrir la source de hello bibliothèques d’identité Microsoft Azure, nous extraire ces données vers le bas pour vous à l’aide de notre point de terminaison de métadonnées.</span><span class="sxs-lookup"><span data-stu-id="f06ad-159">If you use hello open source Microsoft Azure Identity Libraries, we pull this data down for you by using our metadata endpoint.</span></span> <span data-ttu-id="f06ad-160">Nous avons travail hello d’extraction de ces valeurs pour vous.</span><span class="sxs-lookup"><span data-stu-id="f06ad-160">We've done hello hard work of extracting these values for you.</span></span>

<span data-ttu-id="f06ad-161">Hello `keychain` valeur est le conteneur hello hello NXOAuth2Client bibliothèque utilisera toocreate un toostore trousseau vos jetons.</span><span class="sxs-lookup"><span data-stu-id="f06ad-161">hello `keychain` value is hello container that hello NXOAuth2Client library will use toocreate a keychain toostore your tokens.</span></span> <span data-ttu-id="f06ad-162">Si vous souhaitez que tooget-session unique (SSO) entre plusieurs applications, vous pouvez spécifier hello même trousseau dans chacun de vos applications et utiliser ce trousseau dans vos droits Xcode hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-162">If you'd like tooget single sign-on (SSO) across numerous apps, you can specify hello same keychain in each of your applications and request hello use of that keychain in your Xcode entitlements.</span></span> <span data-ttu-id="f06ad-163">Cela est expliqué dans hello documentation Apple.</span><span class="sxs-lookup"><span data-stu-id="f06ad-163">This is explained in hello Apple documentation.</span></span>

<span data-ttu-id="f06ad-164">autres Hello ces valeurs toouse requis hello bibliothèque et créer des emplacements pour vous contexte de toohello toocarry valeurs.</span><span class="sxs-lookup"><span data-stu-id="f06ad-164">hello rest of these values are required toouse hello library and create places for you toocarry values toohello context.</span></span>

### <a name="create-a-url-cache"></a><span data-ttu-id="f06ad-165">Créer un cache d’URL</span><span class="sxs-lookup"><span data-stu-id="f06ad-165">Create a URL cache</span></span>
<span data-ttu-id="f06ad-166">À l’intérieur de `(void)viewDidLoad()`, qui est toujours appelée après le chargée de la vue de hello, un cache pour une utilisation primes hello de code suivant.</span><span class="sxs-lookup"><span data-stu-id="f06ad-166">Inside `(void)viewDidLoad()`, which is always called after hello view is loaded, hello following code primes a cache for our use.</span></span>

<span data-ttu-id="f06ad-167">Ajoutez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="f06ad-167">Add hello following code:</span></span>

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

### <a name="create-a-webview-for-sign-in"></a><span data-ttu-id="f06ad-168">Créer une WebView pour la connexion</span><span class="sxs-lookup"><span data-stu-id="f06ad-168">Create a WebView for sign-in</span></span>
<span data-ttu-id="f06ad-169">Un affichage Web peut inviter l’utilisateur hello autres facteurs tels que le message texte SMS (si configuré) ou erreur messages toohello utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f06ad-169">A WebView can prompt hello user for additional factors like SMS text message (if configured) or return error messages toohello user.</span></span> <span data-ttu-id="f06ad-170">Vous allez définir ici des hello WebView et puis plus tard écriture hello code toohandle hello rappels qui se produira Bonjour WebView à partir des services d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-170">Here you'll set up hello WebView and then later write hello code toohandle hello callbacks that will happen in hello WebView from hello identity services.</span></span>

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

### <a name="override-hello-webview-methods-toohandle-authentication"></a><span data-ttu-id="f06ad-171">Remplacer l’authentification de hello WebView méthodes toohandle</span><span class="sxs-lookup"><span data-stu-id="f06ad-171">Override hello WebView methods toohandle authentication</span></span>
<span data-ttu-id="f06ad-172">tootell hello WebView que se passe-t-il lorsqu’un utilisateur doit toosign dans comme indiqué précédemment, vous pouvez coller hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="f06ad-172">tootell hello WebView what happens when a user needs toosign in as discussed previously, you can paste hello following code.</span></span>

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

### <a name="write-code-toohandle-hello-result-of-hello-oauth2-request"></a><span data-ttu-id="f06ad-173">Écrire du code toohandle hello de résultats de requête de OAuth2 hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-173">Write code toohandle hello result of hello OAuth2 request</span></span>
<span data-ttu-id="f06ad-174">Hello de code suivant gère redirectURL hello qui renvoie à partir de hello WebView.</span><span class="sxs-lookup"><span data-stu-id="f06ad-174">hello following code will handle hello redirectURL that returns from hello WebView.</span></span> <span data-ttu-id="f06ad-175">Si l’authentification a échoué, code de hello tentera à nouveau.</span><span class="sxs-lookup"><span data-stu-id="f06ad-175">If authentication wasn't successful, hello code will try again.</span></span> <span data-ttu-id="f06ad-176">Pendant ce temps, la bibliothèque de hello fournira erreur hello que vous pouvez voir dans la console hello ou gérer de façon asynchrone.</span><span class="sxs-lookup"><span data-stu-id="f06ad-176">Meanwhile, hello library will provide hello error that you can see in hello console or handle asynchronously.</span></span>

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

### <a name="set-up-hello-oauth-context-called-account-store"></a><span data-ttu-id="f06ad-177">Configurer hello contexte OAuth (appelé compte magasin)</span><span class="sxs-lookup"><span data-stu-id="f06ad-177">Set up hello OAuth Context (called account store)</span></span>
<span data-ttu-id="f06ad-178">Ici, vous pouvez appeler `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` sur le magasin de comptes partagés hello pour chaque service que vous souhaitez hello application toobe en mesure de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="f06ad-178">Here you can call `-[NXOAuth2AccountStore setClientID:secret:authorizationURL:tokenURL:redirectURL:forAccountType:]` on hello shared account store for each service that you want hello application toobe able tooaccess.</span></span> <span data-ttu-id="f06ad-179">type de compte Hello est une chaîne qui est utilisée comme identificateur pour un certain service.</span><span class="sxs-lookup"><span data-stu-id="f06ad-179">hello account type is a string that is used as an identifier for a certain service.</span></span> <span data-ttu-id="f06ad-180">Étant donné que vous accédez à l’API Graph de hello, code de hello fait référence tooit comme `"myGraphService"`.</span><span class="sxs-lookup"><span data-stu-id="f06ad-180">Because you are accessing hello Graph API, hello code refers tooit as `"myGraphService"`.</span></span> <span data-ttu-id="f06ad-181">Ensuite, vous configurer un observateur qui vous indique lorsque quelque chose change avec le jeton de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-181">You then set up an observer that will tell you when anything changes with hello token.</span></span> <span data-ttu-id="f06ad-182">Après avoir obtenu le jeton de hello, vous retournez toohello arrière de hello utilisateur `masterView`.</span><span class="sxs-lookup"><span data-stu-id="f06ad-182">After you get hello token, you return hello user back toohello `masterView`.</span></span>

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

## <a name="set-up-hello-master-view-toosearch-and-display-hello-users-from-hello-graph-api"></a><span data-ttu-id="f06ad-183">Définir hello mode Masque toosearch et afficher les utilisateurs hello hello API Graph</span><span class="sxs-lookup"><span data-stu-id="f06ad-183">Set up hello Master View toosearch and display hello users from hello Graph API</span></span>
<span data-ttu-id="f06ad-184">Une application principale-View-Controller (MVC) qui affiche hello a retourné des données dans la grille de hello est abordée dans cette procédure pas à pas hello et plusieurs didacticiels en ligne expliquent comment toobuild une.</span><span class="sxs-lookup"><span data-stu-id="f06ad-184">A Master-View-Controller (MVC) app that displays hello returned data in hello grid is beyond hello scope of this walkthrough, and many online tutorials explain how toobuild one.</span></span> <span data-ttu-id="f06ad-185">Ce code est dans le fichier squelette de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-185">All this code is in hello skeleton file.</span></span> <span data-ttu-id="f06ad-186">Toutefois, vous devez toodeal avec quelques éléments dans cette application MVC :</span><span class="sxs-lookup"><span data-stu-id="f06ad-186">However, you do need toodeal with a few things in this MVC application:</span></span>

* <span data-ttu-id="f06ad-187">Intercept lorsqu’un utilisateur tape quelque chose dans le champ de recherche hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-187">Intercept when a user types something in hello search field</span></span>
* <span data-ttu-id="f06ad-188">Fournir un objet de toohello de données précédent MasterView afin d’afficher les résultats de hello dans la grille de hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-188">Provide an object of data back toohello MasterView so it can display hello results in hello grid</span></span>

<span data-ttu-id="f06ad-189">Nous effectuerons ces actions ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f06ad-189">We'll do those below.</span></span>

### <a name="add-a-check-toosee-if-youre-logged-in"></a><span data-ttu-id="f06ad-190">Ajouter un toosee à cocher si vous êtes connecté</span><span class="sxs-lookup"><span data-stu-id="f06ad-190">Add a check toosee if you're logged in</span></span>
<span data-ttu-id="f06ad-191">application Hello ne peu si hello utilisateur n’est pas connecté, il est toocheck active si un jeton est déjà dans le cache de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-191">hello application does little if hello user is not signed in, so it's smart toocheck if there is already a token in hello cache.</span></span> <span data-ttu-id="f06ad-192">Si non, vous redirigez toohello LoginView pour hello utilisateur toosign dans.</span><span class="sxs-lookup"><span data-stu-id="f06ad-192">If not, you redirect toohello LoginView for hello user toosign in.</span></span> <span data-ttu-id="f06ad-193">Si vous vous souvenez, hello meilleure manière toodo actions lors de la charge d’une vue est toouse hello `viewDidLoad()` méthode nous fournit par Apple.</span><span class="sxs-lookup"><span data-stu-id="f06ad-193">If you recall, hello best way toodo actions when a view loads is toouse hello `viewDidLoad()` method that Apple provides us.</span></span>

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

### <a name="update-hello-table-view-when-data-is-received"></a><span data-ttu-id="f06ad-194">Mettre à jour hello vue Table lors de la réception de données</span><span class="sxs-lookup"><span data-stu-id="f06ad-194">Update hello Table View when data is received</span></span>
<span data-ttu-id="f06ad-195">Hello API Graph renvoie des données, vous devez les données de salutation toodisplay.</span><span class="sxs-lookup"><span data-stu-id="f06ad-195">When hello Graph API returns data, you need toodisplay hello data.</span></span> <span data-ttu-id="f06ad-196">Par souci de simplicité, voici la table de hello tooupdate de code hello tous les.</span><span class="sxs-lookup"><span data-stu-id="f06ad-196">For simplicity, here is all hello code tooupdate hello table.</span></span> <span data-ttu-id="f06ad-197">Vous pouvez simplement Coller les valeurs hello dans votre code réutilisable MVC.</span><span class="sxs-lookup"><span data-stu-id="f06ad-197">You can just paste hello right values in your MVC boilerplate code.</span></span>

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

### <a name="provide-a-way-toocall-hello-graph-api-when-someone-types-in-hello-search-field"></a><span data-ttu-id="f06ad-198">Fournir un Bonjour toocall de façon API Graph lorsqu’un utilisateur tape dans le champ de recherche hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-198">Provide a way toocall hello Graph API when someone types in hello search field</span></span>
<span data-ttu-id="f06ad-199">Lorsqu’un utilisateur tape une recherche dans la zone de hello, vous devez tooshove sur toohello API Graph.</span><span class="sxs-lookup"><span data-stu-id="f06ad-199">When a user types a search in hello box, you need tooshove that over toohello Graph API.</span></span> <span data-ttu-id="f06ad-200">Hello `GraphAPICaller` (classe), que vous allez générer Bonjour suivant de code, la fonctionnalité de recherche hello sépare présentation de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-200">hello `GraphAPICaller` class, which you will build in hello following code, separates hello lookup functionality from hello presentation.</span></span> <span data-ttu-id="f06ad-201">Pour l’instant, nous allons écrire le code hello qui alimente les toohello de caractères recherche API Graph.</span><span class="sxs-lookup"><span data-stu-id="f06ad-201">For now, let's write hello code that feeds any search characters toohello Graph API.</span></span> <span data-ttu-id="f06ad-202">Pour ce faire, nous en fournissant une méthode appelée `lookupInGraph`, qui accepte la chaîne hello que nous souhaitons toosearch pour.</span><span class="sxs-lookup"><span data-stu-id="f06ad-202">We do this by providing a method called `lookupInGraph`, which takes hello string that we want toosearch for.</span></span>

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

## <a name="write-a-helper-class-tooaccess-hello-graph-api"></a><span data-ttu-id="f06ad-203">Écrire un Bonjour de tooaccess de classe d’assistance Graph API</span><span class="sxs-lookup"><span data-stu-id="f06ad-203">Write a Helper class tooaccess hello Graph API</span></span>
<span data-ttu-id="f06ad-204">Il s’agit de noyau de hello de notre application.</span><span class="sxs-lookup"><span data-stu-id="f06ad-204">This is hello core of our application.</span></span> <span data-ttu-id="f06ad-205">Alors que le reste de hello a été insertion de code dans le modèle MVC par défaut hello auprès d’Apple, vous ici graphique de code tooquery hello comme utilisateur de hello types et puis de renvoyer ces données.</span><span class="sxs-lookup"><span data-stu-id="f06ad-205">Whereas hello rest was inserting code in hello default MVC pattern from Apple, here you write code tooquery hello graph as hello user types and then return that data.</span></span> <span data-ttu-id="f06ad-206">Voici le code de hello et suit une explication détaillée.</span><span class="sxs-lookup"><span data-stu-id="f06ad-206">Here's hello code, and a detailed explanation follows it.</span></span>

### <a name="create-a-new-objective-c-header-file"></a><span data-ttu-id="f06ad-207">Créer un nouveau fichier d’en-tête Objective C</span><span class="sxs-lookup"><span data-stu-id="f06ad-207">Create a new Objective C header file</span></span>
<span data-ttu-id="f06ad-208">Nom de fichier hello `GraphAPICaller.h`et ajoutez hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="f06ad-208">Name hello file `GraphAPICaller.h`, and add hello following code.</span></span>

```objc
@interface GraphAPICaller : NSObject<NSURLConnectionDataDelegate>

+(void) searchUserList:(NSString*)searchString
       completionBlock:(void (^) (NSMutableArray*, NSError* error))completionBlock;

@end
```

<span data-ttu-id="f06ad-209">Vous voyez ici qu’une méthode prend une chaîne et retourne un completionBlock.</span><span class="sxs-lookup"><span data-stu-id="f06ad-209">Here you see that a specified method takes a string and returns a completionBlock.</span></span> <span data-ttu-id="f06ad-210">Cette completionBlock, comme vous l’avez peut-être deviné, met à jour la table de hello en fournissant un objet avec des données remplie en temps réel comme hello recherche de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f06ad-210">This completionBlock, as you may have guessed, will update hello table by providing an object with populated data in real time as hello user searches.</span></span>

### <a name="create-a-new-objective-c-file"></a><span data-ttu-id="f06ad-211">Créer un nouveau fichier Objective C</span><span class="sxs-lookup"><span data-stu-id="f06ad-211">Create a new Objective C file</span></span>
<span data-ttu-id="f06ad-212">Nom de fichier hello `GraphAPICaller.m`et ajoutez hello suivant de méthode.</span><span class="sxs-lookup"><span data-stu-id="f06ad-212">Name hello file `GraphAPICaller.m`, and add hello following method.</span></span>

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

<span data-ttu-id="f06ad-213">Examinons cette méthode en détail.</span><span class="sxs-lookup"><span data-stu-id="f06ad-213">Let's go through this method in detail.</span></span>

<span data-ttu-id="f06ad-214">core Hello de ce code est Bonjour `NXOAuth2Request`, méthode qui prend des paramètres de hello que vous avez déjà définies dans le fichier de settings.plist hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-214">hello core of this code is in hello `NXOAuth2Request`, method which takes hello parameters that you've already defined in hello settings.plist file.</span></span>

<span data-ttu-id="f06ad-215">première étape de Hello est appel d’API Graph right tooconstruct hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-215">hello first step is tooconstruct hello right Graph API call.</span></span> <span data-ttu-id="f06ad-216">Étant donné que vous appelez `/users`, vous spécifiez qui en l’ajoutant toohello des ressources de l’API Graph en même temps que la version de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-216">Because you are calling `/users`, you specify that by appending it toohello Graph API resource along with hello version.</span></span> <span data-ttu-id="f06ad-217">Rend sens tooput dans un fichier de paramètres externe, car ceux-ci peuvent modifier que hello API évolue.</span><span class="sxs-lookup"><span data-stu-id="f06ad-217">It makes sense tooput these in an external settings file because these can change as hello API evolves.</span></span>

```objc
NSString *graphURL = [NSString stringWithFormat:@"%@%@/users", data.graphApiUrlString, data.apiversion];
```

<span data-ttu-id="f06ad-218">Ensuite, vous devez toospecify les paramètres que vous fournissez également appel d’API Graph toohello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-218">Next, you need toospecify parameters that you will also provide toohello Graph API call.</span></span> <span data-ttu-id="f06ad-219">Il s’agit de *très important* que vous ne placez pas les paramètres hello dans le point de terminaison de ressource hello car qui est monté pour tous les caractères conforme non-URI lors de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="f06ad-219">It is *very important* that you do not put hello parameters in hello resource endpoint because that is scrubbed for all non-URI conforming characters at runtime.</span></span> <span data-ttu-id="f06ad-220">Tout code de requête doit être fourni dans les paramètres de hello.</span><span class="sxs-lookup"><span data-stu-id="f06ad-220">All query code must be provided in hello parameters.</span></span>

```objc

NSDictionary* params = [self convertParamsToDictionary:searchString];
```

<span data-ttu-id="f06ad-221">Vous remarquerez peut-être que cela appelle une méthode `convertParamsToDictionary` que vous n’avez pas encore écrite.</span><span class="sxs-lookup"><span data-stu-id="f06ad-221">You might notice this calls a `convertParamsToDictionary` method that you haven't written yet.</span></span> <span data-ttu-id="f06ad-222">Nous allons faire maintenant à fin hello du fichier de hello :</span><span class="sxs-lookup"><span data-stu-id="f06ad-222">Let's do so now at hello end of hello file:</span></span>

```objc
+(NSDictionary*) convertParamsToDictionary:(NSString*)searchString
{
    NSMutableDictionary* dictionary = [[NSMutableDictionary alloc]init];

        NSString *query = [NSString stringWithFormat:@"startswith(givenName, '%@')", searchString];

           [dictionary setValue:query forKey:@"$filter"];



    return dictionary;
}

```
<span data-ttu-id="f06ad-223">Ensuite, nous allons utiliser hello `NXOAuth2Request` méthode tooget données sauvegarder à partir de hello API au format JSON.</span><span class="sxs-lookup"><span data-stu-id="f06ad-223">Next, let's use hello `NXOAuth2Request` method tooget data back from hello API in JSON format.</span></span>

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

<span data-ttu-id="f06ad-224">Enfin, nous allons voir comment vous retournez hello données toohello MasterViewController.</span><span class="sxs-lookup"><span data-stu-id="f06ad-224">Finally, let's look at how you return hello data toohello MasterViewController.</span></span> <span data-ttu-id="f06ad-225">les données de salutation retourne comme sérialisé et doit toobe désérialisé et chargées dans un objet qui hello MainViewController peut consommer.</span><span class="sxs-lookup"><span data-stu-id="f06ad-225">hello data returns as serialized and needs toobe deserialized and loaded in an object that hello MainViewController can consume.</span></span> <span data-ttu-id="f06ad-226">Pour cela, le squelette de hello a un `User.m/h` fichier qui crée un objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f06ad-226">For this purpose, hello skeleton has a `User.m/h` file that creates a User object.</span></span> <span data-ttu-id="f06ad-227">Vous devez remplir avec les informations du graphique de hello de cet objet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f06ad-227">You populate that User object with information from hello graph.</span></span>

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


## <a name="run-hello-sample"></a><span data-ttu-id="f06ad-228">Exécuter l’exemple hello</span><span class="sxs-lookup"><span data-stu-id="f06ad-228">Run hello sample</span></span>
<span data-ttu-id="f06ad-229">Si vous avez utilisé le squelette de hello ou suivi, ainsi que la procédure pas à pas hello votre application doit maintenant s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="f06ad-229">If you've used hello skeleton or followed along with hello walkthrough your application should now run.</span></span> <span data-ttu-id="f06ad-230">Démarrer le simulateur de hello et cliquez sur **connectez-vous** application hello de toouse.</span><span class="sxs-lookup"><span data-stu-id="f06ad-230">Start hello simulator and click **Sign in** toouse hello application.</span></span>

## <a name="get-security-updates-for-our-product"></a><span data-ttu-id="f06ad-231">Obtenir des mises à jour de sécurité pour notre produit</span><span class="sxs-lookup"><span data-stu-id="f06ad-231">Get security updates for our product</span></span>
<span data-ttu-id="f06ad-232">Nous vous conseillons de notifications tooget les incidents de sécurité se produire en visitant hello [TechCenter sur la sécurité](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="f06ad-232">We encourage you tooget notifications of when security incidents occur by visiting hello [Security TechCenter](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

