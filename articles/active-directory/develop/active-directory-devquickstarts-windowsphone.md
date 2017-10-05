---
title: "Bien démarrer avec Azure AD Windows Phone | Microsoft Docs"
description: "Création d’une application Windows Phone qui s’intègre avec Azure AD pour la connexion et appelle des API protégées par Azure AD en utilisant OAuth"
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 66f5ac20-5e1f-4b9d-bb99-9b3305e26416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 03c4b6d225dce99d79ef6c1ba2af43af8dea3eae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="24f03-103">Intégration d’Azure AD avec une application Windows Phone</span><span class="sxs-lookup"><span data-stu-id="24f03-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="24f03-104">Les projets du Windows Phone 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="24f03-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="24f03-105">Pour en savoir plus, consultez [Ciblage et compatibilité de la plateforme Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="24f03-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="24f03-106">Si vous développez une application Windows Phone 8.1, Azure AD facilite l’authentification de vos utilisateurs avec leurs comptes Active Directory.</span><span class="sxs-lookup"><span data-stu-id="24f03-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you to authenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="24f03-107">Il permet également à votre application d’utiliser en toute sécurité une API web protégée par Azure AD, telle que l’API Office 365 ou Azure.</span><span class="sxs-lookup"><span data-stu-id="24f03-107">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="24f03-108">Cet exemple de code utilise la bibliothèque ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="24f03-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="24f03-109">Pour utiliser les dernières technologies, vous souhaiterez peut-être plutôt essayer notre [Didacticiel universel Windows avec ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="24f03-109">For the latest technology, you may want to instead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="24f03-110">Si vous créez une application pour Windows Phone 8.1, vous êtes au bon endroit.</span><span class="sxs-lookup"><span data-stu-id="24f03-110">If you are indeed building an app for Windows Phone 8.1, this is the right place.</span></span>  <span data-ttu-id="24f03-111">ADAL v2.0 est entièrement pris en charge. C’est la méthode recommandée pour le développement d’applications, par rapport à Windows Phone 8.1 avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24f03-111">ADAL v2.0 is still fully supported, and is the recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="24f03-112">Pour les clients natifs .NET qui doivent accéder à des ressources protégées, Azure AD fournit la bibliothèque d’authentification Active Directory (bibliothèque ADAL).</span><span class="sxs-lookup"><span data-stu-id="24f03-112">For .NET native clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="24f03-113">Le seul objectif de cette bibliothèque ADAL est de faciliter l’obtention des jetons d'accès pour votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-113">ADAL’s sole purpose in life is to make it easy for your app to get access tokens.</span></span>  <span data-ttu-id="24f03-114">Pour illustrer cette simplicité, nous créerons une application Windows Phone 8.1 « Directory Searcher » effectuant les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="24f03-114">To demonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="24f03-115">obtention de jetons d’accès pour appeler l’API Azure AD Graph à l’aide du [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx);</span><span class="sxs-lookup"><span data-stu-id="24f03-115">Gets access tokens for calling the Azure AD Graph API using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="24f03-116">recherche, dans un répertoire, d’utilisateurs correspondant à un UPN (nom d’utilisateur principal) donné.</span><span class="sxs-lookup"><span data-stu-id="24f03-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="24f03-117">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="24f03-117">Signs users out.</span></span>

<span data-ttu-id="24f03-118">Pour générer l’application fonctionnelle complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="24f03-118">To build the complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="24f03-119">inscrire votre application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="24f03-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="24f03-120">installer et configurer la bibliothèque ADAL ;</span><span class="sxs-lookup"><span data-stu-id="24f03-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="24f03-121">utiliser la bibliothèque ADAL pour obtenir des jetons à partir d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24f03-121">Use ADAL to get tokens from Azure AD.</span></span>

<span data-ttu-id="24f03-122">Pour commencer, téléchargez [la structure du projet](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="24f03-122">To get started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download the completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="24f03-123">Chaque option est une solution Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="24f03-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="24f03-124">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="24f03-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="24f03-125">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="24f03-125">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-the-directory-searcher-application"></a><span data-ttu-id="24f03-126">1. Inscription de l’application Directory Searcher</span><span class="sxs-lookup"><span data-stu-id="24f03-126">1. Register the Directory Searcher Application</span></span>
<span data-ttu-id="24f03-127">Pour autoriser votre application à obtenir des jetons, vous devez tout d’abord l’inscrire dans votre client Azure AD et lui accorder l’autorisation d’accéder à l’API Graph Azure AD :</span><span class="sxs-lookup"><span data-stu-id="24f03-127">To enable your app to get tokens, you’ll first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API:</span></span>

1. <span data-ttu-id="24f03-128">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="24f03-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="24f03-129">Dans la barre supérieure, cliquez sur votre compte et, dans la liste **Répertoire**, choisissez le locataire Active Directory auprès duquel vous voulez inscrire votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-129">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="24f03-130">Cliquez sur **Autres services** dans le volet de navigation gauche et choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="24f03-130">Click on **More Services** in the left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="24f03-131">Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="24f03-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="24f03-132">Suivez les invites et créez une **application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="24f03-132">Follow the prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="24f03-133">Le **nom** de l’application doit décrire votre application aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="24f03-133">The **Name** of the application will describe your application to end-users</span></span>
  * <span data-ttu-id="24f03-134">L’ **URI de redirection** est une combinaison de schémas et de chaînes qu’Azure AD utilise pour renvoyer des réponses concernant les jetons.</span><span class="sxs-lookup"><span data-stu-id="24f03-134">The **Redirect Uri** is a scheme and string combination that Azure AD will use to return token responses.</span></span>  <span data-ttu-id="24f03-135">Entrez temporairement une valeur d’espace réservé, par exemple, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="24f03-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="24f03-136">Nous remplacerons cette valeur ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="24f03-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="24f03-137">Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="24f03-138">Copiez cette valeur sous l’onglet de l’application, car vous en aurez besoin dans les sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="24f03-138">You’ll need this value in the next sections, so copy it from the application tab.</span></span>
7. <span data-ttu-id="24f03-139">Sur la page **Paramètres**, choisissez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="24f03-139">From the **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="24f03-140">Sélectionnez l’API **Microsoft Graph** et ajoutez l’autorisation **Lire les données de l’annuaire** sous **Autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="24f03-140">Select the **Microsoft Graph** as the API and add the **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="24f03-141">Cela permet à votre application d’interroger l’API Graph concernant les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="24f03-141">This will enable your application to query the Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="24f03-142">2. Installez et configurez ADAL</span><span class="sxs-lookup"><span data-stu-id="24f03-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="24f03-143">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="24f03-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="24f03-144">Pour permettre à ADAL de communiquer avec Azure AD, vous devez lui fournir des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-144">In order for ADAL to be able to communicate with Azure AD, you need to provide it with some information about your app registration.</span></span>

* <span data-ttu-id="24f03-145">Commencez par ajouter ADAL au projet DirectorySearcher à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="24f03-145">Begin by adding ADAL to the DirectorySearcher project using the Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="24f03-146">Dans le projet DirectorySearcher, ouvrez `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="24f03-146">In the DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="24f03-147">Remplacez les valeurs dans la zone `Config Values` afin de refléter les valeurs que vous avez saisies dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="24f03-147">Replace the values in the `Config Values` region to reflect the values you input into the Azure Portal.</span></span>  <span data-ttu-id="24f03-148">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="24f03-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="24f03-149">`tenant` est le domaine de votre client Azure AD, par exemple, contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="24f03-149">The `tenant` is the domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="24f03-150">`clientId` est l’ID client de votre application que vous avez copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="24f03-150">The `clientId` is the clientId of your application you copied from the portal.</span></span>
* <span data-ttu-id="24f03-151">Vous devez maintenant découvrir l’URI de rappel pour votre application Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="24f03-151">You now need to discover the callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="24f03-152">Définissez un point d’arrêt sur cette ligne dans la méthode `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="24f03-152">Set a breakpoint on this line in the `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="24f03-153">Exécutez l’application et copiez la valeur de `redirectUri` à part lorsque le point d’arrêt est atteint.</span><span class="sxs-lookup"><span data-stu-id="24f03-153">Run the app, and copy aside the value of `redirectUri` when the breakpoint is hit.</span></span>  <span data-ttu-id="24f03-154">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="24f03-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="24f03-155">Sous l’onglet **Configurer** de votre application, dans le portail de gestion Azure, remplacez la valeur de **l’URI de redirection** par cette valeur.</span><span class="sxs-lookup"><span data-stu-id="24f03-155">Back on the **Configure** tab of your application in the Azure Management Portal, replace the value of the **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-to-get-tokens-from-aad"></a><span data-ttu-id="24f03-156">3. Utilisation de la bibliothèque ADAL pour obtenir des jetons à partir d’AAD</span><span class="sxs-lookup"><span data-stu-id="24f03-156">3. Use ADAL to Get Tokens from AAD</span></span>
<span data-ttu-id="24f03-157">Le principe de base de la bibliothèque ADAL consiste simplement à appeler `authContext.AcquireToken(…)` chaque fois que votre application a besoin d’un jeton d’accès, et la bibliothèque ADAL s’occupe du reste.</span><span class="sxs-lookup"><span data-stu-id="24f03-157">The basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

* <span data-ttu-id="24f03-158">La première étape est d’initialiser le `AuthenticationContext` de votre application, la classe principale de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="24f03-158">The first step is to initialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="24f03-159">C’est à ce moment-là que vous fournissez à la bibliothèque ADAL les coordonnées dont elle a besoin pour communiquer avec Azure AD et lui indiquer comment mettre en cache des jetons.</span><span class="sxs-lookup"><span data-stu-id="24f03-159">This is where you pass ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="24f03-160">Recherchez maintenant la méthode `Search(...)` qui est appelée lorsque l’utilisateur clique sur le bouton Rechercher dans l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="24f03-160">Now locate the `Search(...)` method, which will be invoked when the user cliks the "Search" button in the app's UI.</span></span>  <span data-ttu-id="24f03-161">Cette méthode effectue une demande GET auprès de l’API Graph Azure AD pour l’interroger à propos d’utilisateurs dont l’UPN commence par le terme de recherche donné.</span><span class="sxs-lookup"><span data-stu-id="24f03-161">This method makes a GET request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span>  <span data-ttu-id="24f03-162">Cependant, pour interroger l’API Graph, vous devez inclure un jeton d’accès (access_token) dans l’en-tête `Authorization` de la demande ; c’est à ce moment qu’intervient la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="24f03-162">But in order to query the Graph API, you need to include an access_token in the `Authorization` header of the request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try to get a token without triggering any user prompt.
    // ADAL will check whether the requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained the QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="24f03-163">Si l’authentification interactive est nécessaire, la bibliothèque ADAL utilise le WAB (Web Authentication Broker) de Windows Phone et le [modèle de continuation](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) pour afficher la page de connexion d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24f03-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) to display the Azure AD sign in page.</span></span>  <span data-ttu-id="24f03-164">Lorsque l’utilisateur se connecte, votre application doit fournir à la bibliothèque ADAL les résultats de l’interaction du WAB.</span><span class="sxs-lookup"><span data-stu-id="24f03-164">When the user signs in, your app needs to pass ADAL the results of the WAB interaction.</span></span>  <span data-ttu-id="24f03-165">C’est aussi simple que d’implémenter l’interface `ContinueWebAuthentication` :</span><span class="sxs-lookup"><span data-stu-id="24f03-165">This is as simple as implementing the `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when the application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass the authentication interaction results to ADAL, which will
    // conclude the token acquisition operation and invoke the callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="24f03-166">Il est temps d’utiliser le `AuthenticationResult` qu’ADAL renvoie à votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-166">Now it's time to use the `AuthenticationResult` that ADAL returned to your app.</span></span>  <span data-ttu-id="24f03-167">Dans le rappel `QueryGraph(...)`, joignez à la demande GET, dans l’en-tête d’autorisation, le jeton d’accès (access_token) que vous avez acquis :</span><span class="sxs-lookup"><span data-stu-id="24f03-167">In the `QueryGraph(...)` callback, attach the access_token you acquired to the GET request in the Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add the access token to the Authorization Header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="24f03-168">Vous pouvez également utiliser l’objet `AuthenticationResult` pour afficher des informations concernant l’utilisateur dans votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-168">You can also use the `AuthenticationResult` object to display information about the user in your app.</span></span> <span data-ttu-id="24f03-169">Dans la méthode `QueryGraph(...)` , utilisez le résultat pour afficher l’ID de l’utilisateur sur la page :</span><span class="sxs-lookup"><span data-stu-id="24f03-169">In the `QueryGraph(...)` method, use the result to show the user's id on the page:</span></span>

```C#
// Update the Page UI to represent the signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="24f03-170">Enfin, vous pouvez également utiliser la bibliothèque ADAL pour déconnecter l’utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="24f03-170">Finally, you can use ADAL to sign the user out of hte application as well.</span></span>  <span data-ttu-id="24f03-171">Lorsque l’utilisateur clique sur le bouton Déconnexion, nous voulons vérifier que l’appel suivant vers `AcquireTokenSilentAsync(...)` échoue.</span><span class="sxs-lookup"><span data-stu-id="24f03-171">When the user clicks the "Sign Out" button, we want to ensure that the next call to `AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="24f03-172">Avec la bibliothèque ADAL, c’est aussi simple que d’effacer le cache de jeton :</span><span class="sxs-lookup"><span data-stu-id="24f03-172">With ADAL, this is as easy as clearing the token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from the token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="24f03-173">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="24f03-173">Congratulations!</span></span> <span data-ttu-id="24f03-174">Vous disposez d’une application Windows Phone fonctionnelle capable d’authentifier les utilisateurs, d’appeler en toute sécurité les API web à l’aide d’OAuth 2.0 et d’obtenir des informations de base concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="24f03-174">You now have a working Windows Phone app that has the ability to authenticate users, securely call Web APIs using OAuth 2.0, and get basic information about the user.</span></span>  <span data-ttu-id="24f03-175">Si vous ne l’avez pas encore fait, il est maintenant temps de remplir votre client avec quelques utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="24f03-175">If you haven’t already, now is the time to populate your tenant with some users.</span></span>  <span data-ttu-id="24f03-176">Exécutez votre application DirectorySearcher et connectez-vous avec l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="24f03-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="24f03-177">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="24f03-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="24f03-178">Fermez l’application et exécutez-la de nouveau.</span><span class="sxs-lookup"><span data-stu-id="24f03-178">Close the app, and re-run it.</span></span>  <span data-ttu-id="24f03-179">Observez que la session utilisateur reste identique.</span><span class="sxs-lookup"><span data-stu-id="24f03-179">Notice how the user’s session remains intact.</span></span>  <span data-ttu-id="24f03-180">Déconnectez-vous et reconnectez-vous sous le nom d’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="24f03-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="24f03-181">La bibliothèque ADAL facilite l’intégration de toutes ces fonctionnalités d’identité communes dans votre application.</span><span class="sxs-lookup"><span data-stu-id="24f03-181">ADAL makes it easy to incorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="24f03-182">Elle effectue les tâches ingrates pour vous : gestion du cache, prise en charge du protocole OAuth, présentation d’une interface utilisateur de connexion à l’utilisateur, actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="24f03-182">It takes care of all the dirty work for you - cache management, OAuth protocol support, presenting the user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="24f03-183">La seule chose que vous devez vraiment connaître est un appel unique d’API : `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="24f03-183">All you really need to know is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="24f03-184">Pour référence, l’exemple terminé (sans vos valeurs de configuration) est fourni [ici](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="24f03-184">For reference, the completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="24f03-185">Vous pouvez à présent aborder d’autres scénarios d’identité.</span><span class="sxs-lookup"><span data-stu-id="24f03-185">You can now move on to additional identity scenarios.</span></span>  <span data-ttu-id="24f03-186">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="24f03-186">You may want to try:</span></span>

[<span data-ttu-id="24f03-187">Sécurisation d’une API web .NET avec Azure AD >></span><span class="sxs-lookup"><span data-stu-id="24f03-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

