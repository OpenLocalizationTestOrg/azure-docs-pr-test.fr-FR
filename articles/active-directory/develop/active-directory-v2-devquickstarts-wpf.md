---
title: Application native .NET Azure Active Directory v2.0 | Microsoft Docs
description: "Comment créer une application native .NET qui se connecte avec les comptes Microsoft personnels, ainsi qu’avec les comptes professionnels ou scolaires."
services: active-directory
documentationcenter: 
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 46d81e09-bad0-44ce-9026-881805976e72
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/30/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 7389f55ee6fef9548abb0ca4ac1bbd0399868d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="add-sign-in-to-a-windows-desktop-app"></a><span data-ttu-id="09513-103">Ajouter une connexion à une application de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="09513-103">Add sign-in to a Windows Desktop app</span></span>
<span data-ttu-id="09513-104">Le point de terminaison v2.0 vous permet de rapidement ajouter une authentification à vos applications de bureau avec la prise en charge des comptes Microsoft personnels, ainsi que les comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="09513-104">With the the v2.0 endpoint, you can quickly add authentication to your desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="09513-105">Il permet également à votre application de communiquer de manière sécurisée avec une API web principale, ainsi qu’avec [Microsoft Graph](https://graph.microsoft.io) et un nombre limité [d’API unifiées Office 365](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="09513-105">It also enables your app to securely communicate with a backend web api, as well as [the Microsoft Graph](https://graph.microsoft.io) and a few of the [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="09513-106">Les scénarios et les fonctionnalités Azure Active Directory (AD) ne sont pas tous pris en charge par le point de terminaison v2.0.</span><span class="sxs-lookup"><span data-stu-id="09513-106">Not all Azure Active Directory (AD) scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="09513-107">Pour déterminer si vous devez utiliser le point de terminaison v2.0, consultez les [limitations de v2.0](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="09513-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="09513-108">Pour les [applications natives .NET qui s’exécutent sur un appareil](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD fournit la bibliothèque d’authentification Microsoft Identity (bibliothèque MSAL).</span><span class="sxs-lookup"><span data-stu-id="09513-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides the Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="09513-109">Le seul objectif de cette bibliothèque MSAL est de faciliter l’obtention de jetons pour votre application, qui les utilise pour appeler les services Web.</span><span class="sxs-lookup"><span data-stu-id="09513-109">MSAL's sole purpose in life is to make it easy for your app to get tokens for calling web services.</span></span>  <span data-ttu-id="09513-110">Pour illustrer sa facilité d’utilisation, nous allons créer une application de liste des tâches .NET WPF qui exécute les activités suivantes :</span><span class="sxs-lookup"><span data-stu-id="09513-110">To demonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="09513-111">connexion de l’utilisateur et obtention des jetons d’accès à l’aide du [protocole d’authentification OAuth 2.0](active-directory-v2-protocols.md) ;</span><span class="sxs-lookup"><span data-stu-id="09513-111">Signs the user in & gets access tokens using the [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="09513-112">appel sécurisé d’un service Web principal de liste de tâches, qui est également sécurisé par OAuth 2.0 ;</span><span class="sxs-lookup"><span data-stu-id="09513-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="09513-113">déconnexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09513-113">Signs the user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="09513-114">Télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="09513-114">Download sample code</span></span>
<span data-ttu-id="09513-115">Le code associé à ce didacticiel est stocké [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="09513-115">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="09513-116">Pour suivre la procédure, vous pouvez [télécharger la structure de l’application au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ou la cloner :</span><span class="sxs-lookup"><span data-stu-id="09513-116">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone the skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="09513-117">L'application terminée est également fournie à la fin de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="09513-117">The completed app is provided at the end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="09513-118">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="09513-118">Register an app</span></span>
<span data-ttu-id="09513-119">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="09513-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="09513-120">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="09513-120">Make sure to:</span></span>

* <span data-ttu-id="09513-121">copier l' **ID d'application** attribué à votre application, vous en aurez bientôt besoin ;</span><span class="sxs-lookup"><span data-stu-id="09513-121">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="09513-122">ajouter la plateforme **Mobile** pour votre application ;</span><span class="sxs-lookup"><span data-stu-id="09513-122">Add the **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="09513-123">Installation et configuration de la bibliothèque MSAL</span><span class="sxs-lookup"><span data-stu-id="09513-123">Install & Configure MSAL</span></span>
<span data-ttu-id="09513-124">Maintenant que vous disposez d’une application enregistrée auprès de Microsoft, vous pouvez installer la bibliothèque MSAL et écrire votre code associé aux identités.</span><span class="sxs-lookup"><span data-stu-id="09513-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="09513-125">Pour permettre à la bibliothèque MSAL de communiquer avec le point de terminaison v2.0, vous devez lui fournir des informations sur l’enregistrement de votre application.</span><span class="sxs-lookup"><span data-stu-id="09513-125">In order for MSAL to be able to communicate the v2.0 endpoint, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="09513-126">Commencez par ajouter la bibliothèque MSAL au projet TodoListClient à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="09513-126">Begin by adding MSAL to the TodoListClient project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="09513-127">Dans le projet TodoListClient, ouvrez `app.config`.</span><span class="sxs-lookup"><span data-stu-id="09513-127">In the TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="09513-128">Remplacez les valeurs des éléments de la section `<appSettings>` afin qu’elles reflètent les valeurs saisies dans le portail d’inscription d’applications.</span><span class="sxs-lookup"><span data-stu-id="09513-128">Replace the values of the elements in the `<appSettings>` section to reflect the values you input into the app registration portal.</span></span>  <span data-ttu-id="09513-129">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque MSAL.</span><span class="sxs-lookup"><span data-stu-id="09513-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="09513-130">L’élément `ida:ClientId` est l’ **ID d’application** de l’application copiée à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="09513-130">The `ida:ClientId` is the **Application Id** of your app you copied from the portal.</span></span>
* <span data-ttu-id="09513-131">Dans le projet TodoList-Service, ouvrez l’élément `web.config` dans la racine du projet.</span><span class="sxs-lookup"><span data-stu-id="09513-131">In the TodoList-Service project, open `web.config` in the root of the project.</span></span>  
  
  * <span data-ttu-id="09513-132">Remplacez la valeur `ida:Audience` par l’ **ID d’application** du portail.</span><span class="sxs-lookup"><span data-stu-id="09513-132">Replace the `ida:Audience` value with the same **Application Id** from the portal.</span></span>

## <a name="use-msal-to-get-tokens"></a><span data-ttu-id="09513-133">Utilisation de la bibliothèque MSAL pour obtenir des jetons</span><span class="sxs-lookup"><span data-stu-id="09513-133">Use MSAL to get tokens</span></span>
<span data-ttu-id="09513-134">Le principe de base de la bibliothèque MSAL consiste simplement à appeler `app.AcquireToken(...)`chaque fois que votre application a besoin d’un jeton d’accès, et la bibliothèque MSAL s’occupe du reste.</span><span class="sxs-lookup"><span data-stu-id="09513-134">The basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does the rest.</span></span>  

* <span data-ttu-id="09513-135">Dans le projet `TodoListClient`, ouvrez `MainWindow.xaml.cs` et recherchez la méthode `OnInitialized(...)`.</span><span class="sxs-lookup"><span data-stu-id="09513-135">In the `TodoListClient` project, open `MainWindow.xaml.cs` and locate the `OnInitialized(...)` method.</span></span>  <span data-ttu-id="09513-136">La première étape consiste à initialiser la `PublicClientApplication` de votre application, c’est-à-dire la classe principale de la bibliothèque MSAL représentant les applications natives.</span><span class="sxs-lookup"><span data-stu-id="09513-136">The first step is to initialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="09513-137">C’est à ce moment-là que vous fournissez à la bibliothèque MSAL les coordonnées dont elle a besoin pour communiquer avec Azure AD et lui indiquer comment mettre en cache des jetons.</span><span class="sxs-lookup"><span data-stu-id="09513-137">This is where you pass MSAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="09513-138">Lorsque l’application démarre, nous souhaitons vérifier si l’utilisateur est déjà connecté.</span><span class="sxs-lookup"><span data-stu-id="09513-138">When the app starts up, we want to check and see if the user is already signed into the app.</span></span>  <span data-ttu-id="09513-139">Toutefois, nous ne voulons pas encore invoquer d’interface utilisateur de connexion. Nous demanderons à l’utilisateur de cliquer sur l’option de connexion.</span><span class="sxs-lookup"><span data-stu-id="09513-139">However, we don't want to invoke a sign-in UI just yet - we'll make the user click "Sign In" to do so.</span></span>  <span data-ttu-id="09513-140">Également dans la méthode `OnInitialized(...)` :</span><span class="sxs-lookup"><span data-stu-id="09513-140">Also in the `OnInitialized(...)` method:</span></span>

```C#
// As the app starts, we want to check to see if the user is already signed in.
// You can do so by trying to get a token from MSAL, using the method
// AcquireTokenSilent.  This forces MSAL to throw an exception if it cannot
// get a token for the user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in the cache - or MSAL was able to get a new oen via refresh token.
    // Proceed to fetch the user's tasks from the TodoListService via the GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, the app should take no action,
        // and simply show the user the sign in button.
    }
    else
    {
        // Here, we catch all other MsalExceptions
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }
}

```

* <span data-ttu-id="09513-141">Si l’utilisateur, non connecté, clique sur le bouton de connexion, nous souhaitons invoquer une interface utilisateur de connexion et lui demander de saisir ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="09513-141">If the user is not signed in and they click the "Sign In" button, we want to invoke a login UI and have the user enter their credentials.</span></span>  <span data-ttu-id="09513-142">Implémentez le gestionnaire du bouton de connexion :</span><span class="sxs-lookup"><span data-stu-id="09513-142">Implement the Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign the user out if they clicked the "Clear Cache" button

// If the user clicked the 'Sign-In' button, force
// MSAL to prompt the user for credentials by using
// AcquireTokenAsync, a method that is guaranteed to show a prompt to the user.
// MSAL will get a token for the TodoListService and cache it for you.

AuthenticationResult result = null;
try
{
    result = await app.AcquireTokenAsync(new string[] { clientId });
    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    // If MSAL cannot get a token, it will throw an exception.
    // If the user canceled the login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by the user");
    }
    else
    {
        // An unexpected error occurred.
        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }

        MessageBox.Show(message);
    }

    return;
}


}
```

* <span data-ttu-id="09513-143">Si l’utilisateur parvient à se connecter, la bibliothèque MSAL reçoit et met en cache un jeton pour vous. Vous pouvez appeler la méthode `GetTodoList()` en toute confiance.</span><span class="sxs-lookup"><span data-stu-id="09513-143">If the user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed to call the `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="09513-144">Pour récupérer les tâches d’un utilisateur, il ne vous reste plus qu’à implémenter la méthode `GetTodoList()`.</span><span class="sxs-lookup"><span data-stu-id="09513-144">All that's left to get a user's tasks is to implement the `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try to get an access token to call the TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL to throw an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show the user a message
    // and let them click the Sign-In button.

    if (ex.ErrorCode == "user_interaction_required")
    {
        MessageBox.Show("Please sign in first");
        SignInButton.Content = "Sign In";
    }
    else
    {
        // In any other case, an unexpected error occurred.

        string message = ex.Message;
        if (ex.InnerException != null)
        {
            message += "Inner Exception : " + ex.InnerException.Message;
        }
        MessageBox.Show(message);
    }

    return;
}

// Once the token has been returned by MSAL,
// add it to the http authorization header,
// before making the call to access the To Do list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When the user is done managing their To-Do List, they may finally sign out of the app by clicking the "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If the user clicked the 'clear cache' button,
        // clear the MSAL token cache and show the user as signed out.
        // It's also necessary to clear the cookies from the browser
        // control so the next user has a chance to sign in.

        if (SignInButton.Content.ToString() == "Clear Cache")
        {
                TodoList.ItemsSource = string.Empty;
                app.UserTokenCache.Clear(app.ClientId);
                ClearCookies();
                SignInButton.Content = "Sign In";
                return;
        }

        ...
```

## <a name="run"></a><span data-ttu-id="09513-145">Exécuter</span><span class="sxs-lookup"><span data-stu-id="09513-145">Run</span></span>
<span data-ttu-id="09513-146">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="09513-146">Congratulations!</span></span> <span data-ttu-id="09513-147">Vous disposez désormais d’une application .NET WPF fonctionnelle, capable d’authentifier les utilisateurs et d’appeler des API web en toute sécurité via OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="09513-147">You now have a working .NET WPF app that has the ability to authenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="09513-148">Exécutez vos projets et connectez-vous avec un compte Microsoft personnel ou un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="09513-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="09513-149">Ajoutez des tâches à la liste de tâches de cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09513-149">Add tasks to that user's To-Do list.</span></span>  <span data-ttu-id="09513-150">Déconnectez-vous et reconnectez-vous à l'aide du compte d'un autre utilisateur pour afficher sa liste de tâches. </span><span class="sxs-lookup"><span data-stu-id="09513-150">Sign out, and sign back in as another user to view their To-Do list.</span></span>  <span data-ttu-id="09513-151">Fermez l’application et exécutez-la de nouveau.</span><span class="sxs-lookup"><span data-stu-id="09513-151">Close the app, and re-run it.</span></span>  <span data-ttu-id="09513-152">Remarquez à quel point la session de l’utilisateur reste intacte (cela s’explique par le fait que l’application cache des jetons dans un fichier local).</span><span class="sxs-lookup"><span data-stu-id="09513-152">Notice how the user's session remains intact - that is because the app caches tokens in a local file.</span></span>

<span data-ttu-id="09513-153">La bibliothèque MSAL permet d’intégrer facilement des fonctionnalités d’identité courantes à votre application à l’aide de vos comptes personnels et professionnels.</span><span class="sxs-lookup"><span data-stu-id="09513-153">MSAL makes it easy to incorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="09513-154">Elle effectue les tâches ingrates pour vous : gestion du cache, prise en charge du protocole OAuth, présentation d’une interface utilisateur de connexion à l’utilisateur, actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="09513-154">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="09513-155">La seule chose que vous devez vraiment connaître est un appel unique d’API : `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="09513-155">All you really need to know is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="09513-156">Pour référence, l’exemple terminé (sans vos valeurs de configuration) [est fourni ici au format .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip). Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="09513-156">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="09513-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09513-157">Next steps</span></span>
<span data-ttu-id="09513-158">Vous pouvez maintenant aborder des rubriques plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="09513-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="09513-159">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="09513-159">You may want to try:</span></span>

* [<span data-ttu-id="09513-160">Sécurisation de l’API web TodoListService avec le point de terminaison v2.0</span><span class="sxs-lookup"><span data-stu-id="09513-160">Securing the TodoListService Web API with the v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="09513-161">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="09513-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="09513-162">Guide du développeur 2.0 >></span><span class="sxs-lookup"><span data-stu-id="09513-162">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="09513-163">Balise « msal » StackOverflow >></span><span class="sxs-lookup"><span data-stu-id="09513-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="09513-164">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="09513-164">Get security updates for our products</span></span>
<span data-ttu-id="09513-165">Nous vous encourageons à activer les notifications d’incidents de sécurité en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et en vous abonnant aux alertes d’avis de sécurité.</span><span class="sxs-lookup"><span data-stu-id="09513-165">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

