---
title: "Bien démarrer avec Azure AD .NET | Microsoft Docs"
description: "Création d’une application de bureau Windows .NET qui s’intègre à Azure AD pour la connexion et appelle des API protégées par Azure AD à l’aide d’OAuth."
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
ms.openlocfilehash: 7a252e0e5243c7b7489373845531cb913ca1f6aa
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-into-a-windows-desktop-wpf-app"></a><span data-ttu-id="9d3db-103">Intégration d’Azure AD dans une application WPF de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="9d3db-103">Integrate Azure AD into a Windows Desktop WPF App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="9d3db-104">Si vous développez une application de bureau, Azure AD facilite l’authentification de vos utilisateurs avec leurs comptes Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d3db-104">If you're developing a desktop application, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="9d3db-105">Il permet également à votre application d’utiliser en toute sécurité une API web protégée par Azure AD, telle que l’API Office 365 ou Azure.</span><span class="sxs-lookup"><span data-stu-id="9d3db-105">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="9d3db-106">Pour les clients natifs .NET qui doivent accéder à des ressources protégées, Azure AD fournit la bibliothèque d’authentification Active Directory (bibliothèque ADAL).</span><span class="sxs-lookup"><span data-stu-id="9d3db-106">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="9d3db-107">Le seul objectif de cette bibliothèque est de faciliter l’obtention des jetons d’accès pour votre application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-107">ADAL's sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="9d3db-108">Pour illustrer sa facilité d’utilisation, nous allons créer une application To-Do List WPF .NET qui effectue les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="9d3db-108">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List application that:</span></span>

* <span data-ttu-id="9d3db-109">obtention de jetons d’accès pour appeler l’API Azure AD Graph à l’aide du [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);</span><span class="sxs-lookup"><span data-stu-id="9d3db-109">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="9d3db-110">recherche, dans un répertoire, d’utilisateurs correspondant à un alias donné ;</span><span class="sxs-lookup"><span data-stu-id="9d3db-110">Searches a directory for users with a given alias.</span></span>
* <span data-ttu-id="9d3db-111">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9d3db-111">Signs users out.</span></span>

<span data-ttu-id="9d3db-112">Pour générer l’application fonctionnelle complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="9d3db-112">To build the complete working application, you'll need to:</span></span>

1. <span data-ttu-id="9d3db-113">inscrire votre application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="9d3db-113">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="9d3db-114">installer et configurer la bibliothèque ADAL ;</span><span class="sxs-lookup"><span data-stu-id="9d3db-114">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="9d3db-115">utiliser la bibliothèque ADAL pour obtenir des jetons à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d3db-115">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="9d3db-116">Pour commencer, téléchargez [la structure de l’application](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9d3db-116">To get started, [download the app skeleton](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="9d3db-117">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-117">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="9d3db-118">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9d3db-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directorysearcher-application"></a><span data-ttu-id="9d3db-119">1. Inscription de l’application DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="9d3db-119">1. Register the DirectorySearcher Application</span></span>
<span data-ttu-id="9d3db-120">Pour autoriser votre application à obtenir des jetons, vous devez tout d’abord l’enregistrer dans votre client Azure AD et lui accorder l’autorisation d’accéder à l’API Graph Azure AD :</span><span class="sxs-lookup"><span data-stu-id="9d3db-120">To enable your app to get tokens, you'll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="9d3db-121">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d3db-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9d3db-122">Dans la barre supérieure, cliquez sur votre compte et, dans la liste **Répertoire**, choisissez le locataire Active Directory auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-122">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="9d3db-123">Cliquez sur **Autres services** dans le volet de navigation gauche et choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9d3db-123">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9d3db-124">Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9d3db-124">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="9d3db-125">Suivez les invites et créez une **application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="9d3db-125">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="9d3db-126">Le **nom** de l’application doit décrire votre application aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="9d3db-126">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="9d3db-127">L’ **URI de redirection** est une combinaison de schémas et de chaînes qu’Azure AD utilise pour renvoyer des réponses concernant les jetons.</span><span class="sxs-lookup"><span data-stu-id="9d3db-127">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="9d3db-128">Entrez une valeur spécifique de votre application, par exemple, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="9d3db-128">Enter a value specific to your application, e.g. `http://DirectorySearcher`.</span></span>
6. <span data-ttu-id="9d3db-129">Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-129">Once you've completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="9d3db-130">Copiez cette valeur à partir de la page de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="9d3db-130">You'll need this value in the next sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="9d3db-131">Sur la page **Paramètres**, choisissez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="9d3db-131">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="9d3db-132">Sélectionnez l’API **Microsoft Graph** et ajoutez l’autorisation **Lire les données de l’annuaire** sous **Autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="9d3db-132">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="9d3db-133">Cela permet à votre application d’interroger l’API Graph concernant les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9d3db-133">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="9d3db-134">2. Installez et configurez ADAL</span><span class="sxs-lookup"><span data-stu-id="9d3db-134">2. Install & Configure ADAL</span></span>
<span data-ttu-id="9d3db-135">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="9d3db-135">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="9d3db-136">Pour permettre à ADAL de communiquer avec Azure AD, vous devez lui fournir des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-136">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="9d3db-137">Commencez par ajouter ADAL au projet DirectorySearcher à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="9d3db-137">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="9d3db-138">Dans le projet DirectorySearcher, ouvrez `app.config`.</span><span class="sxs-lookup"><span data-stu-id="9d3db-138">In the DirectorySearcher project, open `app.config`.</span></span>  <span data-ttu-id="9d3db-139">Remplacez les valeurs des éléments de la section `<appSettings>` afin qu’elles reflètent les valeurs que vous avez saisies dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="9d3db-139">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="9d3db-140">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="9d3db-140">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="9d3db-141">`ida:Tenant` est le domaine de votre client Azure AD, par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9d3db-141">The `ida:Tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="9d3db-142">`ida:ClientId` est l’ID client de votre application que vous avez copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="9d3db-142">The `ida:ClientId` is the clientId of your application you copied from the portal.</span></span>
  * <span data-ttu-id="9d3db-143">`ida:RedirectUri` est l’URL de redirection que vous avez inscrite dans le portail.</span><span class="sxs-lookup"><span data-stu-id="9d3db-143">The `ida:RedirectUri` is the redirect url you registered in the portal.</span></span>

## <a name="3----use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="9d3db-144">3.    Utilisation de la bibliothèque ADAL pour obtenir des jetons à partir d’AAD</span><span class="sxs-lookup"><span data-stu-id="9d3db-144">3.    Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="9d3db-145">Le principe de base de la bibliothèque ADAL consiste simplement à appeler `authContext.AcquireTokenAsync(...)` chaque fois que votre application a besoin d’un jeton d’accès, et la bibliothèque ADAL s’occupe du reste.</span><span class="sxs-lookup"><span data-stu-id="9d3db-145">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireTokenAsync(...)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="9d3db-146">Dans le projet `DirectorySearcher`, ouvrez `MainWindow.xaml.cs` et recherchez la méthode `MainWindow()`.</span><span class="sxs-lookup"><span data-stu-id="9d3db-146">In the `DirectorySearcher` project, open `MainWindow.xaml.cs` and locate the `MainWindow()` method.</span></span>  <span data-ttu-id="9d3db-147">La première étape est d’initialiser `AuthenticationContext` pour votre application (classe principale de la bibliothèque ADAL).</span><span class="sxs-lookup"><span data-stu-id="9d3db-147">The first step is to initialize your app's `AuthenticationContext` - ADAL's primary class.</span></span>  <span data-ttu-id="9d3db-148">C’est à ce moment-là que vous fournissez à la bibliothèque ADAL les coordonnées dont elle a besoin pour communiquer avec Azure AD et lui indiquer comment mettre en cache des jetons.</span><span class="sxs-lookup"><span data-stu-id="9d3db-148">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainWindow()
{
    InitializeComponent();

    authContext = new AuthenticationContext(authority, new FileCache());

    CheckForCachedToken();
}
```

* <span data-ttu-id="9d3db-149">Recherchez maintenant la méthode `Search(...)` qui est appelée lorsque l’utilisateur clique sur le bouton Rechercher dans l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-149">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="9d3db-150">Cette méthode effectue une demande GET auprès de l’API Graph Azure AD pour l’interroger à propos d’utilisateurs dont l’UPN commence par le terme de recherche donné.</span><span class="sxs-lookup"><span data-stu-id="9d3db-150">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="9d3db-151">Cependant, pour interroger l’API Graph, vous devez inclure un jeton d’accès (access_token) dans l’en-tête `Authorization` de la demande ; c’est à ce moment qu’intervient la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="9d3db-151">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    // Validate the Input String
    if (string.IsNullOrEmpty(SearchText.Text))
    {
        MessageBox.Show("Please enter a value for the To Do item name");
        return;
    }

    // Get an Access Token for the Graph API
    AuthenticationResult result = null;
    try
    {
        result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectUri, new PlatformParameters(PromptBehavior.Auto));
        UserNameLabel.Content = result.UserInfo.DisplayableId;
        SignOutButton.Visibility = Visibility.Visible;
    }
    catch (AdalException ex)
    {
        // An unexpected error occurred, or user canceled the sign in.
        if (ex.ErrorCode != "access_denied")
            MessageBox.Show(ex.Message);

        return;
    }

    ...
}
```
* <span data-ttu-id="9d3db-152">Lorsque votre application demande un jeton en appelant `AcquireTokenAsync(...)`, la bibliothèque ADAL tente de renvoyer un jeton sans demander à l’utilisateur ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9d3db-152">When your app requests a token by calling `AcquireTokenAsync(...)`, ADAL will attempt to return a token without asking the user for credentials.</span></span>  <span data-ttu-id="9d3db-153">Si la bibliothèque ADAL détermine que l’utilisateur doit se connecter pour obtenir un jeton, elle affiche une boîte de dialogue de connexion, récupère les informations d’identification de l’utilisateur et renvoie un jeton après une authentification réussie.</span><span class="sxs-lookup"><span data-stu-id="9d3db-153">If ADAL determines that the user needs to sign in to get a token, it will display a login dialog, collect the user's credentials, and return a token upon successful authentication.</span></span>  <span data-ttu-id="9d3db-154">Si la bibliothèque ADAL ne peut pas renvoyer un jeton pour une raison quelconque, `AdalException`est renvoyé.</span><span class="sxs-lookup"><span data-stu-id="9d3db-154">If ADAL is unable to return a token for any reason, it will throw an `AdalException`.</span></span>
* <span data-ttu-id="9d3db-155">Notez que l’objet `AuthenticationResult` contient un objet `UserInfo` qui peut être utilisé pour collecter des informations dont votre application peut avoir besoin.</span><span class="sxs-lookup"><span data-stu-id="9d3db-155">Notice that the `AuthenticationResult` object contains a `UserInfo` object that can be used to collect information your app may need.</span></span>  <span data-ttu-id="9d3db-156">Dans DirectorySearcher, `UserInfo` est utilisé pour personnaliser l’interface utilisateur de l’application avec l’ID de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9d3db-156">In the DirectorySearcher, `UserInfo` is used to customize the app's UI with the user's id.</span></span>
* <span data-ttu-id="9d3db-157">Lorsque l’utilisateur clique sur le bouton Déconnexion, nous voulons vérifier que l’appel suivant vers `AcquireTokenAsync(...)` demande à l’utilisateur de se connecter.</span><span class="sxs-lookup"><span data-stu-id="9d3db-157">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenAsync(...)` will ask the user to sign in.</span></span>  <span data-ttu-id="9d3db-158">Avec la bibliothèque ADAL, c’est aussi simple que d’effacer le cache de jeton :</span><span class="sxs-lookup"><span data-stu-id="9d3db-158">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut(object sender = null, RoutedEventArgs args = null)
{
    // Clear the token cache
    authContext.TokenCache.Clear();

    ...
}
```

* <span data-ttu-id="9d3db-159">Toutefois, si l’utilisateur ne clique pas sur le bouton Déconnexion, vous devez maintenir la session de l’utilisateur pour sa prochaine exécution de DirectorySearcher.</span><span class="sxs-lookup"><span data-stu-id="9d3db-159">However, if the user does not click the "Sign Out" button, you will want to maintain the user's session for the next time they run the DirectorySearcher.</span></span>  <span data-ttu-id="9d3db-160">Lorsque l’application démarre, vous pouvez rechercher dans le cache de jetons de la bibliothèque ADAL un jeton existant et mettre à jour l’interface utilisateur en conséquence.</span><span class="sxs-lookup"><span data-stu-id="9d3db-160">When the app launches, you can check ADAL's token cache for an existing token and update the UI accordingly.</span></span>  <span data-ttu-id="9d3db-161">Dans la méthode `CheckForCachedToken()`, passez un autre appel à `AcquireTokenAsync(...)`, cette fois en transmettant le paramètre `PromptBehavior.Never`.</span><span class="sxs-lookup"><span data-stu-id="9d3db-161">In the `CheckForCachedToken()` method, make another call to `AcquireTokenAsync(...)`, this time passing in the `PromptBehavior.Never` parameter.</span></span>  <span data-ttu-id="9d3db-162">`PromptBehavior.Never` indiquera à ADAL que l’utilisateur ne doit pas être invité à se connecter et que la bibliothèque ADAL doit à la place lever une exception s’il est impossible de renvoyer un jeton.</span><span class="sxs-lookup"><span data-stu-id="9d3db-162">`PromptBehavior.Never` will tell ADAL that the user should not be prompted for sign in, and ADAL should instead throw an exception if it is unable to return a token.</span></span>

```C#
public async void CheckForCachedToken() 
{
    // As the application starts, try to get an access token without prompting the user.  If one exists, show the user as signed in.
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

        // If user interaction is required, proceed to main page without singing the user in.
        return;
    }

    // A valid token is in the cache
    SignOutButton.Visibility = Visibility.Visible;
    UserNameLabel.Content = result.UserInfo.DisplayableId;
}
```

<span data-ttu-id="9d3db-163">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="9d3db-163">Congratulations!</span></span> <span data-ttu-id="9d3db-164">Vous disposez d’une application .NET WPF fonctionnelle capable d’authentifier les utilisateurs, d’appeler en toute sécurité les API web à l’aide d’OAuth 2.0 et d’obtenir des informations de base concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9d3db-164">You now have a working .NET WPF application that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="9d3db-165">Si vous ne l’avez pas encore fait, il est maintenant temps de remplir votre client avec quelques utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9d3db-165">If you haven't already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="9d3db-166">Exécutez votre application DirectorySearcher et connectez-vous avec l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="9d3db-166">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="9d3db-167">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="9d3db-167">Search for other users based on their UPN.</span></span>  <span data-ttu-id="9d3db-168">Fermez l’application et exécutez-la de nouveau.</span><span class="sxs-lookup"><span data-stu-id="9d3db-168">Close the app, and re-run it.</span></span>  <span data-ttu-id="9d3db-169">Observez que la session utilisateur reste identique.</span><span class="sxs-lookup"><span data-stu-id="9d3db-169">Notice how the user's session remains intact.</span></span>  <span data-ttu-id="9d3db-170">Déconnectez-vous et reconnectez-vous sous le nom d’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="9d3db-170">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="9d3db-171">La bibliothèque ADAL facilite l’intégration de toutes ces fonctionnalités d’identité communes dans votre application.</span><span class="sxs-lookup"><span data-stu-id="9d3db-171">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="9d3db-172">Elle effectue les tâches ingrates pour vous : gestion du cache, prise en charge du protocole OAuth, présentation d’une interface utilisateur de connexion à l’utilisateur, actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="9d3db-172">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="9d3db-173">La seule chose que vous devez vraiment connaître est un appel unique d’API : `authContext.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="9d3db-173">All you really need to know is a single API call, `authContext.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="9d3db-174">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est fourni [ici](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="9d3db-174">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-DotNet/archive/complete.zip).</span></span>  <span data-ttu-id="9d3db-175">Vous pouvez à présent aborder d’autres scénarios.</span><span class="sxs-lookup"><span data-stu-id="9d3db-175">You can now move on to additional scenarios.</span></span>  <span data-ttu-id="9d3db-176">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="9d3db-176">You may want to try:</span></span>

[<span data-ttu-id="9d3db-177">Sécurisation d’une API web .NET avec Azure AD >></span><span class="sxs-lookup"><span data-stu-id="9d3db-177">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

