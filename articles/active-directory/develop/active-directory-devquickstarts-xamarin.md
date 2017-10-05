---
title: "Bien démarrer avec Azure AD Xamarin | Microsoft Docs"
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
ms.openlocfilehash: 54ee403f283bc5dc79911e2e813dd513ff595828
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="integrate-azure-ad-with-xamarin-apps"></a><span data-ttu-id="7814a-103">Intégrer Azure AD avec des applications Xamarin</span><span class="sxs-lookup"><span data-stu-id="7814a-103">Integrate Azure AD with Xamarin apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="7814a-104">Avec Xamarin, vous pouvez écrire des applications mobiles en C# qui peuvent s’exécuter sous iOS, Android et Windows (appareils mobiles et PC).</span><span class="sxs-lookup"><span data-stu-id="7814a-104">With Xamarin, you can write mobile apps in C# that can run on iOS, Android, and Windows (mobile devices and PCs).</span></span> <span data-ttu-id="7814a-105">Si vous créez une application avec Xamarin, Azure Active Directory (Azure AD) facilite l’authentification des utilisateurs avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7814a-105">If you're building an app using Xamarin, Azure Active Directory (Azure AD) makes it simple to authenticate users with their Azure AD accounts.</span></span> <span data-ttu-id="7814a-106">L’application peut également utiliser en toute sécurité une API web protégée par Azure AD, telle que les API Office 365 ou l’API Azure.</span><span class="sxs-lookup"><span data-stu-id="7814a-106">The app can also securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="7814a-107">Pour les applications Xamarin qui doivent accéder à des ressources protégées, Azure AD fournit la bibliothèque d’authentification Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="7814a-107">For Xamarin apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="7814a-108">Cette bibliothèque a pour seule fonction de simplifier l’obtention des jetons d’accès pour les applications.</span><span class="sxs-lookup"><span data-stu-id="7814a-108">The sole purpose of ADAL is to make it easy for apps to get access tokens.</span></span> <span data-ttu-id="7814a-109">Pour illustrer cette simplicité, cet article montre comment créer des applications DirectorySearcher effectuant les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="7814a-109">To demonstrate how easy it is, this article shows how to build DirectorySearcher apps that:</span></span>

* <span data-ttu-id="7814a-110">exécution sous iOS, Android, Windows Desktop, Windows Phone et Windows Store ;</span><span class="sxs-lookup"><span data-stu-id="7814a-110">Run on iOS, Android, Windows Desktop, Windows Phone, and Windows Store.</span></span>
* <span data-ttu-id="7814a-111">utilisation d’une bibliothèque de classes portable (PCL) unique pour authentifier les utilisateurs et obtenir des jetons pour l’API Graph Azure AD ;</span><span class="sxs-lookup"><span data-stu-id="7814a-111">Use a single portable class library (PCL) to authenticate users and get tokens for the Azure AD Graph API.</span></span>
* <span data-ttu-id="7814a-112">recherche, dans un annuaire, d’utilisateurs correspondant à un UPN (nom d’utilisateur principal) donné.</span><span class="sxs-lookup"><span data-stu-id="7814a-112">Search a directory for users with a given UPN.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="7814a-113">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7814a-113">Before you get started</span></span>
* <span data-ttu-id="7814a-114">Téléchargez [la structure du projet](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip) ou [l’exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="7814a-114">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="7814a-115">Chaque téléchargement est une solution Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7814a-115">Each download is a Visual Studio 2013 solution.</span></span>
* <span data-ttu-id="7814a-116">Vous avez également besoin d’un client Azure AD dans lequel créer les utilisateurs et inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="7814a-116">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="7814a-117">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="7814a-117">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="7814a-118">Lorsque vous êtes prêt, suivez les procédures des quatre sections qui suivent.</span><span class="sxs-lookup"><span data-stu-id="7814a-118">When you are ready, follow the procedures in the next four sections.</span></span>

## <a name="step-1-set-up-your-xamarin-development-environment"></a><span data-ttu-id="7814a-119">Étape 1 : Configurer votre environnement de développement Xamarin</span><span class="sxs-lookup"><span data-stu-id="7814a-119">Step 1: Set up your Xamarin development environment</span></span>
<span data-ttu-id="7814a-120">Étant donné que ce didacticiel inclut des projets pour iOS, Android et Windows, il vous faut à la fois Visual Studio et Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7814a-120">Because this tutorial includes projects for iOS, Android, and Windows, you need both Visual Studio and Xamarin.</span></span> <span data-ttu-id="7814a-121">Pour créer l’environnement nécessaire, suivez la procédure à la page [Configurer et installer Visual Studio et Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="7814a-121">To create the necessary environment, complete the process in [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) on MSDN.</span></span> <span data-ttu-id="7814a-122">Les instructions incluent des documents que vous pouvez consulter pour en savoir plus sur Xamarin en attendant que les installations se terminent.</span><span class="sxs-lookup"><span data-stu-id="7814a-122">The instructions include material that you can review to learn more about Xamarin while you're waiting for the installations to be completed.</span></span>

<span data-ttu-id="7814a-123">Une fois vous avez terminé la configuration, ouvrez la solution dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7814a-123">After you've completed the setup, open the solution in Visual Studio.</span></span> <span data-ttu-id="7814a-124">Vous y trouverez six projets : cinq projets propres à la plateforme et une PCL, DirectorySearcher.cs, partagée par toutes les plateformes.</span><span class="sxs-lookup"><span data-stu-id="7814a-124">There, you will find six projects: five platform-specific projects and one PCL, DirectorySearcher.cs, which will be shared across all platforms.</span></span>

## <a name="step-2-register-the-directorysearcher-app"></a><span data-ttu-id="7814a-125">Étape 2 : Inscrire l’application DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="7814a-125">Step 2: Register the DirectorySearcher app</span></span>
<span data-ttu-id="7814a-126">Pour autoriser l’application à obtenir des jetons, vous devez tout d’abord l’inscrire dans votre client Azure AD et lui accorder l’autorisation d’accéder à l’API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7814a-126">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="7814a-127">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="7814a-127">Here's how:</span></span>

1. <span data-ttu-id="7814a-128">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7814a-128">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7814a-129">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="7814a-129">On the top bar, click your account.</span></span> <span data-ttu-id="7814a-130">Puis, dans la liste **Annuaire**, sélectionnez le client Active Directory dans lequel vous voulez inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="7814a-130">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="7814a-131">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7814a-131">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="7814a-132">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7814a-132">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="7814a-133">Pour créer une **application cliente native**, suivez les invites.</span><span class="sxs-lookup"><span data-stu-id="7814a-133">To create a new **Native Client Application**, follow the prompts.</span></span>
  * <span data-ttu-id="7814a-134">Le champ **Nom** décrit l’application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7814a-134">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="7814a-135">**L’URI de redirection** est une combinaison de schémas et de chaînes qu’Azure AD utilise pour renvoyer des réponses concernant les jetons.</span><span class="sxs-lookup"><span data-stu-id="7814a-135">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="7814a-136">Entrez une valeur (par exemple, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="7814a-136">Enter a value (for example, http://DirectorySearcher).</span></span>
6. <span data-ttu-id="7814a-137">Une fois l’inscription terminée, Azure AD affecte un ID d’application unique à l’application.</span><span class="sxs-lookup"><span data-stu-id="7814a-137">After you’ve completed registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="7814a-138">Copiez la valeur de l’onglet **Application**, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="7814a-138">Copy the value from the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="7814a-139">Sur la page **Paramètres**, sélectionnez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="7814a-139">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="7814a-140">Sélectionnez l’API **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="7814a-140">Select **Microsoft Graph** as the API.</span></span> <span data-ttu-id="7814a-141">Sous **Autorisations déléguées**, ajoutez l’autorisation **Lire les données de l’annuaire**.</span><span class="sxs-lookup"><span data-stu-id="7814a-141">Under **Delegated Permissions**, add the **Read Directory Data** permission.</span></span>  
<span data-ttu-id="7814a-142">Cette action permet à l’application d’interroger l’API Graph pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7814a-142">This action enables the app to query the Graph API for users.</span></span>

## <a name="step-3-install-and-configure-adal"></a><span data-ttu-id="7814a-143">Étape 3 : Installer et configurer la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="7814a-143">Step 3: Install and configure ADAL</span></span>
<span data-ttu-id="7814a-144">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="7814a-144">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="7814a-145">Pour que la bibliothèque ADAL puisse communiquer avec Azure AD, fournissez-lui des informations sur l’inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="7814a-145">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="7814a-146">Ajoutez ADAL au projet DirectorySearcher à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="7814a-146">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

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

    <span data-ttu-id="7814a-147">Notez que deux références de bibliothèque sont ajoutées à chaque projet : la partie PCL de la bibliothèque ADAL et une partie propre à la plateforme.</span><span class="sxs-lookup"><span data-stu-id="7814a-147">Note that two library references are added to each project: the PCL portion of ADAL and a platform-specific portion.</span></span>
2. <span data-ttu-id="7814a-148">Dans le projet DirectorySearcherLib, ouvrez DirectorySearcher.cs.</span><span class="sxs-lookup"><span data-stu-id="7814a-148">In the DirectorySearcherLib project, open DirectorySearcher.cs.</span></span>
3. <span data-ttu-id="7814a-149">Remplacez les valeurs de membre de classe par les valeurs que vous avez entrées sur le Portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7814a-149">Replace the class member values with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="7814a-150">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="7814a-150">Your code refers to these values whenever it uses ADAL.</span></span>

  * <span data-ttu-id="7814a-151">*tenant* est le domaine de votre client Azure AD (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="7814a-151">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="7814a-152">*clientId* est l’ID client de l’application, que vous avez copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="7814a-152">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
  * <span data-ttu-id="7814a-153">*returnUri* est l’URI de redirection que vous avez entré sur le portail (par exemple, http://DirectorySearcher).</span><span class="sxs-lookup"><span data-stu-id="7814a-153">The *returnUri* is the redirect URI that you entered in the portal (for example, http://DirectorySearcher).</span></span>

## <a name="step-4-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="7814a-154">Étape 4 : Utiliser la bibliothèque ADAL pour obtenir des jetons à partir d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="7814a-154">Step 4: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="7814a-155">Presque toute la logique d’authentification de l’application réside dans `DirectorySearcher.SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="7814a-155">Almost all of the app's authentication logic lies in `DirectorySearcher.SearchByAlias(...)`.</span></span> <span data-ttu-id="7814a-156">Dans les projets propres à la plateforme, la seule nécessité est de transmettre un paramètre contextuel à la PCL `DirectorySearcher`.</span><span class="sxs-lookup"><span data-stu-id="7814a-156">All that's necessary in the platform-specific projects is to pass a contextual parameter to the `DirectorySearcher` PCL.</span></span>

1. <span data-ttu-id="7814a-157">Ouvrez DirectorySearcher.cs et ajoutez un nouveau paramètre à la méthode `SearchByAlias(...)`.</span><span class="sxs-lookup"><span data-stu-id="7814a-157">Open DirectorySearcher.cs, and then add a new parameter to the `SearchByAlias(...)` method.</span></span> <span data-ttu-id="7814a-158">`IPlatformParameters` est le paramètre contextuel qui encapsule les objets propres à la plateforme que la bibliothèque ADAL doit authentifier.</span><span class="sxs-lookup"><span data-stu-id="7814a-158">`IPlatformParameters` is the contextual parameter that encapsulates the platform-specific objects that ADAL needs to perform the authentication.</span></span>

    ```C#
    public static async Task<List<User>> SearchByAlias(string alias, IPlatformParameters parent)
    {
    ```

2. <span data-ttu-id="7814a-159">Initialisez `AuthenticationContext`, la classe principale de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="7814a-159">Initialize `AuthenticationContext`, which is the primary class of ADAL.</span></span>  
<span data-ttu-id="7814a-160">Cette action fournit à la bibliothèque ADAL les coordonnées dont elle a besoin pour communiquer avec Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7814a-160">This action passes ADAL the coordinates it needs to communicate with Azure AD.</span></span>
3. <span data-ttu-id="7814a-161">Appelez `AcquireTokenAsync(...)`, qui accepte l’objet `IPlatformParameters` et appelle le flux d’authentification nécessaire pour renvoyer un jeton à l’application.</span><span class="sxs-lookup"><span data-stu-id="7814a-161">Call `AcquireTokenAsync(...)`, which accepts the `IPlatformParameters` object and invokes the authentication flow that's necessary to return a token to the app.</span></span>

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

    <span data-ttu-id="7814a-162">`AcquireTokenAsync(...)` tente tout d’abord de renvoyer un jeton pour la ressource demandée (l’API Graph dans ce cas) sans inviter les utilisateurs à entrer leurs informations d’identification (par le biais de la mise en cache ou de l’actualisation des anciens jetons).</span><span class="sxs-lookup"><span data-stu-id="7814a-162">`AcquireTokenAsync(...)` first attempts to return a token for the requested resource (the Graph API in this case) without prompting users to enter their credentials (via caching or refreshing old tokens).</span></span> <span data-ttu-id="7814a-163">Si nécessaire, il affiche la page de connexion d’Azure AD aux utilisateurs avant d’acquérir le jeton demandé.</span><span class="sxs-lookup"><span data-stu-id="7814a-163">As necessary, it shows users the Azure AD sign-in page before acquiring the requested token.</span></span>
4. <span data-ttu-id="7814a-164">Joignez le jeton d’accès à la demande de l’API Graph, dans l’en-tête **Autorisation** :</span><span class="sxs-lookup"><span data-stu-id="7814a-164">Attach the access token to the Graph API request in the **Authorization** header:</span></span>

    ```C#
    ...
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
    ...
    ```

<span data-ttu-id="7814a-165">Le rôle de la PCL `DirectorySearcher` et du code lié à l’identité de l’application s’arrête là.</span><span class="sxs-lookup"><span data-stu-id="7814a-165">That's all for the `DirectorySearcher` PCL and the app's identity-related code.</span></span> <span data-ttu-id="7814a-166">Il ne reste qu’à appeler la méthode `SearchByAlias(...)` dans les affichages de chaque plateforme et, le cas échéant, à ajouter le code permettant de gérer correctement le cycle de vie de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7814a-166">All that remains is to call the `SearchByAlias(...)` method in each platform's views and, where necessary, to add code for correctly handling the UI lifecycle.</span></span>

### <a name="android"></a><span data-ttu-id="7814a-167">Android</span><span class="sxs-lookup"><span data-stu-id="7814a-167">Android</span></span>
1. <span data-ttu-id="7814a-168">Dans MainActivity.cs, ajoutez un appel à `SearchByAlias(...)` dans le gestionnaire de clic de bouton :</span><span class="sxs-lookup"><span data-stu-id="7814a-168">In MainActivity.cs, add a call to `SearchByAlias(...)` in the button click handler:</span></span>

    ```C#
    List<User> results = await DirectorySearcher.SearchByAlias(searchTermText.Text, new PlatformParameters(this));
    ```
2. <span data-ttu-id="7814a-169">Substituez la méthode du cycle de vie `OnActivityResult` pour rediriger toute authentification vers la méthode appropriée.</span><span class="sxs-lookup"><span data-stu-id="7814a-169">Override the `OnActivityResult` lifecycle method to forward any authentication redirects back to the appropriate method.</span></span> <span data-ttu-id="7814a-170">La bibliothèque ADAL fournit une méthode d’assistance pour cela dans Android :</span><span class="sxs-lookup"><span data-stu-id="7814a-170">ADAL provides a helper method for this in Android:</span></span>

    ```C#
    ...
    protected override void OnActivityResult(int requestCode, Result resultCode, Intent data)
    {
        base.OnActivityResult(requestCode, resultCode, data);
        AuthenticationAgentContinuationHelper.SetAuthenticationAgentContinuationEventArgs(requestCode, resultCode, data);
    }
    ...
    ```

### <a name="windows-desktop"></a><span data-ttu-id="7814a-171">Windows Desktop</span><span class="sxs-lookup"><span data-stu-id="7814a-171">Windows Desktop</span></span>
<span data-ttu-id="7814a-172">Dans MainWindow.xaml.cs, appelez simplement `SearchByAlias(...)` en passant un `WindowInteropHelper` dans l’objet `PlatformParameters` du bureau :</span><span class="sxs-lookup"><span data-stu-id="7814a-172">In MainWindow.xaml.cs, make a call to `SearchByAlias(...)` by passing a `WindowInteropHelper` in the desktop's `PlatformParameters` object:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

#### <a name="ios"></a><span data-ttu-id="7814a-173">iOS</span><span class="sxs-lookup"><span data-stu-id="7814a-173">iOS</span></span>
<span data-ttu-id="7814a-174">Dans DirSearchClient_iOSViewController.cs, l’objet `PlatformParameters` iOS prend une référence au contrôleur d’affichage :</span><span class="sxs-lookup"><span data-stu-id="7814a-174">In DirSearchClient_iOSViewController.cs, the iOS `PlatformParameters` object takes a reference to the View Controller:</span></span>

```C#
List<User> results = await DirectorySearcher.SearchByAlias(
  SearchTermText.Text,
  new PlatformParameters(PromptBehavior.Auto, this.Handle));
```

### <a name="windows-universal"></a><span data-ttu-id="7814a-175">Windows Universal</span><span class="sxs-lookup"><span data-stu-id="7814a-175">Windows Universal</span></span>
<span data-ttu-id="7814a-176">Dans Windows Universal, ouvrez MainPage.xaml.cs et implémentez la méthode `Search`.</span><span class="sxs-lookup"><span data-stu-id="7814a-176">In Windows Universal, open MainPage.xaml.cs, and then implement the `Search` method.</span></span> <span data-ttu-id="7814a-177">Cette méthode utilise une méthode auxiliaire dans un projet partagé pour mettre à jour l’interface utilisateur en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="7814a-177">This method uses a helper method in a shared project to update UI as necessary.</span></span>

```C#
...
List<User> results = await DirectorySearcherLib.DirectorySearcher.SearchByAlias(SearchTermText.Text, new PlatformParameters(PromptBehavior.Auto, false));
...
```

## <a name="whats-next"></a><span data-ttu-id="7814a-178">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7814a-178">What's next</span></span>
<span data-ttu-id="7814a-179">Vous disposez maintenant d’une application Xamarin fonctionnelle capable d’authentifier les utilisateurs et d’appeler en toute sécurité les API web à l’aide d’OAuth 2.0 sur cinq plateformes différentes.</span><span class="sxs-lookup"><span data-stu-id="7814a-179">You now have a working Xamarin app that can authenticate users and securely call web APIs by using OAuth 2.0 across five different platforms.</span></span>

<span data-ttu-id="7814a-180">Si vous n’avez pas encore rempli votre client avec des utilisateurs, il est maintenant temps de le faire.</span><span class="sxs-lookup"><span data-stu-id="7814a-180">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>

1. <span data-ttu-id="7814a-181">Exécutez votre application DirectorySearcher, puis connectez-vous avec l’un des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="7814a-181">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="7814a-182">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="7814a-182">Search for other users based on their UPN.</span></span>

<span data-ttu-id="7814a-183">La bibliothèque ADAL facilite l’intégration des fonctionnalités d’identité communes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="7814a-183">ADAL makes it easy to incorporate common identity features into the app.</span></span> <span data-ttu-id="7814a-184">Elle effectue les tâches ingrates à votre place, notamment la gestion du cache, la prise en charge du protocole OAuth, la présentation d’une interface utilisateur de connexion à l’utilisateur et l’actualisation des jetons expirés.</span><span class="sxs-lookup"><span data-stu-id="7814a-184">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="7814a-185">Vous n’avez besoin de connaître qu’un seul appel d’API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="7814a-185">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="7814a-186">Pour référence, téléchargez [l’exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (sans vos valeurs de configuration).</span><span class="sxs-lookup"><span data-stu-id="7814a-186">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-DotNet/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="7814a-187">Vous pouvez à présent aborder d’autres scénarios d’identité.</span><span class="sxs-lookup"><span data-stu-id="7814a-187">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="7814a-188">Par exemple, essayez de [Sécuriser une API web .NET avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="7814a-188">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
