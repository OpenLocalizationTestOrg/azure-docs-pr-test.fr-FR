---
title: "Intégrer Azure AD à une application iOS | Microsoft Docs"
description: "Création d’une application iOS qui s’intègre à Azure AD pour la connexion et appelle des API protégées par Azure AD en utilisant OAuth."
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
ms.openlocfilehash: 57f465df99ac234466459b8031f61805d8334b59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-an-ios-app"></a><span data-ttu-id="71f31-103">Intégrer Azure AD à une application iOS</span><span class="sxs-lookup"><span data-stu-id="71f31-103">Integrate Azure AD into an iOS app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="71f31-104">Essayez la préversion de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/iOS) qui vous permet de devenir opérationnel avec Azure Active Directory en quelques minutes !</span><span class="sxs-lookup"><span data-stu-id="71f31-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure Active Directory in just a few minutes!</span></span>  <span data-ttu-id="71f31-105">Le portail des développeurs vous guide tout au long du processus d’inscription d’une application et d’intégration d’Azure AD à votre code.</span><span class="sxs-lookup"><span data-stu-id="71f31-105">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span>  <span data-ttu-id="71f31-106">Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre locataire et d’un serveur principal qui peut accepter des jetons et effectuer une validation.</span><span class="sxs-lookup"><span data-stu-id="71f31-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a backend that can accept tokens and perform validation.</span></span> 
> 
> 

<span data-ttu-id="71f31-107">Pour les clients iOS qui doivent accéder à des ressources protégées, Azure Active Directory (Azure AD) fournit la bibliothèque d’authentification Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="71f31-107">Azure Active Directory (Azure AD) provides the Active Directory Authentication Library, or ADAL, for iOS clients that need to access protected resources.</span></span> <span data-ttu-id="71f31-108">ADAL simplifie le processus utilisé par votre application pour obtenir des jetons d’accès.</span><span class="sxs-lookup"><span data-stu-id="71f31-108">ADAL simplifies the process that your app uses to obtain access tokens.</span></span> <span data-ttu-id="71f31-109">Pour illustrer sa facilité d’utilisation, nous allons créer, dans cet article, une application de liste de tâches Objective C qui effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="71f31-109">To demonstrate how easy it is, in this article we build an Objective C To-Do List application that:</span></span>

* <span data-ttu-id="71f31-110">obtention de jetons d’accès pour appeler l’API Graph Azure AD à l’aide du [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) ;</span><span class="sxs-lookup"><span data-stu-id="71f31-110">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="71f31-111">recherche, dans un répertoire, d’utilisateurs correspondant à un alias donné ;</span><span class="sxs-lookup"><span data-stu-id="71f31-111">Searches a directory for users with a given alias.</span></span>

<span data-ttu-id="71f31-112">Pour générer l’application fonctionnelle complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="71f31-112">To build the complete working application, you need to:</span></span>

1. <span data-ttu-id="71f31-113">inscrire votre application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="71f31-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="71f31-114">installer et configurer la bibliothèque ADAL ;</span><span class="sxs-lookup"><span data-stu-id="71f31-114">Install and configure ADAL.</span></span>
3. <span data-ttu-id="71f31-115">utiliser la bibliothèque ADAL pour obtenir des jetons à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71f31-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="71f31-116">Pour commencer, téléchargez [la structure de l’application](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="71f31-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span> <span data-ttu-id="71f31-117">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="71f31-117">You also need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="71f31-118">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="71f31-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>


> [!TIP]
> <span data-ttu-id="71f31-119">Essayez la préversion de notre nouveau [portail des développeurs](https://identity.microsoft.com/Docs/iOS), qui vous permet de devenir opérationnel avec Azure AD en quelques minutes seulement.</span><span class="sxs-lookup"><span data-stu-id="71f31-119">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/iOS) that helps you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="71f31-120">Le portail des développeurs vous guide tout au long du processus d’inscription d’une application et d’intégration d’Azure AD à votre code.</span><span class="sxs-lookup"><span data-stu-id="71f31-120">The developer portal guides you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="71f31-121">Une fois que vous aurez terminé, vous disposerez d’une application simple capable d’authentifier les utilisateurs dans votre locataire et d’un serveur principal qui peut accepter des jetons et effectuer une validation.</span><span class="sxs-lookup"><span data-stu-id="71f31-121">When you’re finished, you'll have a simple application that can authenticate users in your tenant, and a back end that can accept tokens and perform validation.</span></span> 
> 
> 

## <a name="1-determine-what-your-redirect-uri-is-for-ios"></a><span data-ttu-id="71f31-122">1. Déterminer votre URI de redirection pour iOS</span><span class="sxs-lookup"><span data-stu-id="71f31-122">1. Determine what your redirect URI is for iOS</span></span>
<span data-ttu-id="71f31-123">Pour démarrer vos applications en toute sécurité dans certains scénarios d’authentification unique (SSO), vous devez créer un *URI de redirection* dans un format particulier.</span><span class="sxs-lookup"><span data-stu-id="71f31-123">To securely start your applications in certain SSO scenarios, you must create a *redirect URI* in a particular format.</span></span> <span data-ttu-id="71f31-124">Un URI de redirection permet de garantir que les jetons sont retournés vers la bonne application qui les a appelés.</span><span class="sxs-lookup"><span data-stu-id="71f31-124">A redirect URI is used to ensure that the tokens return to the correct application that asked for them.</span></span>


<span data-ttu-id="71f31-125">Le format iOS d’un URI de redirection est le suivant :</span><span class="sxs-lookup"><span data-stu-id="71f31-125">The iOS format for a redirect URI is:</span></span>

```
<app-scheme>://<bundle-id>
```

* <span data-ttu-id="71f31-126">**aap-scheme** : il est enregistré dans votre projet XCode.</span><span class="sxs-lookup"><span data-stu-id="71f31-126">**app-scheme** - This is registered in your XCode project.</span></span> <span data-ttu-id="71f31-127">Cela permet aux autres applications de vous appeler.</span><span class="sxs-lookup"><span data-stu-id="71f31-127">It is how other applications can call you.</span></span> <span data-ttu-id="71f31-128">Vous trouverez cela sous Info.plist -> Types d’URL -> Identificateur d’URL.</span><span class="sxs-lookup"><span data-stu-id="71f31-128">You can find this under Info.plist -> URL types -> URL Identifier.</span></span> <span data-ttu-id="71f31-129">Vous devez en créer une si vous n’en avez pas encore au moins une configurée.</span><span class="sxs-lookup"><span data-stu-id="71f31-129">You should create one if you don't already have one or more configured.</span></span>
* <span data-ttu-id="71f31-130">**bundle-id** : il s’agit de l’identificateur d’offre groupée se trouvant sous « identité » dans les paramètres de votre projet XCode.</span><span class="sxs-lookup"><span data-stu-id="71f31-130">**bundle-id** - This is the Bundle Identifier found under "identity" un your project settings in XCode.</span></span>

<span data-ttu-id="71f31-131">Voici un exemple de code de démarrage rapide : ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span><span class="sxs-lookup"><span data-stu-id="71f31-131">An example for this QuickStart code: ***msquickstart://com.microsoft.azureactivedirectory.samples.graph.QuickStart***</span></span>

## <a name="2-register-the-directorysearcher-application"></a><span data-ttu-id="71f31-132">2. Inscrire l’application DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="71f31-132">2. Register the DirectorySearcher application</span></span>
<span data-ttu-id="71f31-133">Pour configurer votre application afin d’obtenir des jetons, vous devez d’abord l’inscrire dans votre locataire Azure AD et lui accorder l’autorisation d’accéder à l’API Graph Azure AD :</span><span class="sxs-lookup"><span data-stu-id="71f31-133">To set up your app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="71f31-134">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="71f31-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="71f31-135">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="71f31-135">On the top bar, click your account.</span></span> <span data-ttu-id="71f31-136">Dans la liste **Répertoire**, choisissez le locataire Active Directory auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="71f31-136">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>
3. <span data-ttu-id="71f31-137">Cliquez sur **Plus de services** dans le volet de navigation le plus à gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="71f31-137">Click **More Services** in the leftmost navigation pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="71f31-138">Cliquez sur **Inscriptions d’applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="71f31-138">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="71f31-139">Suivez les invites pour créer une **application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="71f31-139">Follow the prompts to create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="71f31-140">Le **nom** de l’application donne une description de votre application aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="71f31-140">The **Name** of the application describes your application to end users.</span></span>
  * <span data-ttu-id="71f31-141">L’**URI de redirection** est une combinaison de schémas et de chaînes qu’Azure AD utilise pour retourner des réponses de jeton.</span><span class="sxs-lookup"><span data-stu-id="71f31-141">The **Redirect Uri** is a scheme and string combination that Azure AD uses to return token responses.</span></span>  <span data-ttu-id="71f31-142">Entrez une valeur spécifique à votre application et basée sur les informations d’URI de redirection précédentes.</span><span class="sxs-lookup"><span data-stu-id="71f31-142">Enter a value that is specific to your application and is based on the previous redirect URI information.</span></span>
6. <span data-ttu-id="71f31-143">Une fois que vous avez terminé l’inscription, Azure AD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="71f31-143">After you've completed the registration, Azure AD assigns your app a unique application ID.</span></span>  <span data-ttu-id="71f31-144">Copiez cette valeur dans l’onglet de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="71f31-144">You'll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="71f31-145">Dans la page **Paramètres**, sélectionnez **Autorisations nécessaires**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="71f31-145">From the **Settings** page, select **Required Permissions** and then select **Add**.</span></span> <span data-ttu-id="71f31-146">Sélectionnez **Microsoft Graph** comme API, puis ajoutez l’autorisation **Lire les données de l’annuaire** sous **Autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="71f31-146">Select **Microsoft Graph** as the API, and then add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="71f31-147">Cette opération configure votre application afin de pouvoir interroger l’API Azure AD Graph concernant les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="71f31-147">This sets up your application to query the Azure AD Graph API for users.</span></span>

## <a name="3-install-and-configure-adal"></a><span data-ttu-id="71f31-148">3. Installer et configurer la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="71f31-148">3. Install and configure ADAL</span></span>
<span data-ttu-id="71f31-149">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="71f31-149">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="71f31-150">Pour que la bibliothèque ADAL communique avec Azure AD, vous devez lui fournir des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="71f31-150">For ADAL to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

1. <span data-ttu-id="71f31-151">Commencez par ajouter la bibliothèque ADAL au projet DirectorySearcher à l’aide de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="71f31-151">Begin by adding ADAL to the DirectorySearcher project by using CocoaPods.</span></span>

    ```
    $ vi Podfile
    ```
2. <span data-ttu-id="71f31-152">Ajoutez le code suivant à ce podfile :</span><span class="sxs-lookup"><span data-stu-id="71f31-152">Add the following to this podfile:</span></span>

    ```
    source 'https://github.com/CocoaPods/Specs.git'
    link_with ['QuickStart']
    xcodeproj 'QuickStart'

    pod 'ADALiOS'
    ```

3. <span data-ttu-id="71f31-153">Chargez maintenant le podfile à l’aide de CocoaPods.</span><span class="sxs-lookup"><span data-stu-id="71f31-153">Now load the podfile by using CocoaPods.</span></span> <span data-ttu-id="71f31-154">Cette étape crée un espace de travail XCode que vous allez charger.</span><span class="sxs-lookup"><span data-stu-id="71f31-154">This step creates a new XCode workspace that you load.</span></span>

    ```
    $ pod install
    ...
    $ open QuickStart.xcworkspace
    ```

4. <span data-ttu-id="71f31-155">Dans le projet de démarrage rapide, ouvrez le fichier plist `settings.plist`.</span><span class="sxs-lookup"><span data-stu-id="71f31-155">In the QuickStart project, open the plist file `settings.plist`.</span></span>  <span data-ttu-id="71f31-156">Remplacez les valeurs des éléments de la section afin qu’elles reflètent les valeurs que vous avez entrées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="71f31-156">Replace the values of the elements in the section to reflect the values that you entered in the Azure portal.</span></span> <span data-ttu-id="71f31-157">Votre code fait référence à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="71f31-157">Your code references these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="71f31-158">`tenant` est le domaine de votre locataire Azure AD ; par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="71f31-158">The `tenant` is the domain of your Azure AD tenant, for example, contoso.onmicrosoft.com.</span></span>
  * <span data-ttu-id="71f31-159">`clientId` est l’ID client de votre application, copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="71f31-159">The `clientId` is the client ID of your application that you copied from the portal.</span></span>
  * <span data-ttu-id="71f31-160">`redirectUri` est l’URL de redirection que vous avez inscrite dans le portail.</span><span class="sxs-lookup"><span data-stu-id="71f31-160">The `redirectUri` is the redirect URL that you registered in the portal.</span></span>

## <a name="4----use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="71f31-161">4.    Utiliser la bibliothèque ADAL pour obtenir des jetons à partir d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="71f31-161">4.    Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="71f31-162">Le principe de base de la bibliothèque ADAL consiste simplement à appeler un completionBlock `+(void) getToken : ` chaque fois que votre application a besoin d’un jeton d’accès, et la bibliothèque ADAL s’occupe du reste.</span><span class="sxs-lookup"><span data-stu-id="71f31-162">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls a completionBlock `+(void) getToken : `, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="71f31-163">Dans le projet `QuickStart`, ouvrez `GraphAPICaller.m` et recherchez le commentaire `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` vers le haut.</span><span class="sxs-lookup"><span data-stu-id="71f31-163">In the `QuickStart` project, open `GraphAPICaller.m` and locate the `// TODO: getToken for generic Web API flows. Returns a token with no additional parameters provided.` comment near the top.</span></span>  <span data-ttu-id="71f31-164">C’est à ce moment-là que vous fournissez à la bibliothèque ADAL, à l’aide d’une méthode CompletionBlock, les coordonnées dont elle a besoin pour communiquer avec Azure AD, et que vous lui indiquez comment mettre en cache des jetons.</span><span class="sxs-lookup"><span data-stu-id="71f31-164">This is where you pass ADAL the coordinates through a CompletionBlock, to communicate with Azure AD, and tell it how to cache tokens.</span></span>

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
                        extraQueryParameters: @"nux=1" // if this strikes you as strange it was legacy to display the correct mobile UX. You most likely won't need it in your code.
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

2. <span data-ttu-id="71f31-165">Nous devons à présent utiliser ce jeton pour rechercher des utilisateurs dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="71f31-165">Now we need to use this token to search for users in the graph.</span></span> <span data-ttu-id="71f31-166">Recherchez le commentaire `// TODO: implement SearchUsersList`.</span><span class="sxs-lookup"><span data-stu-id="71f31-166">Find the `// TODO: implement SearchUsersList` comment.</span></span> <span data-ttu-id="71f31-167">Cette méthode effectue une demande GET auprès de l’API Graph Azure AD pour l’interroger à propos d’utilisateurs dont l’UPN commence par le terme de recherche donné.</span><span class="sxs-lookup"><span data-stu-id="71f31-167">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="71f31-168">Pour interroger l’API Azure AD Graph, vous devez inclure un jeton d’accès (access_token) dans l’en-tête `Authorization` de la demande.</span><span class="sxs-lookup"><span data-stu-id="71f31-168">To query the Azure AD Graph API, you need to include an access_token in the `Authorization` header of the request.</span></span> <span data-ttu-id="71f31-169">C’est là que la bibliothèque ADAL entre en jeu.</span><span class="sxs-lookup"><span data-stu-id="71f31-169">This is where ADAL comes in.</span></span>

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

                         // We can grab the JSON node at the top to get our graph data.
                         NSArray *graphDataArray = [dataReturned objectForKey:@"value"];

                         // Don't be thrown off by the key name being "value". It really is the name of the
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


3. <span data-ttu-id="71f31-170">Quand votre application demande un jeton en appelant `getToken(...)`, la bibliothèque ADAL tente de retourner un jeton sans demander à l’utilisateur ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="71f31-170">When your app requests a token by calling `getToken(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="71f31-171">Si la bibliothèque ADAL détermine que l’utilisateur doit se connecter pour obtenir un jeton, elle affiche une boîte de dialogue de connexion, récupère les informations d’identification de l’utilisateur, puis retourne un jeton après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="71f31-171">If ADAL determines that the user needs to sign in to get a token, it will display a dialog box for sign-in, collect the user's credentials, and then return a token after successful authentication.</span></span>  <span data-ttu-id="71f31-172">Si la bibliothèque ADAL ne peut pas retourner un jeton pour une raison quelconque, un `AdalException` est levé.</span><span class="sxs-lookup"><span data-stu-id="71f31-172">If ADAL is not able to return a token for any reason, it throws an `AdalException`.</span></span>

> [!Note] 
> <span data-ttu-id="71f31-173">L’objet `AuthenticationResult` contient un objet `tokenCacheStoreItem` qui peut être utilisé pour collecter les informations dont votre application peut avoir besoin.</span><span class="sxs-lookup"><span data-stu-id="71f31-173">The `AuthenticationResult` object contains a `tokenCacheStoreItem` object that can be used to collect the information that your app may need.</span></span> <span data-ttu-id="71f31-174">Dans le démarrage rapide, `tokenCacheStoreItem` est utilisé pour déterminer si l’authentification a déjà été effectuée.</span><span class="sxs-lookup"><span data-stu-id="71f31-174">In the QuickStart, `tokenCacheStoreItem` is used to determine if authentication is already done.</span></span>
>
>

## <a name="5-build-and-run-the-application"></a><span data-ttu-id="71f31-175">5. Génération et exécution de l’application</span><span class="sxs-lookup"><span data-stu-id="71f31-175">5. Build and run the application</span></span>
<span data-ttu-id="71f31-176">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="71f31-176">Congratulations!</span></span> <span data-ttu-id="71f31-177">Vous disposez désormais d’une application iOS fonctionnelle pouvant authentifier les utilisateurs, appeler en toute sécurité les API web à l’aide d’OAuth 2.0 et obtenir des informations de base concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="71f31-177">You now have a working iOS application that can authenticate users, securely call Web APIs by using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="71f31-178">Si vous ne l’avez pas encore fait, il est maintenant temps de remplir votre client avec quelques utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="71f31-178">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="71f31-179">Démarrez votre application de démarrage rapide, puis connectez-vous à l’aide de l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="71f31-179">Start your QuickStart app, and then sign in with one of those users.</span></span>  <span data-ttu-id="71f31-180">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="71f31-180">Search for other users based on their UPN.</span></span>  <span data-ttu-id="71f31-181">Fermez l’application, puis redémarrez-la.</span><span class="sxs-lookup"><span data-stu-id="71f31-181">Close the app, and then start it again.</span></span>  <span data-ttu-id="71f31-182">Notez que la session de l’utilisateur reste intacte.</span><span class="sxs-lookup"><span data-stu-id="71f31-182">Notice that the user's session remains intact.</span></span>

<span data-ttu-id="71f31-183">La bibliothèque ADAL facilite l’intégration de toutes ces fonctionnalités d’identité communes dans votre application.</span><span class="sxs-lookup"><span data-stu-id="71f31-183">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="71f31-184">Elle effectue les tâches ingrates à votre place, comme la gestion du cache, la prise en charge du protocole OAuth, la présentation d’une interface utilisateur à l’utilisateur pour qu’il se connecte et l’actualisation des jetons expirés.</span><span class="sxs-lookup"><span data-stu-id="71f31-184">It takes care of all the dirty work for you, like cache management, OAuth protocol support, presenting the user with a UI to sign in, and refreshing expired tokens.</span></span>  <span data-ttu-id="71f31-185">La seule chose que vous devez vraiment connaître est un appel unique d’API : `getToken`.</span><span class="sxs-lookup"><span data-stu-id="71f31-185">All you really need to know is a single API call, `getToken`.</span></span>

<span data-ttu-id="71f31-186">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est fourni sur [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="71f31-186">For reference, the completed sample (without your configuration values) is provided on [GitHub](https://github.com/AzureADQuickStarts/NativeClient-iOS/archive/complete.zip).</span></span>  

## <a name="next-steps"></a><span data-ttu-id="71f31-187">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="71f31-187">Next steps</span></span>
<span data-ttu-id="71f31-188">Vous pouvez à présent aborder d’autres scénarios.</span><span class="sxs-lookup"><span data-stu-id="71f31-188">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="71f31-189">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="71f31-189">You may want to try:</span></span>

* [<span data-ttu-id="71f31-190">Sécurisation d’une API web Node.js avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="71f31-190">Secure a Node.JS Web API with Azure AD</span></span>](active-directory-devquickstarts-webapi-nodejs.md)
* <span data-ttu-id="71f31-191">En savoir plus sur l’[activation d’une authentification unique (SSO) entre applications sur iOS à l’aide de la bibliothèque ADAL](active-directory-sso-ios.md)</span><span class="sxs-lookup"><span data-stu-id="71f31-191">Learn [how to enable cross-app SSO on iOS using ADAL](active-directory-sso-ios.md)</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

