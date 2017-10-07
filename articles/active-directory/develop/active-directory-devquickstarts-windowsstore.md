---
title: aaaAzure AD du Windows Store prise en main | Documents Microsoft
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
ms.openlocfilehash: 1d12c7b928bc0e94fb823f8db4a09ff416205e2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-windows-store-apps"></a><span data-ttu-id="29950-103">Intégration d’Azure AD avec des applications Windows Store</span><span class="sxs-lookup"><span data-stu-id="29950-103">Integrate Azure AD with Windows Store apps</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

> [!NOTE]
> <span data-ttu-id="29950-104">Les projets du Windows Store 8.1 et des versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="29950-104">Windows Store 8.1 and prior version projects are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="29950-105">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="29950-105">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

<span data-ttu-id="29950-106">Si vous développez des applications pour hello du Windows Store, Azure Active Directory (Azure AD) rend très simple tooauthenticate vos utilisateurs avec leurs comptes Active Directory.</span><span class="sxs-lookup"><span data-stu-id="29950-106">If you're developing apps for hello Windows Store, Azure Active Directory (Azure AD) makes it simple and straightforward tooauthenticate your users with their Active Directory accounts.</span></span> <span data-ttu-id="29950-107">En intégrant avec Azure AD, une application peut utiliser en toute sécurité de toutes les API qui est protégé par Azure AD, telles que hello API Office 365 ou hello Azure API web.</span><span class="sxs-lookup"><span data-stu-id="29950-107">By integrating with Azure AD, an app can securely consume any web API that's protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="29950-108">Pour les applications bureautiques Windows Store qui ont besoin de ressources de tooaccess protégé, Azure AD fournit hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="29950-108">For Windows Store desktop apps that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="29950-109">Hello seul but de la bibliothèque ADAL est toomake plus facile pour les jetons d’accès tooget application hello.</span><span class="sxs-lookup"><span data-stu-id="29950-109">hello sole purpose of ADAL is toomake it easy for hello app tooget access tokens.</span></span> <span data-ttu-id="29950-110">toodemonstrate il s’agit, cet article explique comment toobuild un DirectorySearcher Windows Store facilement application qui :</span><span class="sxs-lookup"><span data-stu-id="29950-110">toodemonstrate how easy it is, this article shows how toobuild a DirectorySearcher Windows Store app that:</span></span>

* <span data-ttu-id="29950-111">Obtient les jetons pour l’appel d’API d’Azure AD Graph hello à l’aide de hello d’accès [protocole d’authentification OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="29950-111">Gets access tokens for calling hello Azure AD Graph API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="29950-112">recherche, dans un répertoire, d’utilisateurs correspondant à un nom d’utilisateur principal (UPN) donné ;</span><span class="sxs-lookup"><span data-stu-id="29950-112">Searches a directory for users with a given user principal name (UPN).</span></span>
* <span data-ttu-id="29950-113">déconnexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="29950-113">Signs users out.</span></span>

## <a name="before-you-get-started"></a><span data-ttu-id="29950-114">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="29950-114">Before you get started</span></span>
* <span data-ttu-id="29950-115">Télécharger hello [projet squelette](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), ou télécharger hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="29950-115">Download hello [skeleton project](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/skeleton.zip), or download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip).</span></span> <span data-ttu-id="29950-116">Chaque téléchargement est une solution Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="29950-116">Each download is a Visual Studio 2015 solution.</span></span>
* <span data-ttu-id="29950-117">Vous devez également un locataire Azure AD dans lequel les utilisateurs de toocreate et inscrire l’application hello.</span><span class="sxs-lookup"><span data-stu-id="29950-117">You also need an Azure AD tenant in which toocreate users and register hello app.</span></span> <span data-ttu-id="29950-118">Si vous n’avez pas encore un client, [apprendre comment tooget un](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="29950-118">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="29950-119">Lorsque vous êtes prêt, suivez les procédures de hello dans hello trois sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="29950-119">When you are ready, follow hello procedures in hello next three sections.</span></span>

## <a name="step-1-register-hello-directorysearcher-app"></a><span data-ttu-id="29950-120">Étape 1 : Inscrire l’application DirectorySearcher hello</span><span class="sxs-lookup"><span data-stu-id="29950-120">Step 1: Register hello DirectorySearcher app</span></span>
<span data-ttu-id="29950-121">jetons de tooget tooenable hello application, vous devez tout d’abord tooregister dans votre annuaire Azure AD de client et de lui accorder hello de tooaccess autorisation API Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="29950-121">tooenable hello app tooget tokens, you first need tooregister it in your Azure AD tenant and grant it permission tooaccess hello Azure AD Graph API.</span></span> <span data-ttu-id="29950-122">Voici comment procéder :</span><span class="sxs-lookup"><span data-stu-id="29950-122">Here's how:</span></span>

1. <span data-ttu-id="29950-123">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="29950-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="29950-124">Sur la barre supérieure de hello, cliquez sur votre compte.</span><span class="sxs-lookup"><span data-stu-id="29950-124">On hello top bar, click your account.</span></span> <span data-ttu-id="29950-125">Ensuite, sous hello **répertoire** liste, le client d’Active Directory hello sélectionnez où vous souhaitez tooregister hello application.</span><span class="sxs-lookup"><span data-stu-id="29950-125">Then, under hello **Directory** list, select hello Active Directory tenant where you want tooregister hello app.</span></span>
3. <span data-ttu-id="29950-126">Cliquez sur **plus Services** dans hello du volet gauche, puis sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29950-126">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="29950-127">Cliquez sur **Inscriptions des applications**, puis sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="29950-127">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="29950-128">Suivez hello invites toocreate un **Application cliente Native**.</span><span class="sxs-lookup"><span data-stu-id="29950-128">Follow hello prompts toocreate a **Native Client Application**.</span></span>
  * <span data-ttu-id="29950-129">**Nom** décrit hello application toousers.</span><span class="sxs-lookup"><span data-stu-id="29950-129">**Name** describes hello app toousers.</span></span>
  * <span data-ttu-id="29950-130">**URI de redirection** est une combinaison de schéma et de la chaîne que Azure AD utilise des réponses de jeton tooreturn.</span><span class="sxs-lookup"><span data-stu-id="29950-130">**Redirect URI** is a scheme and string combination that Azure AD uses tooreturn token responses.</span></span> <span data-ttu-id="29950-131">Entrez une valeur d’espace réservé pour l’instant (par exemple, **http://DirectorySearcher**).</span><span class="sxs-lookup"><span data-stu-id="29950-131">Enter a placeholder value for now (for example, **http://DirectorySearcher**).</span></span> <span data-ttu-id="29950-132">Vous allez remplacer les valeur hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="29950-132">You'll replace hello value later.</span></span>
6. <span data-ttu-id="29950-133">Une fois que vous avez terminé l’inscription de hello, Azure AD assigne application hello un ID d’application unique.</span><span class="sxs-lookup"><span data-stu-id="29950-133">After you’ve completed hello registration, Azure AD assigns hello app a unique application ID.</span></span> <span data-ttu-id="29950-134">Copier la valeur hello sur hello **Application** sous l’onglet, car vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="29950-134">Copy hello value on hello **Application** tab, because you'll need it later.</span></span>
7. <span data-ttu-id="29950-135">Sur hello **paramètres** page, sélectionnez **autorisations requises**, puis sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="29950-135">On hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>
8. <span data-ttu-id="29950-136">Pourquoi **Azure Active Directory** application, sélectionnez **Microsoft Graph** comme hello API.</span><span class="sxs-lookup"><span data-stu-id="29950-136">For hello **Azure Active Directory** app, select **Microsoft Graph** as hello API.</span></span>
9. <span data-ttu-id="29950-137">Sous **autorisations déléguées**, ajouter hello **répertoire de hello Access en tant qu’utilisateur connecté hello** autorisation.</span><span class="sxs-lookup"><span data-stu-id="29950-137">Under **Delegated Permissions**, add hello **Access hello directory as hello signed-in user** permission.</span></span> <span data-ttu-id="29950-138">Ainsi, tooquery hello API Graph de hello application pour les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="29950-138">Doing so enables hello app tooquery hello Graph API for users.</span></span>

## <a name="step-2-install-and-configure-adal"></a><span data-ttu-id="29950-139">Étape 2 : Installer et configurer la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="29950-139">Step 2: Install and configure ADAL</span></span>
<span data-ttu-id="29950-140">Maintenant que vous disposez d’une application dans Azure AD, vous pouvez installer la bibliothèque ADAL et écrire votre code lié à l’identité.</span><span class="sxs-lookup"><span data-stu-id="29950-140">Now that you have an app in Azure AD, you can install ADAL and write your identity-related code.</span></span> <span data-ttu-id="29950-141">tooenable toocommunicate ADAL avec Azure AD, lui donner des informations sur l’inscription d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="29950-141">tooenable ADAL toocommunicate with Azure AD, give it some information about hello app registration.</span></span>

1. <span data-ttu-id="29950-142">Ajouter la bibliothèque ADAL toohello DirectorySearcher projet à l’aide de hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="29950-142">Add ADAL toohello DirectorySearcher project by using hello Package Manager Console.</span></span>

    ```
    PM> Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

2. <span data-ttu-id="29950-143">Dans le projet de DirectorySearcher hello, ouvrez MainPage.xaml.cs.</span><span class="sxs-lookup"><span data-stu-id="29950-143">In hello DirectorySearcher project, open MainPage.xaml.cs.</span></span>
3. <span data-ttu-id="29950-144">Remplacez les valeurs de hello en hello **les valeurs de configuration** région avec des valeurs hello que vous avez entré dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="29950-144">Replace hello values in hello **Config Values** region with hello values that you entered in hello Azure portal.</span></span> <span data-ttu-id="29950-145">Votre code fait référence à des valeurs de toothese chaque fois qu’il utilise la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="29950-145">Your code refers toothese values whenever it uses ADAL.</span></span>
  * <span data-ttu-id="29950-146">Hello *client* est domaine hello de votre client Azure AD (par exemple, contoso.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="29950-146">hello *tenant* is hello domain of your Azure AD tenant (for example, contoso.onmicrosoft.com).</span></span>
  * <span data-ttu-id="29950-147">Hello *clientId* est l’ID de client hello de l’application hello, que vous avez copié à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="29950-147">hello *clientId* is hello client ID of hello app, which you copied from hello portal.</span></span>
4. <span data-ttu-id="29950-148">Vous devez maintenant URI de rappel toodiscover hello pour votre application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="29950-148">You now need toodiscover hello callback URI for your Windows Store app.</span></span> <span data-ttu-id="29950-149">Définir un point d’arrêt sur cette ligne de hello `MainPage` méthode :</span><span class="sxs-lookup"><span data-stu-id="29950-149">Set a breakpoint on this line in hello `MainPage` method:</span></span>
    ```
    redirectURI = Windows.Security.Authentication.Web.WebAuthenticationBroker.GetCurrentApplicationCallbackUri();
    ```
5. <span data-ttu-id="29950-150">Générer la solution hello, s’assurer que toutes les références de package sont restaurés.</span><span class="sxs-lookup"><span data-stu-id="29950-150">Build hello solution, making sure that all package references are restored.</span></span> <span data-ttu-id="29950-151">Si tous les packages sont manquants, ouvrez le Gestionnaire de Package NuGet de hello et les restaurer.</span><span class="sxs-lookup"><span data-stu-id="29950-151">If any packages are missing, open hello NuGet Package Manager and restore them.</span></span>
6. <span data-ttu-id="29950-152">Exécuter l’application hello et copiez la valeur hello `redirectUri` lorsque hello point d’arrêt.</span><span class="sxs-lookup"><span data-stu-id="29950-152">Run hello app, and copy hello value of `redirectUri` when hello breakpoint is hit.</span></span> <span data-ttu-id="29950-153">valeur de Hello doit ressembler à hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="29950-153">hello value should look something like hello following:</span></span>

    ```
    ms-app://s-1-15-2-1352796503-54529114-405753024-3540103335-3203256200-511895534-1429095407/
    ```

7. <span data-ttu-id="29950-154">Retour sur hello **paramètres** onglet de l’application hello Bonjour portail Azure, ajoutez un **RedirectUri** avec hello précédant la valeur.</span><span class="sxs-lookup"><span data-stu-id="29950-154">Back on hello **Settings** tab of hello app in hello Azure portal, add a **RedirectUri** with hello preceding value.</span></span>  

## <a name="step-3-use-adal-tooget-tokens-from-azure-ad"></a><span data-ttu-id="29950-155">Étape 3 : Utiliser la bibliothèque ADAL tooget des jetons d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="29950-155">Step 3: Use ADAL tooget tokens from Azure AD</span></span>
<span data-ttu-id="29950-156">Bonjour principe de base derrière la bibliothèque ADAL est que chaque fois que l’application hello a besoin d’un jeton d’accès, il appelle simplement `authContext.AcquireToken(…)`, et la bibliothèque ADAL hello rest.</span><span class="sxs-lookup"><span data-stu-id="29950-156">hello basic principle behind ADAL is that whenever hello app needs an access token, it simply calls `authContext.AcquireToken(…)`, and ADAL does hello rest.</span></span>  

1. <span data-ttu-id="29950-157">Initialiser l’application hello `AuthenticationContext`, qui est la classe principale hello de la bibliothèque ADAL.</span><span class="sxs-lookup"><span data-stu-id="29950-157">Initialize hello app’s `AuthenticationContext`, which is hello primary class of ADAL.</span></span> <span data-ttu-id="29950-158">Cette action transmet les coordonnées hello ADAL il doit toocommunicate avec Azure AD et d’indiquer comment les jetons toocache.</span><span class="sxs-lookup"><span data-stu-id="29950-158">This action passes ADAL hello coordinates it needs toocommunicate with Azure AD and tell it how toocache tokens.</span></span>

    ```C#
    public MainPage()
    {
        ...

        authContext = new AuthenticationContext(authority);
    }
    ```

2. <span data-ttu-id="29950-159">Recherchez hello `Search(...)` (méthode), qui est appelé lorsque les utilisateurs cliquent sur hello **recherche** bouton sur l’interface utilisateur de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="29950-159">Locate hello `Search(...)` method, which is invoked when users click hello **Search** button on hello app's UI.</span></span> <span data-ttu-id="29950-160">Cette méthode rend un tooquery toohello API Azure AD Graph de demande get pour les utilisateurs dont les UPN commence par hello donné du terme de recherche.</span><span class="sxs-lookup"><span data-stu-id="29950-160">This method makes a get request toohello Azure AD Graph API tooquery for users whose UPN begins with hello given search term.</span></span> <span data-ttu-id="29950-161">tooquery hello API Graph, inclure un jeton d’accès dans la demande hello **autorisation** en-tête.</span><span class="sxs-lookup"><span data-stu-id="29950-161">tooquery hello Graph API, include an access token in hello request's **Authorization** header.</span></span> <span data-ttu-id="29950-162">C’est là où la bibliothèque ADAL entre en jeu.</span><span class="sxs-lookup"><span data-stu-id="29950-162">This is where ADAL comes in.</span></span>

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
                ShowAuthError(string.Format("If hello error continues, please contact your administrator.\n\nError: {0}\n\nError Description:\n\n{1}", ex.ErrorCode, ex.Message));
            }
            return;
        }
        ...
    }
    ```
    <span data-ttu-id="29950-163">Lorsque application hello demande un jeton en appelant `AcquireTokenAsync(...)`, la bibliothèque ADAL tente tooreturn un jeton sans demander hello pour les informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="29950-163">When hello app requests a token by calling `AcquireTokenAsync(...)`, ADAL attempts tooreturn a token without asking hello user for credentials.</span></span> <span data-ttu-id="29950-164">Si la bibliothèque ADAL détermine que l’utilisateur hello doit toosign dans tooget un jeton, il affiche une boîte de dialogue de connexion, collecte des informations d’identification de l’utilisateur hello et retourne un jeton après que l’authentification réussit.</span><span class="sxs-lookup"><span data-stu-id="29950-164">If ADAL determines that hello user needs toosign in tooget a token, it displays a sign-in dialog box, collects hello user's credentials, and returns a token after authentication succeeds.</span></span> <span data-ttu-id="29950-165">Si la bibliothèque ADAL est impossible de tooreturn un jeton pour une raison quelconque, hello *AuthenticationResult* état est une erreur.</span><span class="sxs-lookup"><span data-stu-id="29950-165">If ADAL is unable tooreturn a token for any reason, hello *AuthenticationResult* status is an error.</span></span>
3. <span data-ttu-id="29950-166">Il est maintenant de jeton d’accès hello toouse temps que vous venez d’acquérir.</span><span class="sxs-lookup"><span data-stu-id="29950-166">Now it's time toouse hello access token you just acquired.</span></span> <span data-ttu-id="29950-167">Également dans hello `Search(...)` (méthode), joindre toohello de jeton hello demande d’obtention de l’API Graph Bonjour **autorisation** en-tête :</span><span class="sxs-lookup"><span data-stu-id="29950-167">Also in hello `Search(...)` method, attach hello token toohello Graph API get request in hello **Authorization** header:</span></span>

    ```C#
    // Add hello access token toohello Authorization header of hello call toohello Graph API, and call hello Graph API.
    httpClient.DefaultRequestHeaders.Authorization = new HttpCredentialsHeaderValue("Bearer", result.AccessToken);

    ```
4. <span data-ttu-id="29950-168">Vous pouvez utiliser hello `AuthenticationResult` toodisplay informations utilisateur hello dans l’application hello, par exemple hello ID de l’utilisateur de l’objet :</span><span class="sxs-lookup"><span data-stu-id="29950-168">You can use hello `AuthenticationResult` object toodisplay information about hello user in hello app, such as hello user's ID:</span></span>

    ```C#
    // Update hello page UI toorepresent hello signed-in user
    ActiveUser.Text = result.UserInfo.DisplayableId;
    ```
5. <span data-ttu-id="29950-169">Vous pouvez également utiliser la bibliothèque ADAL toosign des utilisateurs en dehors de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="29950-169">You can also use ADAL toosign users out of hello app.</span></span> <span data-ttu-id="29950-170">Lorsque hello utilisateur clique sur hello **se déconnecter** bouton, assurez-vous qu’appel suivant hello trop`AcquireTokenAsync(...)` montre une vue de connexion.</span><span class="sxs-lookup"><span data-stu-id="29950-170">When hello user clicks hello **Sign Out** button, ensure that hello next call too`AcquireTokenAsync(...)` shows a sign-in view.</span></span> <span data-ttu-id="29950-171">La bibliothèque ADAL, cette action est aussi simple que l’effacement du cache de jetons hello :</span><span class="sxs-lookup"><span data-stu-id="29950-171">With ADAL, this action is as easy as clearing hello token cache:</span></span>

    ```C#
    private void SignOut()
    {
        // Clear session state from hello token cache.
        authContext.TokenCache.Clear();

        ...
    }
    ```

## <a name="whats-next"></a><span data-ttu-id="29950-172">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="29950-172">What's next</span></span>
<span data-ttu-id="29950-173">Vous disposez maintenant d’un application du Windows Store qui peut authentifier les utilisateurs, en toute sécurité appeler web API à l’aide d’OAuth 2.0 et obtenir des informations de base sur l’utilisateur de hello du travail.</span><span class="sxs-lookup"><span data-stu-id="29950-173">You now have a working Windows Store app that can authenticate users, securely call web APIs using OAuth 2.0, and get basic information about hello user.</span></span>

<span data-ttu-id="29950-174">Si vous n’avez pas déjà renseigné votre client avec les utilisateurs, est à présent hello temps toodo donc.</span><span class="sxs-lookup"><span data-stu-id="29950-174">If you haven’t already populated your tenant with users, now is hello time toodo so.</span></span>
1. <span data-ttu-id="29950-175">Exécuter votre application DirectorySearcher, puis connectez-vous avec l’un des utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="29950-175">Run your DirectorySearcher app, and then sign in with one of hello users.</span></span>
2. <span data-ttu-id="29950-176">Recherchez d’autres utilisateurs en fonction de leur UPN.</span><span class="sxs-lookup"><span data-stu-id="29950-176">Search for other users based on their UPN.</span></span>
3. <span data-ttu-id="29950-177">Fermez l’application hello et réexécutez-le.</span><span class="sxs-lookup"><span data-stu-id="29950-177">Close hello app, and rerun it.</span></span> <span data-ttu-id="29950-178">Notez que la session de l’utilisateur hello reste intacte.</span><span class="sxs-lookup"><span data-stu-id="29950-178">Notice how hello user’s session remains intact.</span></span>
4. <span data-ttu-id="29950-179">Se déconnecter en cliquant sur la barre inférieure de hello toodisplay et reconnectez-vous en tant qu’un autre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="29950-179">Sign out by right-clicking toodisplay hello bottom bar, and then sign back in as another user.</span></span>

<span data-ttu-id="29950-180">ADAL rend facile tooincorporate toutes ces fonctionnalités identité commune dans une application hello.</span><span class="sxs-lookup"><span data-stu-id="29950-180">ADAL makes it easy tooincorporate all these common identity features into hello app.</span></span> <span data-ttu-id="29950-181">Il s’occupe de tout le travail dirty hello, telles que la gestion du cache, prise en charge de protocole d’OAuth, présentant les utilisateur hello avec une connexion de l’interface utilisateur, et l’actualisation a expiré de jetons.</span><span class="sxs-lookup"><span data-stu-id="29950-181">It takes care of all hello dirty work for you, such as cache management, OAuth protocol support, presenting hello user with a login UI, and refreshing expired tokens.</span></span> <span data-ttu-id="29950-182">Vous devez tooknow uniquement une seule API appel, `authContext.AcquireToken*(…)`.</span><span class="sxs-lookup"><span data-stu-id="29950-182">You need tooknow only a single API call, `authContext.AcquireToken*(…)`.</span></span>

<span data-ttu-id="29950-183">Pour référence, téléchargez hello [exemple terminé](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (sans les valeurs de configuration).</span><span class="sxs-lookup"><span data-stu-id="29950-183">For reference, download hello [completed sample](https://github.com/AzureADQuickStarts/NativeClient-WindowsStore/archive/complete.zip) (without your configuration values).</span></span>

<span data-ttu-id="29950-184">Vous pouvez maintenant déplacer sur les scénarios d’identité tooadditional.</span><span class="sxs-lookup"><span data-stu-id="29950-184">You can now move on tooadditional identity scenarios.</span></span> <span data-ttu-id="29950-185">Par exemple, essayez de [Sécuriser une API web .NET avec Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="29950-185">For example, try [Secure a .NET Web API with Azure AD](active-directory-devquickstarts-webapi-dotnet.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
