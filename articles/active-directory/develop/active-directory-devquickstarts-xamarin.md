---
title: aaaAzure AD Xamarin prise en main | Documents Microsoft
description: "Créez des applications Xamarin qui s’intègrent avec Azure AD pour la connexion et appellent des API protégées par Azure AD en utilisant OAuth."
services: active-directory
documentationcenter: xamarin
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 198cd2c3-f7c8-4ec2-b59d-dfdea9fe7d95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6a0d189648b7071558ac1cf2b908808668960a4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="ba7f2-103">Intégrer Azure AD avec des applications Xamarin</span><span class="sxs-lookup"><span data-stu-id="ba7f2-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="ba7f2-104">Avec Xamarin, vous pouvez écrire des applications mobiles en C# qui peuvent s’exécuter sous iOS, Android et Windows (appareils mobiles et PC).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="ba7f2-105">Si vous créez une application à l’aide de Xamarin, Azure Active Directory (Azure AD) rend tooauthenticate simple des utilisateurs avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple tooauthenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="ba7f2-106">application Hello peut consommer également en toute sécurité les API web qui est protégé par Azure AD, par exemple hello API Office 365 ou hello API Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-106">hello app can also securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="ba7f2-107">Pour les applications Xamarin ont besoin de ressources de tooaccess protégé, Azure AD fournit hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-107">For Xamarin apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="ba7f2-108">Hello seul but de la bibliothèque ADAL est toomake plus facile pour les jetons d’accès aux applications tooget.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-108">hello sole purpose of ADAL is toomake it easy for apps tooget access tokens.</span></span> <span data-ttu-id="ba7f2-109">toodemonstrate facilement est, cet article explique comment les applications DirectorySearcher toobuild qui :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-109">toodemonstrate how easy it is, this article shows how toobuild DirectorySearcher apps that:</span></span>

* <span data-ttu-id="ba7f2-110">exécution sous iOS, Android, Windows Desktop, Windows Phone et Windows Store ;</span><span class="sxs-lookup"><span data-stu-id="ba7f2-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="ba7f2-111">Utiliser une seule classe portable bibliothèque (PCL) tooauthenticate utilisateurs et obtenir des jetons pour hello API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-111">Use a single portable class library (PCL) tooauthenticate users and get tokens for hello Azure AD Graph API.</span></span>
* <span data-ttu-id="ba7f2-112">recherche, dans un annuaire, d’utilisateurs correspondant à un UPN (nom d’utilisateur principal) donné.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="ba7f2-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ba7f2-113">Before you get started</span></span>
* <span data-ttu-id="ba7f2-114">Télécharger hello [projet squelette](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), ou télécharger hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-114">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="ba7f2-115">Chaque téléchargement est une solution Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="ba7f2-116">Vous devez également un locataire Azure AD dans lequel les utilisateurs de toocreate et inscrire l’application hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-116">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="ba7f2-117">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-117">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="ba7f2-118">Lorsque vous êtes prêt, suivez les procédures de hello dans hello quatre sections.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-118">When you are ready, follow hello procedures in hello next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="ba7f2-119">Étape 1 : Configurer votre environnement de développement Xamarin</span><span class="sxs-lookup"><span data-stu-id="ba7f2-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="ba7f2-120">Étant donné que ce didacticiel inclut des projets pour iOS, Android et Windows, il vous faut à la fois Visual Studio et Xamarin.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="ba7f2-121">environnement nécessaires de toocreate hello, processus hello complète dans [définir configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-121">toocreate hello necessary environment, complete hello process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="ba7f2-122">instructions de Hello incluent des documents que vous pouvez consulter toolearn plus sur Xamarin pendant que vous patientez pour hello installations toobe est terminée.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-122">hello instructions include material that you can review toolearn more about Xamarin while you're waiting for hello installations toobe completed.</span></span>

<span data-ttu-id="ba7f2-123">Après avoir terminé le programme d’installation Bonjour, ouvrir la solution de hello dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-123">After you've completed hello setup, open hello solution in Visual Studio.</span></span> <span data-ttu-id="ba7f2-124">Vous y trouverez six projets : cinq projets propres à la plateforme et une PCL, DirectorySearcher.cs, partagée par toutes les plateformes.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-hello-directorysearcher-app"></a><span data-ttu-id="ba7f2-125">Étape 2 : Inscrire l’application DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="ba7f2-125">Step 2: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="ba7f2-126">jetons de tooget tooenable hello application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess autorisation API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-126">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="ba7f2-127">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-127">Here's how:</span></span>

1. <span data-ttu-id="ba7f2-128">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ba7f2-129">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-129">On hello top bar, click your account.</span></span> <span data-ttu-id="ba7f2-130">Ensuite, sous hello **répertoire** liste, le client d’Active Directory hello sélectionnez où vous souhaitez tooregister hello application.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-130">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="ba7f2-131">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-131">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="ba7f2-132">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="ba7f2-133">toocreate un nouveau **Application cliente Native**, suivez les invites hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-133">toocreate a new **Native Client Application**, follow hello prompts.</span></span>
  * <span data-ttu-id="ba7f2-134">**Nom** décrit hello application toousers.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-134">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="ba7f2-135">**URI de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-135">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="ba7f2-136">Entrez une valeur (par exemple, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="ba7f2-137">Une fois que vous avez terminé l’inscription, Azure AD assigne application hello un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-137">After you’ve completed registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="ba7f2-138">Copier la valeur de hello de hello **Application** sous l’onglet, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-138">Copy hello value from hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="ba7f2-139">Sur hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-139">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="ba7f2-140">Sélectionnez **Microsoft Graph** comme hello API.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-140">Select **Microsoft Graph** as hello API.</span></span> <span data-ttu-id="ba7f2-141">Sous **autorisations déléguées**, ajouter hello **les données d’annuaire en lecture** autorisation.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-141">Under **Delegated Permissions**, add hello **Read Directory Data** permission.</span></span>  
<span data-ttu-id="ba7f2-142">Cette action active tooquery hello API Graph de hello application pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-142">This action enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="ba7f2-143">Étape 3 : Installer et configurer la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="ba7f2-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="ba7f2-144">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="ba7f2-145">tooenable toocommunicate ADAL avec Azure AD, lui donner des informations sur l’inscription d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-145">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="ba7f2-146">Ajouter la bibliothèque ADAL toohello DirectorySearcher projet à l’aide de hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-146">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirectorySearcherLib
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Android
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Desktop
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-iOS
    `

    `
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -ProjectName DirSearchClient-Universal
    `

    <span data-ttu-id="ba7f2-147">Notez que les deux références de bibliothèque sont ajoutées tooeach projet : hello PCL partie ADAL et une partie spécifique à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-147">Note that two library references are added tooeach project: hello PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="ba7f2-148">Dans le projet de DirectorySearcherLib hello, ouvrez DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-148">In hello DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="ba7f2-149">Remplacez les valeurs de membre de classe hello avec des valeurs hello que vous avez entré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-149">Replace hello class member values with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="ba7f2-150">Votre code fait référence à des valeurs de toothese chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-150">Your code refers toothese values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="ba7f2-151">Hello *client* est domaine hello de votre client Azure AD (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-151">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="ba7f2-152">Hello *clientId* est l’ID de client hello de l’application hello, que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-152">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
  * <span data-ttu-id="ba7f2-153">Hello *returnUri* est l’URI que vous avez entré dans le portail hello (par exemple, http://DirectorySearcher) de la redirection hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-153">hello *returnUri* is hello redirect URI that you entered in hello portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="ba7f2-154">Étape 4 : Utiliser la bibliothèque ADAL tooget des jetons d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba7f2-154">Step 4: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="ba7f2-155">Quasi-totalité de la logique d’authentification de l’application hello se trouve `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-155">Almost all of hello app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="ba7f2-156">Tout ce qui est nécessaire dans les projets spécifiques à une plateforme hello est toopass un toohello paramètre contextuelles `DirectorySearcher` PCL.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-156">All that's necessary in hello platform-specific projects is toopass a contextual parameter toohello `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="ba7f2-157">Ouvrez DirectorySearcher.cs et ajoutez un nouveau toohello de paramètre `SearchByAlias(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-157">Open DirectorySearcher.cs, and then add a new parameter toohello `SearchByAlias(...)` method.</span></span> <span data-ttu-id="ba7f2-158">`IPlatformParameters`est l’authentification ADAL besoins tooperform hello des objets de paramètre hello contextuelles qui encapsule hello spécifique à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-158">`IPlatformParameters` is hello contextual parameter that encapsulates hello platform-specific objects that ADAL needs tooperform hello authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="ba7f2-159">Initialiser `AuthenticationContext`, qui est la classe principale hello de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-159">Initialize `AuthenticationContext`, which is hello primary class of ADAL.</span></span>  
<span data-ttu-id="ba7f2-160">Cette hello ADAL de passes action il coordonne toocommunicate besoins avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-160">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD.</span></span>
3. <span data-ttu-id="ba7f2-161">Appelez `AcquireTokenAsync(...)`, qui accepte hello `IPlatformParameters` de l’objet et appelle les flux d’authentification hello sont nécessaire tooreturn une application toohello de jeton.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-161">Call `AcquireTokenAsync(...)`, which accepts hello `IPlatformParameters` object and invokes hello authentication flow that's necessary tooreturn a token toohello app.</span></span>

    ```C#
    ...
        AuthenticationResult authResult = null;
        try
        {
            AuthenticationContext authContext = new AuthenticationContext(authority);
            authResult = await authContext.AcquireTokenAsync(graphResourceUri, clientId, returnUri, parent);
        }
        catch (Exception ee)
        {
            results.Add(new User { error = ee.Message });
            return results;
        }
    ...
    ```

    <span data-ttu-id="ba7f2-162">`AcquireTokenAsync(...)`première tentatives tooreturn un jeton pour hello la ressource (hello API Graph dans ce cas) demandée sans invite les utilisateurs tooenter leurs informations d’identification (via la mise en cache ou l’actualisation des jetons ancien).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-162">`AcquireTokenAsync(...)` first attempts tooreturn a token for hello requested resource (hello Graph API in this case) without prompting users tooenter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="ba7f2-163">Si nécessaire, il affiche les utilisateurs hello Azure AD-page de connexion avant d’acquérir le jeton demandé de hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-163">As necessary, it shows users hello Azure AD sign-in page before acquiring hello requested token.</span></span>
4. <span data-ttu-id="ba7f2-164">Attacher la demande d’API Graph hello accès toohello jeton Bonjour **autorisation** en-tête :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-164">Attach hello access token toohello Graph API request in hello **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="ba7f2-165">C’est pourquoi `DirectorySearcher` le code de bibliothèque de classes portables et hello application associées à l’identité.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-165">That's all for hello `DirectorySearcher` PCL and hello app's identity-related code.</span></span> <span data-ttu-id="ba7f2-166">Il ne reste que toocall hello `SearchByAlias(...)` méthode dans les vues de chaque plateforme et, le cas échéant, le code tooadd pour gérer correctement hello cycle de vie de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-166">All that remains is toocall hello `SearchByAlias(...)` method in each platform's views and, where necessary, tooadd code for correctly handling hello UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="ba7f2-167">Android</span><span class="sxs-lookup"><span data-stu-id="ba7f2-167">Android</span></span>
1. <span data-ttu-id="ba7f2-168">Dans MainActivity.cs, ajoutez un appel trop`SearchByAlias(...)` du bouton hello Gestionnaire click :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-168">In MainActivity.cs, add a call too`SearchByAlias(...)` in hello button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="ba7f2-169">Remplacer hello `OnActivityResult` tooforward de méthode du cycle de vie d’authentification redirige la méthode appropriée de toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-169">Override hello `OnActivityResult` lifecycle method tooforward any authentication redirects back toohello appropriate method.</span></span> <span data-ttu-id="ba7f2-170">La bibliothèque ADAL fournit une méthode d’assistance pour cela dans Android :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="ba7f2-171">Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="ba7f2-171">Windows Desktop</span></span>
<span data-ttu-id="ba7f2-172">Dans MainWindow.xaml.cs, effectuez un appel trop`SearchByAlias(...)` en passant un `WindowInteropHelper` dans desktop hello `PlatformParameters` objet :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-172">In MainWindow.xaml.cs, make a call too`SearchByAlias(...)` by passing a `WindowInteropHelper` in hello desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="ba7f2-173">iOS</span><span class="sxs-lookup"><span data-stu-id="ba7f2-173">iOS</span></span>
<span data-ttu-id="ba7f2-174">Dans DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` objet prend un toohello référence View Controller :</span><span class="sxs-lookup"><span data-stu-id="ba7f2-174">In DirSearchClient_iOSViewController.cs, hello iOS `PlatformParameters` object takes a reference toohello View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="ba7f2-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="ba7f2-175">Windows Universal</span></span>
<span data-ttu-id="ba7f2-176">Dans l’application Windows universelle, ouvrez MainPage.xaml.cs et implémentez hello `Search` (méthode).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-176">In Windows Universal, open MainPage.xaml.cs, and then implement hello `Search` method.</span></span> <span data-ttu-id="ba7f2-177">Cette méthode utilise une méthode d’assistance dans une interface utilisateur de tooupdate projet partagé si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-177">This method uses a helper method in a shared project tooupdate UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="ba7f2-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba7f2-178">What's next</span></span>
<span data-ttu-id="ba7f2-179">Vous disposez maintenant d’une application Xamarin fonctionnelle capable d’authentifier les utilisateurs et d’appeler en toute sécurité les API web à l’aide d’OAuth 2.0 sur cinq plateformes différentes.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="ba7f2-180">Si vous n’avez pas déjà renseigné votre client avec les utilisateurs, est à présent hello temps toodo donc.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-180">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>

1. <span data-ttu-id="ba7f2-181">Exécuter votre application DirectorySearcher, puis connectez-vous avec l’un des utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-181">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="ba7f2-182">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="ba7f2-183">La bibliothèque ADAL facilite fonctionnalités d’identité commune tooincorporate facile dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-183">ADAL makes it easy tooincorporate common identity features into hello app.</span></span> <span data-ttu-id="ba7f2-184">Il s’occupe de tout le travail dirty hello, telles que la gestion du cache, prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, et l’actualisation a expiré de jetons.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-184">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="ba7f2-185">Vous devez tooknow uniquement une seule API appel, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-185">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="ba7f2-186">Pour référence, téléchargez hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sans les valeurs de configuration).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-186">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="ba7f2-187">Vous pouvez maintenant déplacer sur les scénarios d’identité tooadditional.</span><span class="sxs-lookup"><span data-stu-id="ba7f2-187">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="ba7f2-188">Par exemple, essayez de [Sécuriser une API web .NET avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ba7f2-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
