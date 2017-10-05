---
title: "Bien démarrer avec Azure AD Windows Store | Microsoft Docs"
description: "Créez des applications Windows Store qui s’intègrent avec Azure AD pour la connexion et appellent des API protégées par Azure AD en utilisant OAuth."
services: active-directory
documentationcenter: windows
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 3b96a6d1-270b-4ac1-b9b5-58070c896a68
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 09/16/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 6b5189dc06d7f8b0ed4426944948b904feba847e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="cd36d-103">Intégration d’Azure AD avec des applications Windows Store</span><span class="sxs-lookup"><span data-stu-id="cd36d-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="cd36d-104">Les projets du Windows Store 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cd36d-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="cd36d-105">Pour en savoir plus, consultez [Ciblage et compatibilité de la plateforme Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="cd36d-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="cd36d-106">Si vous développez des applications pour Windows Store, Azure Active Directory (Azure AD) facilite l’authentification de vos utilisateurs avec leurs comptes Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cd36d-106">If you're developing apps for the Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward to authenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="cd36d-107">Grâce à l’intégration avec Azure AD, une application peut utiliser en toute sécurité une API web qui est protégée par Azure AD, telle que les API Office 365 ou l’API Azure.</span><span class="sxs-lookup"><span data-stu-id="cd36d-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="cd36d-108">Pour les applications de bureau Windows Store qui doivent accéder à des ressources protégées, Azure AD fournit la bibliothèque d’authentification Active Directory (ADAL).</span><span class="sxs-lookup"><span data-stu-id="cd36d-108">For Windows Store desktop apps that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="cd36d-109">Cette bibliothèque a pour seule fonction de simplifier l’obtention des jetons d’accès pour l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-109">The sole purpose of ADAL is to make it easy for the app to get access tokens.</span></span> <span data-ttu-id="cd36d-110">Pour illustrer cette simplicité, cet article montre comment créer une application Windows Store DirectorySearcher effectuant les actions suivantes :</span><span class="sxs-lookup"><span data-stu-id="cd36d-110">To demonstrate how easy it is, this article shows how to build a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="cd36d-111">obtention de jetons d’accès pour appeler l’API Graph Azure AD à l’aide du [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx) ;</span><span class="sxs-lookup"><span data-stu-id="cd36d-111">Gets access tokens for calling the Azure AD Graph API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="cd36d-112">recherche, dans un répertoire, d’utilisateurs correspondant à un nom d’utilisateur principal (UPN) donné ;</span><span class="sxs-lookup"><span data-stu-id="cd36d-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="cd36d-113">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cd36d-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="cd36d-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="cd36d-114">Before you get started</span></span>
* <span data-ttu-id="cd36d-115">Téléchargez la [structure du projet](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip) ou l’[exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="cd36d-115">Download the [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="cd36d-116">Chaque téléchargement est une solution Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="cd36d-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="cd36d-117">Vous avez également besoin d’un locataire Azure AD dans lequel créer les utilisateurs et inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-117">You also need an Azure AD tenant in which to create users and register the app.</span></span> <span data-ttu-id="cd36d-118">Si vous ne disposez pas encore d’un client, [découvrez comment en obtenir un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="cd36d-118">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="cd36d-119">Lorsque vous êtes prêt, suivez les procédures des trois sections qui suivent.</span><span class="sxs-lookup"><span data-stu-id="cd36d-119">When you are ready, follow the procedures in the next three sections.</span></span>

## <a name="step-1-register-the-directorysearcher-app"></a><span data-ttu-id="cd36d-120">Étape 1 : Inscrire l’application DirectorySearcher</span><span class="sxs-lookup"><span data-stu-id="cd36d-120">Step 1: Register the DirectorySearcher app</span></span>
<span data-ttu-id="cd36d-121">Pour autoriser l’application à obtenir des jetons, vous devez tout d’abord l’inscrire dans votre locataire Azure AD et lui accorder l’autorisation d’accéder à l’API Graph Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd36d-121">To enable the app to get tokens, you first need to register it in your Azure AD tenant and grant it permission to access the Azure AD Graph API.</span></span> <span data-ttu-id="cd36d-122">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="cd36d-122">Here's how:</span></span>

1. <span data-ttu-id="cd36d-123">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd36d-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cd36d-124">Dans la barre supérieure, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="cd36d-124">On the top bar, click your account.</span></span> <span data-ttu-id="cd36d-125">Puis, dans la liste **Annuaire**, sélectionnez le client Active Directory dans lequel vous voulez inscrire l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-125">Then, under the **Directory** list, select the Active Directory tenant where you want to register the app.</span></span>
3. <span data-ttu-id="cd36d-126">Dans le volet gauche, cliquez sur **Plus de services**, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd36d-126">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="cd36d-127">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cd36d-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="cd36d-128">Suivez les invites à l’écran pour créer une **application cliente native**.</span><span class="sxs-lookup"><span data-stu-id="cd36d-128">Follow the prompts to create a **Native Client Application**.</span></span>
  * <span data-ttu-id="cd36d-129">Le champ **Nom** décrit l’application aux utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cd36d-129">**Name** describes the app to users.</span></span>
  * <span data-ttu-id="cd36d-130">L’**URI de redirection** est une combinaison de schémas et de chaînes qu’Azure AD utilise pour renvoyer des réponses concernant les jetons.</span><span class="sxs-lookup"><span data-stu-id="cd36d-130">**Redirect URI** is a scheme and string combination that Azure AD uses to return token responses.</span></span> <span data-ttu-id="cd36d-131">Entrez une valeur d’espace réservé pour l’instant (par exemple, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="cd36d-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="cd36d-132">Vous remplacerez cette valeur ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="cd36d-132">You'll replace the value later.</span></span>
6. <span data-ttu-id="cd36d-133">Une fois que vous avez terminé l’inscription, Azure AD affecte un ID d’application unique à l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-133">After you’ve completed the registration, Azure AD assigns the app a unique application ID.</span></span> <span data-ttu-id="cd36d-134">Copiez la valeur dans l’onglet **Application**, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="cd36d-134">Copy the value on the **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="cd36d-135">Dans la page **Paramètres**, sélectionnez **Autorisations requises**, puis **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="cd36d-135">On the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="cd36d-136">Pour l’application **Azure Active Directory**, sélectionnez **Microsoft Graph** comme API.</span><span class="sxs-lookup"><span data-stu-id="cd36d-136">For the **Azure Active Directory** app, select **Microsoft Graph** as the API.</span></span>
9. <span data-ttu-id="cd36d-137">Sous **Autorisations déléguées**, ajoutez l’autorisation **Accéder au répertoire en tant qu’utilisateur actuellement connecté**.</span><span class="sxs-lookup"><span data-stu-id="cd36d-137">Under **Delegated Permissions**, add the **Access the directory as the signed-in user** permission.</span></span> <span data-ttu-id="cd36d-138">Cela permet à l’application d’interroger l’API Graph pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cd36d-138">Doing so enables the app to query the Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="cd36d-139">Étape 2 : Installer et configurer la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="cd36d-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="cd36d-140">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="cd36d-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="cd36d-141">Pour que la bibliothèque ADAL puisse communiquer avec Azure AD, fournissez-lui des informations sur l’inscription des applications.</span><span class="sxs-lookup"><span data-stu-id="cd36d-141">To enable ADAL to communicate with Azure AD, give it some information about the app registration.</span></span>

1. <span data-ttu-id="cd36d-142">Ajoutez ADAL au projet DirectorySearcher à l’aide de la console du gestionnaire de package.</span><span class="sxs-lookup"><span data-stu-id="cd36d-142">Add ADAL to the DirectorySearcher project by using the Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="cd36d-143">Dans le projet DirectorySearcher, ouvrez MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="cd36d-143">In the DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="cd36d-144">Remplacez les valeurs dans la région **Valeurs de configuration** par les valeurs que vous avez entrées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="cd36d-144">Replace the values in the **Config Values** region with the values that you entered in the Azure portal.</span></span> <span data-ttu-id="cd36d-145">Votre code se réfère à ces valeurs chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="cd36d-145">Your code refers to these values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="cd36d-146">*tenant* est le domaine de votre client Azure AD (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="cd36d-146">The *tenant* is the domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="cd36d-147">Le *clientId* est l’ID client de l’application, que vous avez copié à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="cd36d-147">The *clientId* is the client ID of the app, which you copied from the portal.</span></span>
4. <span data-ttu-id="cd36d-148">Vous devez maintenant découvrir l’URI de rappel pour votre application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="cd36d-148">You now need to discover the callback URI for your Windows Store app.</span></span> <span data-ttu-id="cd36d-149">Définissez un point d’arrêt sur cette ligne dans la méthode `MainPage` :</span><span class="sxs-lookup"><span data-stu-id="cd36d-149">Set a breakpoint on this line in the `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="cd36d-150">Générez la solution en vous assurant que toutes les références de package sont restaurées.</span><span class="sxs-lookup"><span data-stu-id="cd36d-150">Build the solution, making sure that all package references are restored.</span></span> <span data-ttu-id="cd36d-151">Si des packages sont manquants, ouvrez le Gestionnaire de package NuGet et restaurez-les.</span><span class="sxs-lookup"><span data-stu-id="cd36d-151">If any packages are missing, open the NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="cd36d-152">Exécutez l’application et copiez la valeur de `redirectUri` lorsque le point d’arrêt est atteint.</span><span class="sxs-lookup"><span data-stu-id="cd36d-152">Run the app, and copy the value of `redirectUri` when the breakpoint is hit.</span></span> <span data-ttu-id="cd36d-153">La valeur doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="cd36d-153">The value should look something like the following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="cd36d-154">De nouveau sous l’onglet **Paramètres** de l’application dans le portail Azure, ajoutez une **URI de redirection** avec la valeur précédente.</span><span class="sxs-lookup"><span data-stu-id="cd36d-154">Back on the **Settings** tab of the app in the Azure portal, add a **RedirectUri** with the preceding value.</span></span>  

## <a name="step-3-use-adal-to-get-tokens-from-azure-ad"></a><span data-ttu-id="cd36d-155">Étape 3 : Utiliser la bibliothèque ADAL pour obtenir des jetons à partir d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd36d-155">Step 3: Use ADAL to get tokens from Azure AD</span></span>
<span data-ttu-id="cd36d-156">Le principe de base de la bibliothèque ADAL consiste simplement à appeler `authContext.AcquireToken(…)` chaque fois que l’application a besoin d’un jeton d’accès, et la bibliothèque ADAL s’occupe du reste.</span><span class="sxs-lookup"><span data-stu-id="cd36d-156">The basic principle behind ADAL is that whenever the app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does the rest.</span></span>  

1. <span data-ttu-id="cd36d-157">Initialisez le `AuthenticationContext` de l’application, qui est la classe principale de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="cd36d-157">Initialize the app’s `AuthenticationContext`, which is the primary class of ADAL.</span></span> <span data-ttu-id="cd36d-158">Cette action fournit à la bibliothèque ADAL les coordonnées dont elle a besoin pour communiquer avec Azure AD et lui indique comment mettre en cache des jetons.</span><span class="sxs-lookup"><span data-stu-id="cd36d-158">This action passes ADAL the coordinates it needs to communicate with Azure AD and tell it how to cache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="cd36d-159">Recherchez la méthode `Search(...)`, qui est appelée lorsque les utilisateurs cliquent sur le bouton **Rechercher** dans l’interface utilisateur de l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-159">Locate the `Search(...)` method, which is invoked when users click the **Search** button on the app's UI.</span></span> <span data-ttu-id="cd36d-160">Cette méthode effectue une demande GET auprès de l’API Graph Azure AD pour l’interroger à propos d’utilisateurs dont l’UPN commence par le terme de recherche donné.</span><span class="sxs-lookup"><span data-stu-id="cd36d-160">This method makes a get request to the Azure AD Graph API to query for users whose UPN begins with the given search term.</span></span> <span data-ttu-id="cd36d-161">Pour interroger l’API Graph, incluez un jeton d’accès dans l’en-tête **Autorisation** de la demande.</span><span class="sxs-lookup"><span data-stu-id="cd36d-161">To query the Graph API, include an access token in the request's **Authorization** header.</span></span> <span data-ttu-id="cd36d-162">C’est là où la bibliothèque ADAL entre en jeu.</span><span class="sxs-lookup"><span data-stu-id="cd36d-162">This is where ADAL comes in.</span></span>

    ```C#
    private async void Search(object sender, RoutedEventArgs e)
    {
        ...
        AuthenticationResult result = null;
        try
        {
            result = await authContext.AcquireTokenAsync(graphResourceId, clientId, redirectURI, new PlatformParameters(PromptBehavior.Auto, false));
        }
        catch (AdalException ex)
        {
            if (ex.ErrorCode != "authentication_canceled")
            {
                ShowAuthError(string.Format("If the error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="cd36d-163">Lorsque l’application demande un jeton en appelant `AcquireTokenAsync(...)`, la bibliothèque ADAL tente de renvoyer un jeton sans demander à l’utilisateur ses informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="cd36d-163">When the app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts to return a token without asking the user for credentials.</span></span> <span data-ttu-id="cd36d-164">Si la bibliothèque ADAL détermine que l’utilisateur doit se connecter pour obtenir un jeton, elle affiche une boîte de dialogue de connexion, récupère les informations d’identification de l’utilisateur et renvoie un jeton lorsque l’authentification réussit.</span><span class="sxs-lookup"><span data-stu-id="cd36d-164">If ADAL determines that the user needs to sign in to get a token, it displays a sign-in dialog box, collects the user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="cd36d-165">Si la bibliothèque ADAL ne peut pas renvoyer un jeton pour une raison quelconque, l’état *AuthenticationResult* est une erreur.</span><span class="sxs-lookup"><span data-stu-id="cd36d-165">If ADAL is unable to return a token for any reason, the *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="cd36d-166">Il est à présent temps d’utiliser le jeton d’accès que vous venez d’acquérir.</span><span class="sxs-lookup"><span data-stu-id="cd36d-166">Now it's time to use the access token you just acquired.</span></span> <span data-ttu-id="cd36d-167">Également dans la méthode `Search(...)`, joignez le jeton à la demande GET de l’API Graph, dans l’en-tête **Autorisation** :</span><span class="sxs-lookup"><span data-stu-id="cd36d-167">Also in the `Search(...)` method, attach the token to the Graph API get request in the **Authorization** header:</span></span>

    ```C#
    // Add the access token to the Authorization header of the call to the Graph API, and call the Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="cd36d-168">Vous pouvez utiliser l’objet `AuthenticationResult` pour afficher des informations concernant l’utilisateur dans l’application, par exemple l’ID de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="cd36d-168">You can use the `AuthenticationResult` object to display information about the user in the app, such as the user's ID:</span></span>

    ```C#
    // Update the page UI to represent the signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="cd36d-169">Vous pouvez également utiliser la bibliothèque ADAL pour déconnecter des utilisateurs de l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-169">You can also use ADAL to sign users out of the app.</span></span> <span data-ttu-id="cd36d-170">Lorsque l’utilisateur clique sur le bouton **Déconnexion**, vérifiez que l’appel suivant vers `AcquireTokenAsync(...)` affiche une fenêtre de connexion.</span><span class="sxs-lookup"><span data-stu-id="cd36d-170">When the user clicks the **Sign Out** button, ensure that the next call to `AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="cd36d-171">Avec la bibliothèque ADAL, cette action aussi simple que d’effacer le cache de jeton :</span><span class="sxs-lookup"><span data-stu-id="cd36d-171">With ADAL, this action is as easy as clearing the token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from the token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="cd36d-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cd36d-172">What's next</span></span>
<span data-ttu-id="cd36d-173">Vous disposez maintenant d’une application Windows Store pouvant authentifier les utilisateurs, appeler en toute sécurité les API web à l’aide d’OAuth 2.0 et obtenir des informations de base concernant l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cd36d-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about the user.</span></span>

<span data-ttu-id="cd36d-174">Si vous n’avez pas encore rempli votre locataire avec des utilisateurs, il est maintenant temps de le faire.</span><span class="sxs-lookup"><span data-stu-id="cd36d-174">If you haven’t already populated your tenant with users, now is the time to do so.</span></span>
1. <span data-ttu-id="cd36d-175">Exécutez votre application DirectorySearcher, puis connectez-vous avec l’un des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="cd36d-175">Run your DirectorySearcher app, and then sign in with one of the users.</span></span>
2. <span data-ttu-id="cd36d-176">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="cd36d-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="cd36d-177">Fermez l’application et réexécutez-la.</span><span class="sxs-lookup"><span data-stu-id="cd36d-177">Close the app, and rerun it.</span></span> <span data-ttu-id="cd36d-178">Observez que la session utilisateur reste identique.</span><span class="sxs-lookup"><span data-stu-id="cd36d-178">Notice how the user’s session remains intact.</span></span>
4. <span data-ttu-id="cd36d-179">Déconnectez-vous par un clic droit pour afficher la barre inférieure, puis reconnectez-vous sous le nom d’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="cd36d-179">Sign out by right-clicking to display the bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="cd36d-180">La bibliothèque ADAL facilite l’intégration de toutes ces fonctionnalités d’identité communes dans l’application.</span><span class="sxs-lookup"><span data-stu-id="cd36d-180">ADAL makes it easy to incorporate all these common identity features into the app.</span></span> <span data-ttu-id="cd36d-181">Elle effectue les tâches ingrates pour vous, telles que gestion du cache, prise en charge du protocole OAuth, présentation d’une interface utilisateur de connexion à l’utilisateur et actualisation des jetons expirés.</span><span class="sxs-lookup"><span data-stu-id="cd36d-181">It takes care of all the dirty work for you, such as cache management, OAuth protocol support, presenting the user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="cd36d-182">Vous n’avez besoin de connaître qu’un seul appel d’API, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="cd36d-182">You need to know only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="cd36d-183">Pour référence, téléchargez [l’exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sans vos valeurs de configuration).</span><span class="sxs-lookup"><span data-stu-id="cd36d-183">For reference, download the [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="cd36d-184">Vous pouvez à présent aborder d’autres scénarios d’identité.</span><span class="sxs-lookup"><span data-stu-id="cd36d-184">You can now move on to additional identity scenarios.</span></span> <span data-ttu-id="cd36d-185">Par exemple, essayez de [Sécuriser une API web .NET avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cd36d-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
