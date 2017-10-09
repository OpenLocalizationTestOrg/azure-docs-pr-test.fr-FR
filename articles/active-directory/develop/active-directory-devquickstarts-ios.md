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
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="ad29b-103">Intégrer Azure AD à une application iOS</span><span class="sxs-lookup"><span data-stu-id="ad29b-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="ad29b-104">Un aperçu de hello de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/iOS) qui vous permet d’obtenir en cours d’exécution avec Azure Active Directory en quelques minutes !</span><span class="sxs-lookup"><span data-stu-id="ad29b-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="ad29b-105">portail des développeurs Hello vous guide tout au long des processus de hello l’inscription d’une application et l’intégration d’Azure AD dans votre code.</span><span class="sxs-lookup"><span data-stu-id="ad29b-105">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="ad29b-106">Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre locataire et d’un serveur principal qui peut accepter des jetons et effectuer une validation.</span><span class="sxs-lookup"><span data-stu-id="ad29b-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="ad29b-107">Azure Active Directory (Azure AD) fournit hello bibliothèque d’authentification Active Directory, ou la bibliothèque ADAL, pour les clients d’iOS qui doivent tooaccess des ressources protégées.</span><span class="sxs-lookup"><span data-stu-id="ad29b-107">Azure Active Directory (Azure AD) provides hello Active Directory Authentication Library, or ADAL, for iOS clients that need tooaccess protected resources.</span></span> <span data-ttu-id="ad29b-108">La bibliothèque ADAL simplifie hello que votre application utilise des jetons d’accès tooobtain.</span><span class="sxs-lookup"><span data-stu-id="ad29b-108">ADAL simplifies hello process that your app uses tooobtain access tokens.</span></span> <span data-ttu-id="ad29b-109">toodemonstrate facilement est, dans cet article nous générer une application de liste de tâches objectif C :</span><span class="sxs-lookup"><span data-stu-id="ad29b-109">toodemonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="ad29b-110">Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="ad29b-110">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="ad29b-111">recherche, dans un répertoire, d’utilisateurs correspondant à un alias donné ;</span><span class="sxs-lookup"><span data-stu-id="ad29b-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="ad29b-112">toobuild hello travail application complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="ad29b-112">toobuild hello complete working application, you need to:</span></span>

1. <span data-ttu-id="ad29b-113">inscrire votre application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="ad29b-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="ad29b-114">installer et configurer la bibliothèque ADAL ;</span><span class="sxs-lookup"><span data-stu-id="ad29b-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="ad29b-115">Utiliser des jetons tooget ADAL d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ad29b-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="ad29b-116">tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ad29b-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="ad29b-117">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="ad29b-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="ad29b-118">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ad29b-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="ad29b-119">Un aperçu de hello de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/iOS) qui vous permet d’obtenir en cours d’exécution auprès d’Azure AD en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ad29b-119">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="ad29b-120">portail des développeurs Hello vous guide tout au long des processus de hello l’inscription d’une application et l’intégration d’Azure AD dans votre code.</span><span class="sxs-lookup"><span data-stu-id="ad29b-120">hello developer portal guides you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="ad29b-121">Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre locataire et d’un serveur principal qui peut accepter des jetons et effectuer une validation.</span><span class="sxs-lookup"><span data-stu-id="ad29b-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="ad29b-122">1. Déterminer votre URI de redirection pour iOS</span><span class="sxs-lookup"><span data-stu-id="ad29b-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="ad29b-123">toosecurely démarrer vos applications dans certains scénarios d’authentification unique, vous devez créer un *URI de redirection* dans un format particulier.</span><span class="sxs-lookup"><span data-stu-id="ad29b-123">toosecurely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="ad29b-124">Une redirection URI est utilisé tooensure qui hello jetons toohello retour correct application demandé pour eux.</span><span class="sxs-lookup"><span data-stu-id="ad29b-124">A redirect URI is used tooensure that hello tokens return toohello correct application that asked for them.</span></span>


<span data-ttu-id="ad29b-125">format d’iOS Hello pour une redirection URI est :</span><span class="sxs-lookup"><span data-stu-id="ad29b-125">hello iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="ad29b-126">**aap-scheme** : il est enregistré dans votre projet XCode.</span><span class="sxs-lookup"><span data-stu-id="ad29b-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="ad29b-127">Cela permet aux autres applications de vous appeler.</span><span class="sxs-lookup"><span data-stu-id="ad29b-127">It is how other applications can call you.</span></span> <span data-ttu-id="ad29b-128">Vous trouverez cela sous Info.plist -> Types d’URL -> Identificateur d’URL.</span><span class="sxs-lookup"><span data-stu-id="ad29b-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="ad29b-129">Vous devez en créer une si vous n’en avez pas encore au moins une configurée.</span><span class="sxs-lookup"><span data-stu-id="ad29b-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="ad29b-130">**id d’offre groupée** -il s’agit de hello identificateur d’offre groupée se trouvant sous « identité » annule les paramètres de votre projet dans XCode.</span><span class="sxs-lookup"><span data-stu-id="ad29b-130">**bundle-id** - This is hello Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="ad29b-131">Voici un exemple de code de démarrage rapide : ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="ad29b-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-hello-directorysearcher-application"></a><span data-ttu-id="ad29b-132">2. Enregistrer l’application de DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="ad29b-132">2. Register hello DirectorySearcher application</span></span>
<span data-ttu-id="ad29b-133">tooset des jetons de tooget de votre application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess d’autorisation Azure AD Graph API :</span><span class="sxs-lookup"><span data-stu-id="ad29b-133">tooset up your app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="ad29b-134">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad29b-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ad29b-135">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="ad29b-135">On hello top bar, click your account.</span></span> <span data-ttu-id="ad29b-136">Sous hello **répertoire** , choisissez client Active Directory de hello où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="ad29b-136">Under hello **Directory** list, choose hello Active Directory tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="ad29b-137">Cliquez sur **plus Services** dans hello du volet de navigation de gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ad29b-137">Click **More Services** in hello leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ad29b-138">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ad29b-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ad29b-139">Suivez hello invite toocreate un nouveau **Application cliente Native**.</span><span class="sxs-lookup"><span data-stu-id="ad29b-139">Follow hello prompts toocreate a new **Native Client Application**.</span></span>
  * <span data-ttu-id="ad29b-140">Hello **nom** Hello application décrit utilisateurs tooend de votre application.</span><span class="sxs-lookup"><span data-stu-id="ad29b-140">hello **Name** of hello application describes your application tooend users.</span></span>
  * <span data-ttu-id="ad29b-141">Hello **Uri de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.</span><span class="sxs-lookup"><span data-stu-id="ad29b-141">hello **Redirect Uri** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span>  <span data-ttu-id="ad29b-142">Entrez une valeur qui est l’application de tooyour spécifique et basée sur les informations de URI de redirection précédentes hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-142">Enter a value that is specific tooyour application and is based on hello previous redirect URI information.</span></span>
6. <span data-ttu-id="ad29b-143">Une fois que vous avez terminé l’inscription de hello, Azure AD assigne à votre application un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="ad29b-143">After you've completed hello registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="ad29b-144">Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-144">You'll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="ad29b-145">À partir de hello **paramètres** page, sélectionnez **autorisations requises** , puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ad29b-145">From hello **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="ad29b-146">Sélectionnez **Microsoft Graph** comme hello API, puis ajoutez hello **les données d’annuaire en lecture** autorisation sous **autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="ad29b-146">Select **Microsoft Graph** as hello API, and then add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="ad29b-147">Cela configure votre hello de tooquery d’application API Azure AD Graph pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ad29b-147">This sets up your application tooquery hello Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="ad29b-148">3. Installer et configurer la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="ad29b-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="ad29b-149">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="ad29b-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="ad29b-150">Pour toocommunicate ADAL avec Azure AD, vous devez tooprovide avec des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="ad29b-150">For ADAL toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

1. <span data-ttu-id="ad29b-151">Commencez par ajouter la bibliothèque ADAL toohello DirectorySearcher projet à l’aide de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="ad29b-151">Begin by adding ADAL toohello DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="ad29b-152">Ajoutez hello suivant toothis podfile :</span><span class="sxs-lookup"><span data-stu-id="ad29b-152">Add hello following toothis podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="ad29b-153">Charger hello podfile à l’aide de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="ad29b-153">Now load hello podfile by using CocoaPods.</span></span> <span data-ttu-id="ad29b-154">Cette étape crée un espace de travail XCode que vous allez charger.</span><span class="sxs-lookup"><span data-stu-id="ad29b-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="ad29b-155">Dans le projet de démarrage rapide de hello, ouvrir le fichier .plist de hello `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="ad29b-155">In hello QuickStart project, open hello plist file `settings.plist`.</span></span>  <span data-ttu-id="ad29b-156">Remplacez les valeurs hello d’éléments hello dans hello section tooreflect hello les valeurs que vous avez entré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ad29b-156">Replace hello values of hello elements in hello section tooreflect hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="ad29b-157">Votre code fait référence à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="ad29b-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="ad29b-158">Hello `tenant` est domaine hello de votre client Azure AD, par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="ad29b-158">hello `tenant` is hello domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="ad29b-159">Hello `clientId` est l’ID de client hello de votre application que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-159">hello `clientId` is hello client ID of your application that you copied from hello portal.</span></span>
  * <span data-ttu-id="ad29b-160">Hello `redirectUri` est l’URL de redirection hello que vous avez enregistré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-160">hello `redirectUri` is hello redirect URL that you registered in hello portal.</span></span>

## <a name="4----use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="ad29b-161">4.    Utiliser des jetons tooget ADAL d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad29b-161">4.    Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="ad29b-162">Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que votre application a besoin d’un jeton d’accès, il appelle simplement un completionBlock `+(void) getToken : `, et la bibliothèque ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="ad29b-162">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="ad29b-163">Bonjour `QuickStart` projet, ouvrez `GraphAPICaller.m` et recherchez hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` commentaire haut hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-163">In hello `QuickStart` project, open `GraphAPICaller.m` and locate hello `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near hello top.</span></span>  <span data-ttu-id="ad29b-164">Il s’agit où vous transmettez des coordonnées de la bibliothèque ADAL hello via un CompletionBlock, toocommunicate avec Azure AD et lui indiquer comment les jetons toocache.</span><span class="sxs-lookup"><span data-stu-id="ad29b-164">This is where you pass ADAL hello coordinates through a CompletionBlock, toocommunicate with Azure AD, and tell it how toocache tokens.</span></span>

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

2. <span data-ttu-id="ad29b-165">Nous devons maintenant toouse ce jeton toosearch pour les utilisateurs dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-165">Now we need toouse this token toosearch for users in hello graph.</span></span> <span data-ttu-id="ad29b-166">Recherche hello `// TODO: implement SearchUsersList` commentaire.</span><span class="sxs-lookup"><span data-stu-id="ad29b-166">Find hello `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="ad29b-167">Cette méthode rend un tooquery toohello API Azure AD Graph de demande GET pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="ad29b-167">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="ad29b-168">tooquery hello Azure AD Graph API, vous devez tooinclude un access_token Bonjour `Authorization` en-tête de demande de hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-168">tooquery hello Azure AD Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request.</span></span> <span data-ttu-id="ad29b-169">C’est là où la bibliothèque ADAL entre en jeu.</span><span class="sxs-lookup"><span data-stu-id="ad29b-169">This is where ADAL comes in.</span></span>

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


3. <span data-ttu-id="ad29b-170">Lorsque votre application demande un jeton en appelant `getToken(...)`, la bibliothèque ADAL tente tooreturn un jeton sans demander hello pour les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="ad29b-170">When your app requests a token by calling `getToken(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="ad29b-171">Si la bibliothèque ADAL détermine que l’utilisateur hello doit toosign dans tooget un jeton, s’afficher une boîte de dialogue pour la connexion, collecter des informations d’identification de l’utilisateur hello et puis retourne un jeton après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="ad29b-171">If ADAL determines that hello user needs toosign in tooget a token, it will display a dialog box for sign-in, collect hello user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="ad29b-172">Si la bibliothèque ADAL n’est pas en mesure de tooreturn un jeton pour une raison quelconque, elle lève une `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="ad29b-172">If ADAL is not able tooreturn a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="ad29b-173">Hello `AuthenticationResult` objet contient un `tokenCacheStoreItem` objet qui peut être utilisé toocollect hello informations votre application.</span><span class="sxs-lookup"><span data-stu-id="ad29b-173">hello `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used toocollect hello information that your app may need.</span></span> <span data-ttu-id="ad29b-174">Bonjour démarrage rapide, `tokenCacheStoreItem` est toodetermine utilisé si l’authentification est déjà faite.</span><span class="sxs-lookup"><span data-stu-id="ad29b-174">In hello QuickStart, `tokenCacheStoreItem` is used toodetermine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-hello-application"></a><span data-ttu-id="ad29b-175">5. Générer et exécuter l’application hello</span><span class="sxs-lookup"><span data-stu-id="ad29b-175">5. Build and run hello application</span></span>
<span data-ttu-id="ad29b-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="ad29b-176">Congratulations!</span></span> <span data-ttu-id="ad29b-177">Vous disposez maintenant d’une application iOS de travail qui peut authentifier les utilisateurs, en toute sécurité appeler des API Web à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ad29b-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="ad29b-178">Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ad29b-178">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="ad29b-179">Démarrez votre application de démarrage rapide, puis connectez-vous à l’aide de l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ad29b-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="ad29b-180">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="ad29b-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="ad29b-181">Fermez l’application hello et lancez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="ad29b-181">Close hello app, and then start it again.</span></span>  <span data-ttu-id="ad29b-182">Notez que la session de l’utilisateur hello reste intacte.</span><span class="sxs-lookup"><span data-stu-id="ad29b-182">Notice that hello user's session remains intact.</span></span>

<span data-ttu-id="ad29b-183">ADAL rend facile tooincorporate toutes ces fonctionnalités d’identité commune dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ad29b-183">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="ad29b-184">Il s’occupe de tout le travail dirty hello, tels que la gestion du cache, protocole prise en charge OAuth, afficher hello un toosign de l’interface utilisateur dans et l’actualisation des jetons expirés.</span><span class="sxs-lookup"><span data-stu-id="ad29b-184">It takes care of all hello dirty work for you, like cache management, OAuth protocol support, presenting hello user with a UI toosign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="ad29b-185">Vous devez vraiment tooknow est un simple appel d’API `getToken`.</span><span class="sxs-lookup"><span data-stu-id="ad29b-185">All you really need tooknow is a single API call, `getToken`.</span></span>

<span data-ttu-id="ad29b-186">Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni sur [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ad29b-186">For reference, hello completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="ad29b-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ad29b-187">Next steps</span></span>
<span data-ttu-id="ad29b-188">Vous pouvez maintenant déplacer sur les scénarios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="ad29b-188">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="ad29b-189">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="ad29b-189">You may want tootry:</span></span>

* [<span data-ttu-id="ad29b-190">Sécurisation d’une API web Node.js avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad29b-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="ad29b-191">En savoir plus [comment tooenable SSO inter-applications sur iOS à l’aide de la bibliothèque ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="ad29b-191">Learn [how tooenable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

