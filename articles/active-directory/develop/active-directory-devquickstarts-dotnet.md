---
title: .NET aaaAzure AD prise en main | Documents Microsoft
description: "Comment toobuild une application de bureau Windows de .NET qui s’intègre à Azure AD pour l’authentification dans Azure AD qui appelle protégé API en utilisant OAuth."
services: active-directory
documentationcenter: .net
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: ed33574f-6fa3-402c-b030-fae76fba84e1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: c09b358f24c7bfb371b34cf72ca48c0a45042f5f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="30241-103">Intégration d’Azure AD dans une application WPF de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="30241-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="30241-104">Si vous développez une application de bureau, Azure AD rend très simple pour vous tooauthenticate vos utilisateurs avec leurs comptes Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30241-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="30241-105">Il permet également de votre application toosecurely consommer n’importe quel web API protégée par Azure AD, comme la hello API Office 365 ou hello API Azure.</span><span class="sxs-lookup"><span data-stu-id="30241-105">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="30241-106">Pour .NET native les clients qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello bibliothèque d’authentification Active Directory, ou la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="30241-106">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="30241-107">Seul objectif la bibliothèque ADAL de durée de vie est toomake plus facile pour les jetons d’accès tooget votre application.</span><span class="sxs-lookup"><span data-stu-id="30241-107">ADAL's sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="30241-108">toodemonstrate facilité il s’agit, ici nous allons créer une application de liste de tâches WPF .NET :</span><span class="sxs-lookup"><span data-stu-id="30241-108">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="30241-109">Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="30241-109">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="30241-110">recherche, dans un répertoire, d’utilisateurs correspondant à un alias donné ;</span><span class="sxs-lookup"><span data-stu-id="30241-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="30241-111">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="30241-111">Signs users out.</span></span>

<span data-ttu-id="30241-112">toobuild hello travail application complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="30241-112">toobuild hello complete working application, you'll need to:</span></span>

1. <span data-ttu-id="30241-113">inscrire votre application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="30241-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="30241-114">installer et configurer la bibliothèque ADAL ;</span><span class="sxs-lookup"><span data-stu-id="30241-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="30241-115">Utiliser des jetons tooget ADAL d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30241-115">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="30241-116">tooget démarré, [télécharger squelette d’application hello](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="30241-116">tooget started, [download hello app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="30241-117">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="30241-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="30241-118">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="30241-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directorysearcher-application"></a><span data-ttu-id="30241-119">1. Inscrire hello DirectorySearcher Application</span><span class="sxs-lookup"><span data-stu-id="30241-119">1. Register hello DirectorySearcher Application</span></span>
<span data-ttu-id="30241-120">tooenable vos jetons tooget d’application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess d’autorisation Azure AD Graph API :</span><span class="sxs-lookup"><span data-stu-id="30241-120">tooenable your app tooget tokens, you'll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="30241-121">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="30241-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="30241-122">Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="30241-122">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="30241-123">Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="30241-123">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="30241-124">Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="30241-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="30241-125">Suivez les invites hello et créer un nouveau **Application cliente Native**.</span><span class="sxs-lookup"><span data-stu-id="30241-125">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="30241-126">Hello **nom** Hello application décrivent tooend-utilisateurs de votre application</span><span class="sxs-lookup"><span data-stu-id="30241-126">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="30241-127">Hello **Uri de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.</span><span class="sxs-lookup"><span data-stu-id="30241-127">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="30241-128">Entrez une application tooyour spécifique de la valeur, par exemple, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="30241-128">Enter a value specific tooyour application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="30241-129">Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="30241-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="30241-130">Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de la page de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="30241-130">You'll need this value in hello next sections, so copy it from hello application page.</span></span>
7. <span data-ttu-id="30241-131">À partir de hello **paramètres** choisissez **autorisations requises** et choisissez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="30241-131">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="30241-132">Sélectionnez hello **Microsoft Graph** comme hello API et ajouter hello **les données d’annuaire en lecture** autorisation sous **autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="30241-132">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="30241-133">Cette opération activera votre hello de tooquery d’application API Graph pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="30241-133">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="30241-134">2. Installez et configurez ADAL</span><span class="sxs-lookup"><span data-stu-id="30241-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="30241-135">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="30241-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="30241-136">Toocommunicate en mesure de toobe ADAL avec Azure AD, vous devez tooprovide avec des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="30241-136">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="30241-137">Commencez par ajouter le projet de DirectorySearcher toohello ADAL à l’aide de la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="30241-137">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="30241-138">Dans le projet de DirectorySearcher hello, ouvrez `app.config`.</span><span class="sxs-lookup"><span data-stu-id="30241-138">In hello DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="30241-139">Remplacez les valeurs hello d’éléments hello Bonjour `<appSettings>` hello tooreflect de section les valeurs d’entrée en hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="30241-139">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="30241-140">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="30241-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="30241-141">Hello `ida:Tenant` est domaine hello de votre client Azure AD, par exemple, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="30241-141">hello `ida:Tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="30241-142">Hello `ida:ClientId` est clientId hello de votre application que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="30241-142">hello `ida:ClientId` is hello clientId of your application you copied from hello portal.</span></span>
  * <span data-ttu-id="30241-143">Hello `ida:RedirectUri` est hello rediriger l’url que vous avez enregistré dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="30241-143">hello `ida:RedirectUri` is hello redirect url you registered in hello portal.</span></span>

## <a name="3----use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="30241-144">3.    Utiliser des jetons tooGet ADAL d’AAD</span><span class="sxs-lookup"><span data-stu-id="30241-144">3.    Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="30241-145">Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que votre application a besoin d’un jeton d’accès, il appelle simplement `authContext.AcquireTokenAsync(...)`, et la bibliothèque ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="30241-145">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="30241-146">Bonjour `DirectorySearcher` projet, ouvrez `MainWindow.xaml.cs` et recherchez hello `MainWindow()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="30241-146">In hello `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate hello `MainWindow()` method.</span></span>  <span data-ttu-id="30241-147">première étape de Hello est tooinitialize de votre application `AuthenticationContext` -ADAL de la classe principale.</span><span class="sxs-lookup"><span data-stu-id="30241-147">hello first step is tooinitialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="30241-148">Il s’agit d’où vous passez la bibliothèque ADAL hello coordonnées nécessaires toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.</span><span class="sxs-lookup"><span data-stu-id="30241-148">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="30241-149">Maintenant recherchez hello `Search(...)` (méthode), qui sera appelé lorsque hello utilisateur cliks hello « Rechercher » un bouton dans l’interface utilisateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="30241-149">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="30241-150">Cette méthode rend un tooquery toohello API Azure AD Graph de demande GET pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="30241-150">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="30241-151">Mais dans hello tooquery de commande API Graph, vous devez tooinclude un access_token Bonjour `Authorization` en-tête Hello demande - il s’agit là qu’intervient la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="30241-151">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate hello Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for hello tooDo item name");
        return;
    }

    // Get an Access Token for hello Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled hello sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="30241-152">Lorsque votre application demande un jeton en appelant `AcquireTokenAsync(...)`, la bibliothèque ADAL va tenter de tooreturn un jeton sans demander hello pour les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="30241-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt tooreturn a token without asking hello user for credentials.</span></span>  <span data-ttu-id="30241-153">Si la bibliothèque ADAL détermine que l’utilisateur hello doit toosign dans tooget un jeton, s’afficher une boîte de dialogue de connexion, collecter des informations d’identification de l’utilisateur hello et retourne un jeton après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="30241-153">If ADAL determines that hello user needs toosign in tooget a token, it will display a login dialog, collect hello user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="30241-154">Si la bibliothèque ADAL est impossible de tooreturn un jeton pour une raison quelconque, elle lève une `AdalException`.</span><span class="sxs-lookup"><span data-stu-id="30241-154">If ADAL is unable tooreturn a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="30241-155">Notez que hello `AuthenticationResult` objet contient un `UserInfo` objet qui peut être informations toocollect utilisé votre application peut avoir besoin.</span><span class="sxs-lookup"><span data-stu-id="30241-155">Notice that hello `AuthenticationResult` object contains a `UserInfo` object that can be used toocollect information your app may need.</span></span>  <span data-ttu-id="30241-156">Bonjour DirectorySearcher, `UserInfo` est l’interface utilisateur de l’application de hello toocustomize utilisé avec l’id de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="30241-156">In hello DirectorySearcher, `UserInfo` is used toocustomize hello app's UI with hello user's id.</span></span>
* <span data-ttu-id="30241-157">Utilisateur de hello clique sur bouton « Déconnexion » hello, nous souhaitons tooensure qui hello prochain appel trop`AcquireTokenAsync(...)` demandera toosign d’utilisateur hello dans.</span><span class="sxs-lookup"><span data-stu-id="30241-157">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenAsync(...)` will ask hello user toosign in.</span></span>  <span data-ttu-id="30241-158">Avec la bibliothèque ADAL, il est aussi simple que l’effacement du cache de jetons hello :</span><span class="sxs-lookup"><span data-stu-id="30241-158">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear hello token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="30241-159">Toutefois, si l’utilisateur de hello ne cliquez pas sur bouton « Déconnexion » hello, vous pouvez toomaintain hello de session pour hello leur exécution suivante hello DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="30241-159">However, if hello user does not click hello "Sign Out" button, you will want toomaintain hello user's session for hello next time they run hello DirectorySearcher.</span></span>  <span data-ttu-id="30241-160">Lors de l’application hello démarre, vous pouvez vérifier le cache de jeton de la bibliothèque ADAL pour un jeton existant et mettre à jour de l’interface utilisateur de hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="30241-160">When hello app launches, you can check ADAL's token cache for an existing token and update hello UI accordingly.</span></span>  <span data-ttu-id="30241-161">Bonjour `CheckForCachedToken()` (méthode), effectuer un autre appel trop`AcquireTokenAsync(...)`, cette fois en passant hello `PromptBehavior.Never` paramètre.</span><span class="sxs-lookup"><span data-stu-id="30241-161">In hello `CheckForCachedToken()` method, make another call too`AcquireTokenAsync(...)`, this time passing in hello `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="30241-162">`PromptBehavior.Never`Indique à la bibliothèque ADAL qu’utilisateur de hello ne doit pas être invité pour la connexion et la bibliothèque ADAL doit plutôt lever une exception s’il est impossible de tooreturn un jeton.</span><span class="sxs-lookup"><span data-stu-id="30241-162">`PromptBehavior.Never` will tell ADAL that hello user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable tooreturn a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As hello application starts, try tooget an access token without prompting hello user.  If one exists, show hello user as signed in.
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Never));
    }
    catch (AdalException ex)
    {
        if (ex.ErrorCode != "user_interaction_required")
        {
            // An unexpected error occurred.
            MessageBox.Show(ex.Message);
        }

        // If user interaction is required, proceed toomain page without singing hello user in.
        return;
    }

    // A valid token is in hello cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="30241-163">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="30241-163">Congratulations!</span></span> <span data-ttu-id="30241-164">Vous avez une application WPF .NET qui a des utilisateurs tooauthenticate hello capacité, en toute sécurité appelez des API Web à l’aide d’OAuth 2.0 et obtenez des informations de base sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="30241-164">You now have a working .NET WPF application that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="30241-165">Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="30241-165">If you haven't already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="30241-166">Exécutez votre application DirectorySearcher et connectez-vous avec l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="30241-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="30241-167">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="30241-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="30241-168">Fermez l’application hello et réexécutez-la.</span><span class="sxs-lookup"><span data-stu-id="30241-168">Close hello app, and re-run it.</span></span>  <span data-ttu-id="30241-169">Notez que la session de l’utilisateur hello reste intacte.</span><span class="sxs-lookup"><span data-stu-id="30241-169">Notice how hello user's session remains intact.</span></span>  <span data-ttu-id="30241-170">Déconnectez-vous et reconnectez-vous sous le nom d’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="30241-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="30241-171">ADAL rend facile tooincorporate toutes ces fonctionnalités d’identité commune dans votre application.</span><span class="sxs-lookup"><span data-stu-id="30241-171">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="30241-172">Il s’occupe de tout le travail dirty hello vous - gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="30241-172">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="30241-173">Vous devez vraiment tooknow est un simple appel d’API `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="30241-173">All you really need tooknow is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="30241-174">Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni [ici](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="30241-174">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="30241-175">Vous pouvez maintenant déplacer sur les scénarios de tooadditional.</span><span class="sxs-lookup"><span data-stu-id="30241-175">You can now move on tooadditional scenarios.</span></span>  <span data-ttu-id="30241-176">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="30241-176">You may want tootry:</span></span>

[<span data-ttu-id="30241-177">Sécurisation d’une API web .NET avec Azure AD &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="30241-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

