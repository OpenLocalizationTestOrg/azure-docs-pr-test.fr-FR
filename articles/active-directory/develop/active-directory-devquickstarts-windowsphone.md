---
title: aaaAzure AD Windows Phone prise en main | Documents Microsoft
description: "Comment toobuild une application Windows Phone qui s’intègre à Azure AD pour l’authentification dans Azure AD qui appelle protégé API en utilisant OAuth."
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
ms.openlocfilehash: e766bfcdfae10483772154f4b5facdec05fc846f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-a-windows-phone-app"></a><span data-ttu-id="64496-103">Intégration d’Azure AD avec une application Windows Phone</span><span class="sxs-lookup"><span data-stu-id="64496-103">Integrate Azure AD with a Windows Phone App</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="64496-104">Les projets du Windows Phone 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="64496-104">Windows Phone 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="64496-105">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="64496-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="64496-106">Si vous développez une application Windows Phone 8.1, Azure AD rend très simple pour vous tooauthenticate vos utilisateurs avec leurs comptes Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64496-106">If you're developing a Windows Phone 8.1 app, Azure AD makes it simple and straightforward for you tooauthenticate your users with their Active Directory accounts.</span></span>  <span data-ttu-id="64496-107">Il permet également de votre application toosecurely consommer n’importe quel web API protégée par Azure AD, comme la hello API Office 365 ou hello API Azure.</span><span class="sxs-lookup"><span data-stu-id="64496-107">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

> [!NOTE]
> <span data-ttu-id="64496-108">Cet exemple de code utilise la bibliothèque ADAL v2.0.</span><span class="sxs-lookup"><span data-stu-id="64496-108">This code sample uses ADAL v2.0.</span></span>  <span data-ttu-id="64496-109">Pour la dernière technologie de hello, vous souhaiterez peut-être tooinstead Essayez notre [didacticiel universelle de Windows à l’aide de la version 3.0 de la bibliothèque ADAL](active-directory-devquickstarts-windowsstore.md).</span><span class="sxs-lookup"><span data-stu-id="64496-109">For hello latest technology, you may want tooinstead try our [Windows Universal Tutorial using ADAL v3.0](active-directory-devquickstarts-windowsstore.md).</span></span>  <span data-ttu-id="64496-110">Si vous créez en fait une application pour Windows Phone 8.1, il s’agit ici de hello.</span><span class="sxs-lookup"><span data-stu-id="64496-110">If you are indeed building an app for Windows Phone 8.1, this is hello right place.</span></span>  <span data-ttu-id="64496-111">ADAL v2.0 est toujours entièrement compatible avec, et est hello recommandée de développement agianst d’applications Windows Phone 8.1 à l’aide de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64496-111">ADAL v2.0 is still fully supported, and is hello recommended way of developing apps agianst Windows Phone 8.1 using Azure AD.</span></span>
> 
> 

<span data-ttu-id="64496-112">Pour .NET native les clients qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello bibliothèque d’authentification Active Directory, ou la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="64496-112">For .NET native clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library, or ADAL.</span></span>  <span data-ttu-id="64496-113">Seul objectif la bibliothèque ADAL de durée de vie est toomake plus facile pour les jetons d’accès tooget votre application.</span><span class="sxs-lookup"><span data-stu-id="64496-113">ADAL’s sole purpose in life is toomake it easy for your app tooget access tokens.</span></span>  <span data-ttu-id="64496-114">toodemonstrate facilité il s’agit, ici, nous créerons une application Windows Phone 8.1 « répertoire de recherche » qui :</span><span class="sxs-lookup"><span data-stu-id="64496-114">toodemonstrate just how easy it is, here we’ll build a "Directory Searcher" Windows Phone 8.1 app that:</span></span>

* <span data-ttu-id="64496-115">Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="64496-115">Gets access tokens for calling hello Azure AD Graph API using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="64496-116">recherche, dans un répertoire, d’utilisateurs correspondant à un UPN (nom d’utilisateur principal) donné.</span><span class="sxs-lookup"><span data-stu-id="64496-116">Searches a directory for users with a given UPN.</span></span>
* <span data-ttu-id="64496-117">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="64496-117">Signs users out.</span></span>

<span data-ttu-id="64496-118">toobuild hello travail application complète, vous devez :</span><span class="sxs-lookup"><span data-stu-id="64496-118">toobuild hello complete working application, you’ll need to:</span></span>

1. <span data-ttu-id="64496-119">inscrire votre application auprès d’Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="64496-119">Register your application with Azure AD.</span></span>
2. <span data-ttu-id="64496-120">installer et configurer la bibliothèque ADAL ;</span><span class="sxs-lookup"><span data-stu-id="64496-120">Install & Configure ADAL.</span></span>
3. <span data-ttu-id="64496-121">Utiliser des jetons tooget ADAL d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64496-121">Use ADAL tooget tokens from Azure AD.</span></span>

<span data-ttu-id="64496-122">tooget démarré, [télécharger un projet de squelette](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) ou [télécharger l’exemple hello terminée](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="64496-122">tooget started, [download a skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/skeleton.zip) or [download hello completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="64496-123">Chaque option est une solution Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="64496-123">Each is a Visual Studio 2013 solution.</span></span>  <span data-ttu-id="64496-124">Vous avez également besoin d’un client Azure AD dans lequel vous pouvez créer des utilisateurs et inscrire une application.</span><span class="sxs-lookup"><span data-stu-id="64496-124">You'll also need an Azure AD tenant in which you can create users and register an application.</span></span>  <span data-ttu-id="64496-125">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="64496-125">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="1-register-hello-directory-searcher-application"></a><span data-ttu-id="64496-126">1. Inscrire hello Application recherche de répertoire</span><span class="sxs-lookup"><span data-stu-id="64496-126">1. Register hello Directory Searcher Application</span></span>
<span data-ttu-id="64496-127">tooenable vos jetons tooget d’application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess d’autorisation Azure AD Graph API :</span><span class="sxs-lookup"><span data-stu-id="64496-127">tooenable your app tooget tokens, you’ll first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="64496-128">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="64496-128">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="64496-129">Sur la barre supérieure de hello, cliquez sur votre compte et sous hello **répertoire** , sélectionnez le client Active Directory de hello où vous souhaitez tooregister votre application.</span><span class="sxs-lookup"><span data-stu-id="64496-129">On hello top bar, click on your account and under hello **Directory** list, choose hello Active Directory tenant where you wish tooregister your application.</span></span>
3. <span data-ttu-id="64496-130">Cliquez sur **plus Services** dans hello de navigation de gauche, puis choisissez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="64496-130">Click on **More Services** in hello left hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="64496-131">Cliquez sur **Inscriptions des applications**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64496-131">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="64496-132">Suivez les invites hello et créer un nouveau **Application cliente Native**.</span><span class="sxs-lookup"><span data-stu-id="64496-132">Follow hello prompts and create a new **Native Client Application**.</span></span>
  * <span data-ttu-id="64496-133">Hello **nom** Hello application décrivent tooend-utilisateurs de votre application</span><span class="sxs-lookup"><span data-stu-id="64496-133">hello **Name** of hello application will describe your application tooend-users</span></span>
  * <span data-ttu-id="64496-134">Hello **Uri de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.</span><span class="sxs-lookup"><span data-stu-id="64496-134">hello **Redirect Uri** is a scheme and string combination that Azure AD will use tooreturn token responses.</span></span>  <span data-ttu-id="64496-135">Entrez temporairement une valeur d’espace réservé, par exemple, `http://DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="64496-135">Enter a placeholder value for now, e.g. `http://DirectorySearcher`.</span></span>  <span data-ttu-id="64496-136">Nous remplacerons cette valeur ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="64496-136">We'll replace this value later.</span></span>
6. <span data-ttu-id="64496-137">Une fois l’inscription terminée, AAD affecte un ID d’application unique à votre application.</span><span class="sxs-lookup"><span data-stu-id="64496-137">Once you’ve completed registration, AAD will assign your app a unique Application ID.</span></span>  <span data-ttu-id="64496-138">Vous aurez besoin de cette valeur dans les sections suivantes hello, par conséquent, copiez-le à partir de l’onglet de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="64496-138">You’ll need this value in hello next sections, so copy it from hello application tab.</span></span>
7. <span data-ttu-id="64496-139">À partir de hello **paramètres** choisissez **autorisations requises** et choisissez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="64496-139">From hello **Settings** page, choose **Required Permissions** and choose **Add**.</span></span> <span data-ttu-id="64496-140">Sélectionnez hello **Microsoft Graph** comme hello API et ajouter hello **les données d’annuaire en lecture** autorisation sous **autorisations déléguées**.</span><span class="sxs-lookup"><span data-stu-id="64496-140">Select hello **Microsoft Graph** as hello API and add hello **Read Directory Data** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="64496-141">Cette opération activera votre hello de tooquery d’application API Graph pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="64496-141">This will enable your application tooquery hello Graph API for users.</span></span>

## <a name="2-install--configure-adal"></a><span data-ttu-id="64496-142">2. Installez et configurez ADAL</span><span class="sxs-lookup"><span data-stu-id="64496-142">2. Install & Configure ADAL</span></span>
<span data-ttu-id="64496-143">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="64496-143">Now that you have an application in Azure AD, you can install ADAL and write your identity-related code.</span></span>  <span data-ttu-id="64496-144">Toocommunicate en mesure de toobe ADAL avec Azure AD, vous devez tooprovide avec des informations sur l’inscription de votre application.</span><span class="sxs-lookup"><span data-stu-id="64496-144">In order for ADAL toobe able toocommunicate with Azure AD, you need tooprovide it with some information about your app registration.</span></span>

* <span data-ttu-id="64496-145">Commencez par ajouter le projet de DirectorySearcher toohello ADAL à l’aide de la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="64496-145">Begin by adding ADAL toohello DirectorySearcher project using hello Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
```

* <span data-ttu-id="64496-146">Dans le projet de DirectorySearcher hello, ouvrez `MainPage.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="64496-146">In hello DirectorySearcher project, open `MainPage.xaml.cs`.</span></span>  <span data-ttu-id="64496-147">Remplacez les valeurs de hello en hello `Config Values` hello tooreflect de région les valeurs d’entrée en hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="64496-147">Replace hello values in hello `Config Values` region tooreflect hello values you input into hello Azure Portal.</span></span>  <span data-ttu-id="64496-148">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="64496-148">Your code will reference these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="64496-149">Hello `tenant` est domaine hello de votre client Azure AD, par exemple, contoso.onmicrosoft.com</span><span class="sxs-lookup"><span data-stu-id="64496-149">hello `tenant` is hello domain of your Azure AD tenant, e.g. contoso.onmicrosoft.com</span></span>
  * <span data-ttu-id="64496-150">Hello `clientId` est clientId hello de votre application que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="64496-150">hello `clientId` is hello clientId of your application you copied from hello portal.</span></span>
* <span data-ttu-id="64496-151">Vous devez maintenant uri de rappel toodiscover hello pour votre application Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="64496-151">You now need toodiscover hello callback uri for your Windows Phone app.</span></span>  <span data-ttu-id="64496-152">Définir un point d’arrêt sur cette ligne de hello `MainPage` méthode :</span><span class="sxs-lookup"><span data-stu-id="64496-152">Set a breakpoint on this line in hello `MainPage` method:</span></span>

```
redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
```
* <span data-ttu-id="64496-153">Exécutez l’application hello et copiez mis de côté valeur hello `redirectUri` lorsque hello point d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="64496-153">Run hello app, and copy aside hello value of `redirectUri` when hello breakpoint is hit.</span></span>  <span data-ttu-id="64496-154">Le résultat suivant doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="64496-154">It should look something like</span></span>

```
ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
```

* <span data-ttu-id="64496-155">Retour sur hello **configurer** onglet de votre application Bonjour portail de gestion Azure, remplacez la valeur hello hello **RedirectUri** avec cette valeur.</span><span class="sxs-lookup"><span data-stu-id="64496-155">Back on hello **Configure** tab of your application in hello Azure Management Portal, replace hello value of hello **RedirectUri** with this value.</span></span>  

## <a name="3-use-adal-tooget-tokens-from-aad"></a><span data-ttu-id="64496-156">3. Utiliser des jetons tooGet ADAL d’AAD</span><span class="sxs-lookup"><span data-stu-id="64496-156">3. Use ADAL tooGet Tokens from AAD</span></span>
<span data-ttu-id="64496-157">Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que votre application a besoin d’un jeton d’accès, il appelle simplement `authContext.AcquireToken(…)`, et la bibliothèque ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="64496-157">hello basic principle behind ADAL is that whenever your app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

* <span data-ttu-id="64496-158">première étape de Hello est tooinitialize de votre application `AuthenticationContext` -ADAL de la classe principale.</span><span class="sxs-lookup"><span data-stu-id="64496-158">hello first step is tooinitialize your app’s `AuthenticationContext` - ADAL’s primary class.</span></span>  <span data-ttu-id="64496-159">Il s’agit d’où vous passez la bibliothèque ADAL hello coordonnées nécessaires toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.</span><span class="sxs-lookup"><span data-stu-id="64496-159">This is where you pass ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

```C#
public MainPage()
{
    ...

    // ADAL for Windows Phone 8.1 builds AuthenticationContext instances through a factory
    authContext = AuthenticationContext.CreateAsync(authority).GetResults();
}
```

* <span data-ttu-id="64496-160">Maintenant recherchez hello `Search(...)` (méthode), qui sera appelé lorsque hello utilisateur cliks hello « Rechercher » un bouton dans l’interface utilisateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="64496-160">Now locate hello `Search(...)` method, which will be invoked when hello user cliks hello "Search" button in hello app's UI.</span></span>  <span data-ttu-id="64496-161">Cette méthode rend un tooquery toohello API Azure AD Graph de demande GET pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="64496-161">This method makes a GET request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span>  <span data-ttu-id="64496-162">Mais dans hello tooquery de commande API Graph, vous devez tooinclude un access_token Bonjour `Authorization` en-tête Hello demande - il s’agit là qu’intervient la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="64496-162">But in order tooquery hello Graph API, you need tooinclude an access_token in hello `Authorization` header of hello request - this is where ADAL comes in.</span></span>

```C#
private async void Search(object sender, RoutedEventArgs e)
{
    ...

    // Try tooget a token without triggering any user prompt.
    // ADAL will check whether hello requested token is in ADAL's token cache or can otherwise be obtained without user interaction.
    AuthenticationResult result = await authContext.AcquireTokenSilentAsync(graphResourceId, clientId);
    if (result != null && result.Status == AuthenticationStatus.Success)
    {
        // A token was successfully retrieved.
        QueryGraph(result);
    }
    else
    {
        // Acquiring a token without user interaction was not possible.
        // Trigger an authentication experience and specify that once a token has been obtained hello QueryGraph method should be called
        authContext.AcquireTokenAndContinue(graphResourceId, clientId, redirectURI, QueryGraph);
    }
}
```
* <span data-ttu-id="64496-163">Si l’authentification interactive est nécessaire, la bibliothèque ADAL utilise du Windows Phone Web d’authentification Service Broker (carnet d’adresses) et [modèle de continuation](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) page de connexion toodisplay hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64496-163">If interactive authentication is necessary, ADAL will use Windows Phone's Web Authentication Broker (WAB) and [continuation model](http://www.cloudidentity.com/blog/2014/06/16/adal-for-windows-phone-8-1-deep-dive/) toodisplay hello Azure AD sign in page.</span></span>  <span data-ttu-id="64496-164">Lorsque l’utilisateur de hello se connecte, votre application doit toopass les résultats de la bibliothèque ADAL hello d’interaction de carnet d’adresses Windows hello.</span><span class="sxs-lookup"><span data-stu-id="64496-164">When hello user signs in, your app needs toopass ADAL hello results of hello WAB interaction.</span></span>  <span data-ttu-id="64496-165">Il est aussi simple que l’implémentation hello `ContinueWebAuthentication` interface :</span><span class="sxs-lookup"><span data-stu-id="64496-165">This is as simple as implementing hello `ContinueWebAuthentication` interface:</span></span>

```C#
// This method is automatically invoked when hello application
// is reactivated after an authentication interaction through WebAuthenticationBroker.
public async void ContinueWebAuthentication(WebAuthenticationBrokerContinuationEventArgs args)
{
    // pass hello authentication interaction results tooADAL, which will
    // conclude hello token acquisition operation and invoke hello callback specified in AcquireTokenAndContinue.
    await authContext.ContinueAcquireTokenAsync(args);
}
```

* <span data-ttu-id="64496-166">À présent, il hello toouse de temps `AuthenticationResult` que la bibliothèque ADAL retournée tooyour application.</span><span class="sxs-lookup"><span data-stu-id="64496-166">Now it's time toouse hello `AuthenticationResult` that ADAL returned tooyour app.</span></span>  <span data-ttu-id="64496-167">Bonjour `QueryGraph(...)` rappel, attacher access_token hello acquis de demande GET de toohello dans l’en-tête d’autorisation hello :</span><span class="sxs-lookup"><span data-stu-id="64496-167">In hello `QueryGraph(...)` callback, attach hello access_token you acquired toohello GET request in hello Authorization header:</span></span>

```C#
private async void QueryGraph(AuthenticationResult result)
{
    if (result.Status != AuthenticationStatus.Success)
    {
        MessageDialog dialog = new MessageDialog(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", result.Error, result.ErrorDescription), "Sorry, an error occurred while signing you in.");
        await dialog.ShowAsync();
    }

    // Add hello access token toohello Authorization Header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

    ...
}
```
* <span data-ttu-id="64496-168">Vous pouvez également utiliser hello `AuthenticationResult` toodisplay informations utilisateur hello dans votre application de l’objet.</span><span class="sxs-lookup"><span data-stu-id="64496-168">You can also use hello `AuthenticationResult` object toodisplay information about hello user in your app.</span></span> <span data-ttu-id="64496-169">Bonjour `QueryGraph(...)` méthode, utilisez hello résultat tooshow hello id de l’utilisateur sur la page de hello :</span><span class="sxs-lookup"><span data-stu-id="64496-169">In hello `QueryGraph(...)` method, use hello result tooshow hello user's id on hello page:</span></span>

```C#
// Update hello Page UI toorepresent hello signed in user
ActiveUser.Text = result.UserInfo.DisplayableId;
```
* <span data-ttu-id="64496-170">Enfin, vous pouvez utiliser utilisateur hello toosign ADAL ainsi l’application.</span><span class="sxs-lookup"><span data-stu-id="64496-170">Finally, you can use ADAL toosign hello user out of hte application as well.</span></span>  <span data-ttu-id="64496-171">Utilisateur de hello clique sur bouton « Déconnexion » hello, nous souhaitons tooensure qui hello prochain appel trop`AcquireTokenSilentAsync(...)` échoue.</span><span class="sxs-lookup"><span data-stu-id="64496-171">When hello user clicks hello "Sign Out" button, we want tooensure that hello next call too`AcquireTokenSilentAsync(...)` will fail.</span></span>  <span data-ttu-id="64496-172">Avec la bibliothèque ADAL, il est aussi simple que l’effacement du cache de jetons hello :</span><span class="sxs-lookup"><span data-stu-id="64496-172">With ADAL, this is as easy as clearing hello token cache:</span></span>

```C#
private void SignOut()
{
    // Clear session state from hello token cache.
    authContext.TokenCache.Clear();

    ...
}
```

<span data-ttu-id="64496-173">Félicitations !</span><span class="sxs-lookup"><span data-stu-id="64496-173">Congratulations!</span></span> <span data-ttu-id="64496-174">Vous avez une application Windows Phone qui a des utilisateurs tooauthenticate hello capacité, en toute sécurité appelez des API Web à l’aide d’OAuth 2.0 et obtenez des informations de base sur l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="64496-174">You now have a working Windows Phone app that has hello ability tooauthenticate users, securely call Web APIs using OAuth 2.0, and get basic information about hello user.</span></span>  <span data-ttu-id="64496-175">Si vous n’avez pas encore, est à présent hello temps toopopulate votre locataire avec certains utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="64496-175">If you haven’t already, now is hello time toopopulate your tenant with some users.</span></span>  <span data-ttu-id="64496-176">Exécutez votre application DirectorySearcher et connectez-vous avec l’un de ces utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="64496-176">Run your DirectorySearcher app, and sign in with one of those users.</span></span>  <span data-ttu-id="64496-177">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="64496-177">Search for other users based on their UPN.</span></span>  <span data-ttu-id="64496-178">Fermez l’application hello et réexécutez-la.</span><span class="sxs-lookup"><span data-stu-id="64496-178">Close hello app, and re-run it.</span></span>  <span data-ttu-id="64496-179">Notez que la session de l’utilisateur hello reste intacte.</span><span class="sxs-lookup"><span data-stu-id="64496-179">Notice how hello user’s session remains intact.</span></span>  <span data-ttu-id="64496-180">Déconnectez-vous et reconnectez-vous sous le nom d’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="64496-180">Sign out, and sign back in as another user.</span></span>

<span data-ttu-id="64496-181">ADAL rend facile tooincorporate toutes ces fonctionnalités d’identité commune dans votre application.</span><span class="sxs-lookup"><span data-stu-id="64496-181">ADAL makes it easy tooincorporate all of these common identity features into your application.</span></span>  <span data-ttu-id="64496-182">Il s’occupe de tout le travail dirty hello vous - gestion du cache, la prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, l’actualisation des jetons expirés et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="64496-182">It takes care of all hello dirty work for you - cache management, OAuth protocol support, presenting hello user with a login UI, refreshing expired tokens, and more.</span></span>  <span data-ttu-id="64496-183">Vous devez vraiment tooknow est un simple appel d’API `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="64496-183">All you really need tooknow is a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="64496-184">Pour référence, exemple hello terminée (sans les valeurs de configuration) est fourni [ici](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="64496-184">For reference, hello completed sample (without your configuration values) is provided [here](https://github.com/AzureADQuickStarts/NativeClient-WindowsPhone/archive/complete.zip).</span></span>  <span data-ttu-id="64496-185">Vous pouvez maintenant déplacer sur les scénarios d’identité tooadditional.</span><span class="sxs-lookup"><span data-stu-id="64496-185">You can now move on tooadditional identity scenarios.</span></span>  <span data-ttu-id="64496-186">Vous souhaiterez peut-être tootry :</span><span class="sxs-lookup"><span data-stu-id="64496-186">You may want tootry:</span></span>

[<span data-ttu-id="64496-187">Sécurisation d’une API web .NET avec Azure AD &gt;&gt;</span><span class="sxs-lookup"><span data-stu-id="64496-187">Secure a .NET Web API with Azure AD >></span></span>](active-directory-devquickstarts-webapi-dotnet.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]

