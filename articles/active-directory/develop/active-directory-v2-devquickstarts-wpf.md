---
title: aaaAzure Active Directory v2.0 application Native .NET | Documents Microsoft
description: Comment toobuild une application native .NET qui connecte aux utilisateurs avec les deux Account personnel de Microsoft et comptes professionnels ou scolaires.
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
ms.openlocfilehash: 9418eeba02b800feee5cb00219574eb16506f0a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-tooa-windows-desktop-app"></a><span data-ttu-id="14520-103">Ajouter une application de bureau Windows de connexion tooa</span><span class="sxs-lookup"><span data-stu-id="14520-103">Add sign-in tooa Windows Desktop app</span></span>
<span data-ttu-id="14520-104">Avec le point de terminaison hello hello v2.0, vous pouvez ajouter rapidement des applications de bureau tooyour l’authentification avec prise en charge pour les deux comptes personnels de Microsoft et comptes professionnels ou scolaires.</span><span class="sxs-lookup"><span data-stu-id="14520-104">With hello hello v2.0 endpoint, you can quickly add authentication tooyour desktop apps with support for both personal Microsoft accounts and work or school accounts.</span></span>  <span data-ttu-id="14520-105">Elle aussi Active toosecurely de votre application communiquer avec un service principal web api, ainsi que [hello Microsoft Graph](https://graph.microsoft.io) et quelques exemples de hello [les API Office 365 unifiée](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span><span class="sxs-lookup"><span data-stu-id="14520-105">It also enables your app toosecurely communicate with a backend web api, as well as [hello Microsoft Graph](https://graph.microsoft.io) and a few of hello [Office 365 Unified APIs](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2).</span></span>

> [!NOTE]
> <span data-ttu-id="14520-106">Pas toutes les fonctionnalités et scénarios d’Azure Active Directory (AD) sont pris en charge par le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="14520-106">Not all Azure Active Directory (AD) scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="14520-107">toodetermine si vous devez utiliser le point de terminaison hello v2.0, en savoir plus sur [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="14520-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="14520-108">Pour [.NET des applications natives qui s’exécutent sur un appareil](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD fournit hello bibliothèque d’authentification d’identité ou MSAL.</span><span class="sxs-lookup"><span data-stu-id="14520-108">For [.NET native apps that run on a device](active-directory-v2-flows.md#mobile-and-native-apps), Azure AD provides hello Microsoft Identity Authentication Library, or MSAL.</span></span>  <span data-ttu-id="14520-109">Seul but de MSAL vie est toomake tooget de votre application plus facilement des jetons pour appeler des services web.</span><span class="sxs-lookup"><span data-stu-id="14520-109">MSAL's sole purpose in life is toomake it easy for your app tooget tokens for calling web services.</span></span>  <span data-ttu-id="14520-110">toodemonstrate facilité il s’agit, ici nous allons construire une application de liste de tâches WPF .NET :</span><span class="sxs-lookup"><span data-stu-id="14520-110">toodemonstrate just how easy it is, here we'll build a .NET WPF To-Do List app that:</span></span>

* <span data-ttu-id="14520-111">Signes hello utilisateur dans & obtient accéder aux jetons à l’aide de hello [protocole d’authentification OAuth 2.0](active-directory-v2-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="14520-111">Signs hello user in & gets access tokens using hello [OAuth 2.0 authentication protocol](active-directory-v2-protocols.md).</span></span>
* <span data-ttu-id="14520-112">appel sécurisé d’un service Web principal de liste de tâches, qui est également sécurisé par OAuth 2.0 ;</span><span class="sxs-lookup"><span data-stu-id="14520-112">Securely calls a backend To-Do List web service, which is also secured by OAuth 2.0.</span></span>
* <span data-ttu-id="14520-113">Utilisateur se connecte hello out.</span><span class="sxs-lookup"><span data-stu-id="14520-113">Signs hello user out.</span></span>

## <a name="download-sample-code"></a><span data-ttu-id="14520-114">Télécharger l’exemple de code</span><span class="sxs-lookup"><span data-stu-id="14520-114">Download sample code</span></span>
<span data-ttu-id="14520-115">code Hello pour ce didacticiel est maintenue [sur GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="14520-115">hello code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet).</span></span>  <span data-ttu-id="14520-116">toofollow le long, vous pouvez [structure de l’application hello en tant qu’un fichier ZIP de téléchargement](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) ou un clone hello squelette :</span><span class="sxs-lookup"><span data-stu-id="14520-116">toofollow along, you can [download hello app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/skeleton.zip) or clone hello skeleton:</span></span>

    git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git

<span data-ttu-id="14520-117">application Hello terminée est fournie à des fin de hello de ce didacticiel également.</span><span class="sxs-lookup"><span data-stu-id="14520-117">hello completed app is provided at hello end of this tutorial as well.</span></span>

## <a name="register-an-app"></a><span data-ttu-id="14520-118">Inscription d’une application</span><span class="sxs-lookup"><span data-stu-id="14520-118">Register an app</span></span>
<span data-ttu-id="14520-119">Créez une application à l’adresse [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), ou suivez cette [procédure détaillée](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="14520-119">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="14520-120">Veillez à respecter les points suivants :</span><span class="sxs-lookup"><span data-stu-id="14520-120">Make sure to:</span></span>

* <span data-ttu-id="14520-121">Copie vers le bas hello **Id d’Application** affecté tooyour application, vous en aurez besoin plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="14520-121">Copy down hello **Application Id** assigned tooyour app, you'll need it soon.</span></span>
* <span data-ttu-id="14520-122">Ajouter hello **Mobile** plate-forme pour votre application.</span><span class="sxs-lookup"><span data-stu-id="14520-122">Add hello **Mobile** platform for your app.</span></span>

## <a name="install--configure-msal"></a><span data-ttu-id="14520-123">Installation et configuration de la bibliothèque MSAL</span><span class="sxs-lookup"><span data-stu-id="14520-123">Install & Configure MSAL</span></span>
<span data-ttu-id="14520-124">Maintenant que vous disposez d’une application enregistrée auprès de Microsoft, vous pouvez installer la bibliothèque MSAL et écrire votre code associé aux identités.</span><span class="sxs-lookup"><span data-stu-id="14520-124">Now that you have an app registered with Microsoft, you can install MSAL and write your identity-related code.</span></span>  <span data-ttu-id="14520-125">Point de terminaison MSAL toobe toocommunicate en mesure de hello v2.0, vous devez tooprovide avec des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="14520-125">In order for MSAL toobe able toocommunicate hello v2.0 endpoint, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="14520-126">Commencez par ajouter le projet de TodoListClient toohello MSAL à l’aide de la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="14520-126">Begin by adding MSAL toohello TodoListClient project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -ProjectName TodoListClient -IncludePrerelease
```

* <span data-ttu-id="14520-127">Dans le projet de TodoListClient hello, ouvrez `app.config`.</span><span class="sxs-lookup"><span data-stu-id="14520-127">In hello TodoListClient project, open `app.config`.</span></span>  <span data-ttu-id="14520-128">Remplacez les valeurs hello d’éléments hello Bonjour `<appSettings>` hello tooreflect de section les valeurs d’entrée dans le portail de l’enregistrement d’application hello.</span><span class="sxs-lookup"><span data-stu-id="14520-128">Replace hello values of hello elements in hello `<appSettings>` section tooreflect hello values you input into hello app registration portal.</span></span>  <span data-ttu-id="14520-129">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque MSAL.</span><span class="sxs-lookup"><span data-stu-id="14520-129">Your code will reference these values whenever it uses MSAL.</span></span>
  
  * <span data-ttu-id="14520-130">Hello `ida:ClientId` est hello **Id d’Application** de votre application que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="14520-130">hello `ida:ClientId` is hello **Application Id** of your app you copied from hello portal.</span></span>
* <span data-ttu-id="14520-131">Dans le projet de hello TodoList-Service, ouvrez `web.config` dans racine hello du projet de hello.</span><span class="sxs-lookup"><span data-stu-id="14520-131">In hello TodoList-Service project, open `web.config` in hello root of hello project.</span></span>  
  
  * <span data-ttu-id="14520-132">Remplacez hello `ida:Audience` valeur hello même **Id de l’Application** à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="14520-132">Replace hello `ida:Audience` value with hello same **Application Id** from hello portal.</span></span>

## <a name="use-msal-tooget-tokens"></a><span data-ttu-id="14520-133">Utiliser des jetons de tooget MSAL</span><span class="sxs-lookup"><span data-stu-id="14520-133">Use MSAL tooget tokens</span></span>
<span data-ttu-id="14520-134">Bonjour derrière MSAL principe de base est que chaque fois que votre application a besoin d’un jeton d’accès, il suffit d’appeler `app.AcquireToken(...)`, et MSAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="14520-134">hello basic principle behind MSAL is that whenever your app needs an access token, you simply call `app.AcquireToken(...)`, and MSAL does hello rest.</span></span>  

* <span data-ttu-id="14520-135">Bonjour `TodoListClient` projet, ouvrez `MainWindow.xaml.cs` et recherchez hello `OnInitialized(...)` (méthode).</span><span class="sxs-lookup"><span data-stu-id="14520-135">In hello `TodoListClient` project, open `MainWindow.xaml.cs` and locate hello `OnInitialized(...)` method.</span></span>  <span data-ttu-id="14520-136">première étape de Hello est tooinitialize de votre application `PublicClientApplication` -classe de principal du MSAL représentant des applications natives.</span><span class="sxs-lookup"><span data-stu-id="14520-136">hello first step is tooinitialize your app's `PublicClientApplication` - MSAL's primary class representing native applications.</span></span>  <span data-ttu-id="14520-137">Il s’agit d’où vous passez MSAL hello coordonnées nécessaires toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.</span><span class="sxs-lookup"><span data-stu-id="14520-137">This is where you pass MSAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
protected override async void OnInitialized(EventArgs e)
{
        base.OnInitialized(e);

        app = new PublicClientApplication(new FileCache());
        AuthenticationResult result = null;
        ...
}
```

* <span data-ttu-id="14520-138">Lors de l’application hello démarre, toocheck et nous voir si hello utilisateur est déjà connecté à application hello.</span><span class="sxs-lookup"><span data-stu-id="14520-138">When hello app starts up, we want toocheck and see if hello user is already signed into hello app.</span></span>  <span data-ttu-id="14520-139">Toutefois, nous ne voulons pas encore tooinvoke une interface utilisateur de l’authentification : nous allons effectuer les utilisateur hello cliquez sur « Sign In » toodo donc.</span><span class="sxs-lookup"><span data-stu-id="14520-139">However, we don't want tooinvoke a sign-in UI just yet - we'll make hello user click "Sign In" toodo so.</span></span>  <span data-ttu-id="14520-140">Également dans hello `OnInitialized(...)` méthode :</span><span class="sxs-lookup"><span data-stu-id="14520-140">Also in hello `OnInitialized(...)` method:</span></span>

```C#
// As hello app starts, we want toocheck toosee if hello user is already signed in.
// You can do so by trying tooget a token from MSAL, using hello method
// AcquireTokenSilent.  This forces MSAL toothrow an exception if it cannot
// get a token for hello user without showing a UI.
try
{
    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
    // If we got here, a valid token is in hello cache - or MSAL was able tooget a new oen via refresh token.
    // Proceed toofetch hello user's tasks from hello TodoListService via hello GetTodoList() method.

    SignInButton.Content = "Clear Cache";
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "user_interaction_required")
    {
        // If user interaction is required, hello app should take no action,
        // and simply show hello user hello sign in button.
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

* <span data-ttu-id="14520-141">Si l’utilisateur de hello n’est pas connecté et ils cliquent sur hello » bouton se connecter », nous tooinvoke une interface utilisateur de connexion et souhaitez utilisateur de hello entrer leurs informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="14520-141">If hello user is not signed in and they click hello "Sign In" button, we want tooinvoke a login UI and have hello user enter their credentials.</span></span>  <span data-ttu-id="14520-142">Implémenter le Gestionnaire du bouton hello-In :</span><span class="sxs-lookup"><span data-stu-id="14520-142">Implement hello Sign-In button handler:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // TODO: Sign hello user out if they clicked hello "Clear Cache" button

// If hello user clicked hello 'Sign-In' button, force
// MSAL tooprompt hello user for credentials by using
// AcquireTokenAsync, a method that is guaranteed tooshow a prompt toohello user.
// MSAL will get a token for hello TodoListService and cache it for you.

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
    // If hello user canceled hello login, it will result in the
    // error code 'authentication_canceled'.

    if (ex.ErrorCode == "authentication_canceled")
    {
        MessageBox.Show("Sign in was canceled by hello user");
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

* <span data-ttu-id="14520-143">Si hello correctement les signes de l’utilisateur, MSAL recevra et mettre en cache un jeton pour vous et vous pouvez passer toocall hello `GetTodoList()` méthode en toute confiance.</span><span class="sxs-lookup"><span data-stu-id="14520-143">If hello user successfully signs-in, MSAL will receive and cache a token for you, and you can proceed toocall hello `GetTodoList()` method with confidence.</span></span>  <span data-ttu-id="14520-144">Tout ce qui l’a laissé tooget les tâches d’un utilisateur est tooimplement hello `GetTodoList()` (méthode).</span><span class="sxs-lookup"><span data-stu-id="14520-144">All that's left tooget a user's tasks is tooimplement hello `GetTodoList()` method.</span></span>

```C#
private async void GetTodoList()
{

AuthenticationResult result = null;
try
{
    // Here, we try tooget an access token toocall hello TodoListService
    // without invoking any UI prompt.  AcquireTokenSilentAsync forces
    // MSAL toothrow an exception if it cannot get a token silently.


    result = await app.AcquireTokenSilentAsync(new string[] { clientId });
}
catch (MsalException ex)
{
    // MSAL couldn't get a token silently, so show hello user a message
    // and let them click hello Sign-In button.

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

// Once hello token has been returned by MSAL,
// add it toohello http authorization header,
// before making hello call tooaccess hello tooDo list service.

httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);


        ...
...


- When hello user is done managing their To-Do List, they may finally sign out of hello app by clicking hello "Clear Cache" button.

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
        // If hello user clicked hello 'clear cache' button,
        // clear hello MSAL token cache and show hello user as signed out.
        // It's also necessary tooclear hello cookies from hello browser
        // control so hello next user has a chance toosign in.

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

## <a name="run"></a><span data-ttu-id="14520-145">Exécuter</span><span class="sxs-lookup"><span data-stu-id="14520-145">Run</span></span>
<span data-ttu-id="14520-146">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="14520-146">Congratulations!</span></span> <span data-ttu-id="14520-147">Vous maintenant disposerez d’une application WPF .NET qui a des utilisateurs tooauthenticate hello capacité & appelez en toute sécurité des API Web à l’aide d’OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="14520-147">You now have a working .NET WPF app that has hello ability tooauthenticate users & securely call Web APIs using OAuth 2.0.</span></span>  <span data-ttu-id="14520-148">Exécutez vos projets et connectez-vous avec un compte Microsoft personnel ou un compte professionnel ou scolaire.</span><span class="sxs-lookup"><span data-stu-id="14520-148">Run your both projects, and sign in with either a personal Microsoft account or a work or school account.</span></span>  <span data-ttu-id="14520-149">Ajouter la liste des tâches de l’utilisateur toothat de tâches.</span><span class="sxs-lookup"><span data-stu-id="14520-149">Add tasks toothat user's To-Do list.</span></span>  <span data-ttu-id="14520-150">Déconnectez-vous et reconnectez-vous en tant qu’un autre utilisateur tooview leur liste de tâches.</span><span class="sxs-lookup"><span data-stu-id="14520-150">Sign out, and sign back in as another user tooview their To-Do list.</span></span>  <span data-ttu-id="14520-151">Fermez l’application hello et réexécutez-la.</span><span class="sxs-lookup"><span data-stu-id="14520-151">Close hello app, and re-run it.</span></span>  <span data-ttu-id="14520-152">Notez comment de hello session reste intacte, c’est parce que l’application hello met en cache des jetons dans un fichier local.</span><span class="sxs-lookup"><span data-stu-id="14520-152">Notice how hello user's session remains intact - that is because hello app caches tokens in a local file.</span></span>

<span data-ttu-id="14520-153">MSAL rend fonctionnalités d’identité commune tooincorporate facile dans votre application, à l’aide des comptes personnels et professionnels.</span><span class="sxs-lookup"><span data-stu-id="14520-153">MSAL makes it easy tooincorporate common identity features into your app, using both personal and work accounts.</span></span>  <span data-ttu-id="14520-154">Il s’occupe de tout le travail dirty hello vous - gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="14520-154">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="14520-155">Vous devez vraiment tooknow est un simple appel d’API `app.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="14520-155">All you really need tooknow is a single API call, `app.AcquireTokenAsync(...)`.</span></span>

<span data-ttu-id="14520-156">Pour référence, hello effectuée exemple (sans les valeurs de configuration) [est fournie en tant qu’un fichier zip ici](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), ou vous pouvez le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="14520-156">For reference, hello completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-NativeClient-DotNet.git```

## <a name="next-steps"></a><span data-ttu-id="14520-157">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="14520-157">Next steps</span></span>
<span data-ttu-id="14520-158">Vous pouvez maintenant aborder des rubriques plus sophistiquées.</span><span class="sxs-lookup"><span data-stu-id="14520-158">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="14520-159">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="14520-159">You may want tootry:</span></span>

* [<span data-ttu-id="14520-160">Sécurisation de hello TodoListService Web API avec le point de terminaison hello v2.0</span><span class="sxs-lookup"><span data-stu-id="14520-160">Securing hello TodoListService Web API with hello v2.0 endpoint</span></span>](active-directory-v2-devquickstarts-dotnet-api.md)

<span data-ttu-id="14520-161">Pour obtenir des ressources supplémentaires, consultez :</span><span class="sxs-lookup"><span data-stu-id="14520-161">For additional resources, check out:</span></span>  

* [<span data-ttu-id="14520-162">guide du développeur v2.0 Hello >></span><span class="sxs-lookup"><span data-stu-id="14520-162">hello v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="14520-163">Balise « msal » StackOverflow &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="14520-163">StackOverflow "msal" tag >></span></span>](http://stackoverflow.com/questions/tagged/msal)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="14520-164">Obtenir les mises à jour de sécurité de nos produits</span><span class="sxs-lookup"><span data-stu-id="14520-164">Get security updates for our products</span></span>
<span data-ttu-id="14520-165">Nous vous conseillons de notifications tooget les incidents de sécurité se produire en vous rendant sur [cette page](https://technet.microsoft.com/security/dd252948) et l’abonnement d’alerte tooSecurity.</span><span class="sxs-lookup"><span data-stu-id="14520-165">We encourage you tooget notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing tooSecurity Advisory Alerts.</span></span>

