---
title: Azure Active Directory B2C | Microsoft Docs
description: "Comment créer une application de bureau Windows comprenant connexion, inscription et gestion de profil à l’aide d’Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: .net
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 9da14362-8216-4485-960e-af17cd5ba3bd
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/07/2017
ms.author: dastrock
ms.openlocfilehash: 8e2b5c704230ee2ba1395dc76a1551aaa8e7af7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="90548-103">Azure AD B2C : création d’une application de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="90548-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="90548-104">Avec Azure Active Directory (Azure AD) B2C, vous pouvez ajouter de puissantes fonctionnalités de gestion des identités en libre-service à vos applications de bureau, en seulement quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="90548-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features to your desktop app in a few short steps.</span></span> <span data-ttu-id="90548-105">Cet article explique comment créer une application WPF (Windows Presentation Foundation) .NET de type « liste des tâches », qui inclut l’inscription d’utilisateur, la connexion et la gestion de profil.</span><span class="sxs-lookup"><span data-stu-id="90548-105">This article will show you how to create a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="90548-106">L’application prendra en charge l’inscription et la connexion à l’aide d’un nom d’utilisateur ou d’une adresse e-mail.</span><span class="sxs-lookup"><span data-stu-id="90548-106">The app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="90548-107">Elle prendra également en charge l’inscription et la connexion à l’aide d’un compte de réseau social comme Facebook et Google.</span><span class="sxs-lookup"><span data-stu-id="90548-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="90548-108">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="90548-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="90548-109">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="90548-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="90548-110">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="90548-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="90548-111">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="90548-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="90548-112">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="90548-112">Create an application</span></span>
<span data-ttu-id="90548-113">Vous devez maintenant créer dans votre répertoire B2C une application</span><span class="sxs-lookup"><span data-stu-id="90548-113">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="90548-114">fournissant à Azure AD certaines informations nécessaires pour communiquer de manière sécurisée avec votre application.</span><span class="sxs-lookup"><span data-stu-id="90548-114">This gives Azure AD information that it needs to securely communicate with your app.</span></span> <span data-ttu-id="90548-115">Pour créer une application, suivez [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="90548-115">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="90548-116">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="90548-116">Be sure to:</span></span>

* <span data-ttu-id="90548-117">Incluez un **client natif** dans l’application.</span><span class="sxs-lookup"><span data-stu-id="90548-117">Include a **native client** in the application.</span></span>
* <span data-ttu-id="90548-118">Copiez l’ **URI de redirection** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="90548-118">Copy the **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="90548-119">Il s’agit de l’URL par défaut pour cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="90548-119">It is the default URL for this code sample.</span></span>
* <span data-ttu-id="90548-120">Copiez **l’ID d’application** affecté à votre application.</span><span class="sxs-lookup"><span data-stu-id="90548-120">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="90548-121">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="90548-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="90548-122">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="90548-122">Create your policies</span></span>
<span data-ttu-id="90548-123">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="90548-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="90548-124">Cet exemple de code contient trois expériences liées à l’identité : l’inscription, la connexion et la modification du profil.</span><span class="sxs-lookup"><span data-stu-id="90548-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="90548-125">Vous devez créer une stratégie pour chaque type, comme décrit dans [l’article de référence sur les stratégies](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="90548-125">You need to create a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="90548-126">Lors de la création des trois stratégies, assurez-vous de :</span><span class="sxs-lookup"><span data-stu-id="90548-126">When you create the three policies, be sure to:</span></span>

* <span data-ttu-id="90548-127">Choisir **Inscription par le biais d’un ID utilisateur** ou **Inscription par le biais d’une adresse e-mail** dans le panneau des fournisseurs d’identité.</span><span class="sxs-lookup"><span data-stu-id="90548-127">Choose either **User ID sign-up** or **Email sign-up** in the identity providers blade.</span></span>
* <span data-ttu-id="90548-128">Choisir **Nom d’affichage** et d’autres attributs d’inscription dans votre stratégie d’inscription.</span><span class="sxs-lookup"><span data-stu-id="90548-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="90548-129">Choisir les revendications **Nom d’affichage** et **ID d’objet** comme revendications d’application pour chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="90548-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="90548-130">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="90548-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="90548-131">Copiez le **nom** de chaque stratégie après sa création.</span><span class="sxs-lookup"><span data-stu-id="90548-131">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="90548-132">Il doit porter le préfixe `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="90548-132">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="90548-133">Vous aurez besoin des noms de ces stratégies ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="90548-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="90548-134">Une fois vos trois stratégies créées, vous pouvez générer votre application.</span><span class="sxs-lookup"><span data-stu-id="90548-134">After you have successfully created the three policies, you're ready to build your app.</span></span>

## <a name="download-the-code"></a><span data-ttu-id="90548-135">Téléchargement du code</span><span class="sxs-lookup"><span data-stu-id="90548-135">Download the code</span></span>
<span data-ttu-id="90548-136">Le code associé à ce didacticiel [est stocké sur GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="90548-136">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="90548-137">Pour générer l’exemple à mesure que vous avancez, vous pouvez [télécharger une structure de projet sous la forme d’un fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="90548-137">To build the sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="90548-138">Vous pouvez également cloner la structure :</span><span class="sxs-lookup"><span data-stu-id="90548-138">You can also clone the skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="90548-139">L’application terminée est également [disponible en tant que fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou sur la branche `complete` du même référentiel.</span><span class="sxs-lookup"><span data-stu-id="90548-139">The completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on the `complete` branch of the same repository.</span></span>

<span data-ttu-id="90548-140">Une fois l’exemple de code téléchargé, ouvrez le fichier .sln Visual Studio pour commencer.</span><span class="sxs-lookup"><span data-stu-id="90548-140">After you download the sample code, open the Visual Studio .sln file to get started.</span></span> <span data-ttu-id="90548-141">Le projet `TaskClient` est l’application de bureau WPF avec laquelle l’utilisateur interagit.</span><span class="sxs-lookup"><span data-stu-id="90548-141">The `TaskClient` project is the WPF desktop application that the user interacts with.</span></span> <span data-ttu-id="90548-142">Dans le cadre de ce didacticiel, il appelle une API web de tâche principale, hébergée dans Azure, qui stocke la liste des actions de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90548-142">For the purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="90548-143">Vous n’avez pas besoin de créer l’API web, nous l’avons déjà exécutée pour vous.</span><span class="sxs-lookup"><span data-stu-id="90548-143">You do not need to build the web API, we already have it running for you.</span></span>

<span data-ttu-id="90548-144">Pour apprendre comment une API web authentifie en toute sécurité les demandes à l’aide d’Azure AD B2C, consultez [l’article sur la prise en main de l’API web](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="90548-144">To learn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="90548-145">Exécuter des stratégies</span><span class="sxs-lookup"><span data-stu-id="90548-145">Execute policies</span></span>
<span data-ttu-id="90548-146">Votre application communique avec Azure AD B2C en envoyant des messages d’authentification HTTP qui indiquent la stratégie à exécuter dans le cadre de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="90548-146">Your app communicates with Azure AD B2C by sending authentication messages that specify the policy they want to execute as part of the HTTP request.</span></span> <span data-ttu-id="90548-147">Pour les applications de bureau .NET, vous pouvez utiliser la version préliminaire de la bibliothèque d’authentification Microsoft (MSAL) pour envoyer des messages d’authentification OAuth 2.0, exécuter des stratégies et obtenir des jetons qui appellent des API web.</span><span class="sxs-lookup"><span data-stu-id="90548-147">For .NET desktop applications, you can use the preview Microsoft Authentication Library (MSAL) to send OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="90548-148">Installation de la bibliothèque MSAL</span><span class="sxs-lookup"><span data-stu-id="90548-148">Install MSAL</span></span>
<span data-ttu-id="90548-149">Ajoutez la bibliothèque MSAL au projet `TaskClient` à l’aide de la console du gestionnaire de package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="90548-149">Add MSAL to the `TaskClient` project by using the Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="90548-150">saisissez les informations B2C</span><span class="sxs-lookup"><span data-stu-id="90548-150">Enter your B2C details</span></span>
<span data-ttu-id="90548-151">Ouvrez le fichier `Globals.cs` , puis remplacez chacune des valeurs de propriété par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="90548-151">Open the file `Globals.cs` and replace each of the property values with your own.</span></span> <span data-ttu-id="90548-152">Cette classe est utilisée dans `TaskClient` pour référencer des valeurs couramment utilisées.</span><span class="sxs-lookup"><span data-stu-id="90548-152">This class is used throughout `TaskClient` to reference commonly used values.</span></span>

```C#
public static class Globals
{
    ...

    // TODO: Replace these five default with your own configuration values
    public static string tenant = "fabrikamb2c.onmicrosoft.com";
    public static string clientId = "90c0fe63-bcf2-44d5-8fb7-b8bbc0b29dc6";
    public static string signInPolicy = "b2c_1_sign_in";
    public static string signUpPolicy = "b2c_1_sign_up";
    public static string editProfilePolicy = "b2c_1_edit_profile";

    ...
}
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

### <a name="create-the-publicclientapplication"></a><span data-ttu-id="90548-153">Création de la PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="90548-153">Create the PublicClientApplication</span></span>
<span data-ttu-id="90548-154">La classe principale de la bibliothèque MSAL est `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="90548-154">The primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="90548-155">Cette classe représente votre application dans le système Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="90548-155">This class represents your application in the Azure AD B2C system.</span></span> <span data-ttu-id="90548-156">Quand l’application démarre, créez une instance `PublicClientApplication` dans `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="90548-156">When the app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="90548-157">Celle-ci peut être utilisée dans l’ensemble de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="90548-157">This can be used throughout the window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens to persist when the user closes the app,
        // we've extended the MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="90548-158">Lancement d’un flux d'inscription</span><span class="sxs-lookup"><span data-stu-id="90548-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="90548-159">Quand un utilisateur choisit de s’inscrire, vous devez lancer un flux d’inscription qui utilise la stratégie d’inscription que vous avez créée.</span><span class="sxs-lookup"><span data-stu-id="90548-159">When a user opts to signs up, you want to initiate a sign-up flow that uses the sign-up policy you created.</span></span> <span data-ttu-id="90548-160">À l’aide de la bibliothèque MSAL, il vous suffit d’appeler `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="90548-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="90548-161">Les paramètres que vous transmettez à `AcquireTokenAsync(...)` déterminent, entre autres, le jeton que vous recevez et la stratégie utilisée dans la demande d’authentification.</span><span class="sxs-lookup"><span data-stu-id="90548-161">The parameters you pass to `AcquireTokenAsync(...)` determine which token you receive, the policy used in the authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use the app's clientId here as the scope parameter, indicating that
        // you want a token to the your app's backend web API (represented by
        // the cloud hosted task API).  Use the UiOptions.ForceLogin flag to
        // indicate to MSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in the app that the user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When the request completes successfully, you can get user
        // information from the AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After the sign up successfully completes, display the user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of the policy.
    catch (MsalException ex)
    {
        if (ex.ErrorCode != "authentication_canceled")
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="90548-162">Lancement d’un flux de connexion</span><span class="sxs-lookup"><span data-stu-id="90548-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="90548-163">Vous pouvez lancer un flux de connexion de la même façon que vous lancez un flux d’inscription.</span><span class="sxs-lookup"><span data-stu-id="90548-163">You can initiate a sign-in flow in the same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="90548-164">Quand un utilisateur se connecte, effectuez le même appel à la bibliothèque MSAL, en utilisant cette fois votre stratégie de connexion :</span><span class="sxs-lookup"><span data-stu-id="90548-164">When a user signs in, make the same call to MSAL, this time by using your sign-in policy:</span></span>

```C#
private async void SignIn(object sender = null, RoutedEventArgs args = null)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.signInPolicy);
        ...
```

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="90548-165">Lancement d’un flux de modification de profil</span><span class="sxs-lookup"><span data-stu-id="90548-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="90548-166">Là encore, vous pouvez exécuter une stratégie de modification de profil de la même manière :</span><span class="sxs-lookup"><span data-stu-id="90548-166">Again, you can execute an edit-profile policy in the same fashion:</span></span>

```C#
private async void EditProfile(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                    string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                    Globals.editProfilePolicy);
```

<span data-ttu-id="90548-167">Dans tous ces cas, la bibliothèque MSAL retourne un jeton dans `AuthenticationResult` ou lève une exception.</span><span class="sxs-lookup"><span data-stu-id="90548-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="90548-168">Chaque fois que vous obtenez un jeton de la bibliothèque MSAL, vous pouvez utiliser l’objet `AuthenticationResult.User` pour mettre à jour les données utilisateur dans l’application, telles que l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90548-168">Each time you get a token from MSAL, you can use the `AuthenticationResult.User` object to update the user data in the app, such as the UI.</span></span> <span data-ttu-id="90548-169">La bibliothèque ADAL met également en cache le jeton, pour une utilisation dans d’autres parties de l’application.</span><span class="sxs-lookup"><span data-stu-id="90548-169">ADAL also caches the token for use in other parts of the application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="90548-170">Vérification des jetons sur le démarrage de l’application</span><span class="sxs-lookup"><span data-stu-id="90548-170">Check for tokens on app start</span></span>
<span data-ttu-id="90548-171">Vous pouvez également utiliser la bibliothèque MSAL pour effectuer le suivi de l’état de connexion de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90548-171">You can also use MSAL to keep track of the user's sign-in state.</span></span>  <span data-ttu-id="90548-172">Dans cette application, nous voulons que l’utilisateur reste connecté même après la fermeture et la réouverture de l’application.</span><span class="sxs-lookup"><span data-stu-id="90548-172">In this app, we want the user to remain signed in even after they close the app & re-open it.</span></span>  <span data-ttu-id="90548-173">Pour le remplacement de `OnInitialized`, utilisez la méthode `AcquireTokenSilent` de la bibliothèque MSAL pour rechercher les jetons mis en cache :</span><span class="sxs-lookup"><span data-stu-id="90548-173">Back inside the `OnInitialized` override, use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If the user has has a token cached with any policy, we'll display them as signed-in.
    TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
    string existingPolicy = tci == null ? null : tci.Policy;
    result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    SignInButton.Visibility = Visibility.Collapsed;
    SignUpButton.Visibility = Visibility.Collapsed;
    EditProfileButton.Visibility = Visibility.Visible;
    SignOutButton.Visibility = Visibility.Visible;
    UsernameLabel.Content = result.User.Name;
    GetTodoList();
}
catch (MsalException ex)
{
    if (ex.ErrorCode == "failed_to_acquire_token_silently")
    {
        // There are no tokens in the cache.  Proceed without calling the To Do list service.
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
```

## <a name="call-the-task-api"></a><span data-ttu-id="90548-174">Appel de l’API de tâche</span><span class="sxs-lookup"><span data-stu-id="90548-174">Call the task API</span></span>
<span data-ttu-id="90548-175">Vous avez maintenant utilisé la bibliothèque MSAL pour exécuter des stratégies et obtenir des jetons.</span><span class="sxs-lookup"><span data-stu-id="90548-175">You have now used MSAL to execute policies and get tokens.</span></span>  <span data-ttu-id="90548-176">Si vous souhaitez utiliser un de ces jetons pour appeler l’API de tâche, vous pouvez utiliser à nouveau la méthode `AcquireTokenSilent` de la bibliothèque MSAL pour rechercher les jetons mis en cache :</span><span class="sxs-lookup"><span data-stu-id="90548-176">When you want to use one these tokens to call the task API, you can again use MSAL's `AcquireTokenSilent` method to check for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want to check for a cached token, independent of whatever policy was used to acquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent to indicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch the exception and show the user a message.
    catch (MsalException ex)
    {
        // There is no access token in the cache, so prompt the user to sign-in.
        if (ex.ErrorCode == "failed_to_acquire_token_silently")
        {
            MessageBox.Show("Please sign up or sign in first");
            SignInButton.Visibility = Visibility.Visible;
            SignUpButton.Visibility = Visibility.Visible;
            EditProfileButton.Visibility = Visibility.Collapsed;
            SignOutButton.Visibility = Visibility.Collapsed;
            UsernameLabel.Content = string.Empty;
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
    ...
```

<span data-ttu-id="90548-177">Quand l’appel à `AcquireTokenSilentAsync(...)` réussit et qu’un jeton est trouvé dans le cache, vous pouvez ajouter le jeton à l’en-tête `Authorization` de la demande HTTP.</span><span class="sxs-lookup"><span data-stu-id="90548-177">When the call to `AcquireTokenSilentAsync(...)` succeeds and a token is found in the cache, you can add the token to the `Authorization` header of the HTTP request.</span></span> <span data-ttu-id="90548-178">L’API web de tâche utilisera cet en-tête pour authentifier la demande afin de lire la liste des tâches de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="90548-178">The task web API will use this header to authenticate the request to read the user's to-do list:</span></span>

```C#
    ...
    // Once the token has been returned by MSAL, add it to the http authorization header, before making the call to access the To Do list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call the To Do list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-the-user-out"></a><span data-ttu-id="90548-179">Déconnexion de l'utilisateur</span><span class="sxs-lookup"><span data-stu-id="90548-179">Sign the user out</span></span>
<span data-ttu-id="90548-180">Enfin, vous pouvez utiliser la bibliothèque MSAL pour mettre fin à la session d’un utilisateur dans l’application quand l’utilisateur sélectionne **Se déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="90548-180">Finally, you can use MSAL to end a user's session with the app when the user selects **Sign out**.</span></span>  <span data-ttu-id="90548-181">À l’aide de la bibliothèque MSAL, vous pouvez effectuer cette opération en effaçant tous les jetons du cache de jetons :</span><span class="sxs-lookup"><span data-stu-id="90548-181">When using MSAL, this is accomplished by clearing all of the tokens from the token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of the user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in the browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update the UI to show the user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-the-sample-app"></a><span data-ttu-id="90548-182">Exécution de l'exemple d'application</span><span class="sxs-lookup"><span data-stu-id="90548-182">Run the sample app</span></span>
<span data-ttu-id="90548-183">Enfin, créez et exécutez l’exemple.</span><span class="sxs-lookup"><span data-stu-id="90548-183">Finally, build and run the sample.</span></span>  <span data-ttu-id="90548-184">Inscrivez-vous à l’application à l’aide d’une adresse de messagerie ou d’un nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90548-184">Sign up for the app by using an email address or user name.</span></span> <span data-ttu-id="90548-185">Déconnectez-vous, puis reconnectez-vous en tant que même utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90548-185">Sign out and sign back in as the same user.</span></span> <span data-ttu-id="90548-186">Modifiez le profil de cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="90548-186">Edit that user's profile.</span></span> <span data-ttu-id="90548-187">Déconnectez-vous et connectez-vous en utilisant un utilisateur différent.</span><span class="sxs-lookup"><span data-stu-id="90548-187">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="90548-188">Ajout d’IDP sociaux</span><span class="sxs-lookup"><span data-stu-id="90548-188">Add social IDPs</span></span>
<span data-ttu-id="90548-189">Actuellement, l’application prend uniquement en charge l’inscription et la connexion d’utilisateurs qui utilisent des **comptes locaux**.</span><span class="sxs-lookup"><span data-stu-id="90548-189">Currently, the app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="90548-190">Il s’agit de comptes stockés dans votre répertoire B2C qui utilisent un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="90548-190">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="90548-191">Avec Azure AD B2C, vous pouvez ajouter la prise en charge d’autres fournisseurs d’identité sans modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="90548-191">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="90548-192">Pour ajouter des fournisseurs d’identité sociaux à votre application, commencez par suivre les instructions détaillées figurant dans ces articles.</span><span class="sxs-lookup"><span data-stu-id="90548-192">To add social IDPs to your app, begin by following the detailed instructions in these articles.</span></span> <span data-ttu-id="90548-193">Pour chaque fournisseur d’identité que vous souhaitez prendre en charge, vous devez inscrire une application dans ce système et obtenir un ID client.</span><span class="sxs-lookup"><span data-stu-id="90548-193">For each IDP you want to support, you need to register an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="90548-194">Définir Facebook en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="90548-194">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="90548-195">Définir Google en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="90548-195">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="90548-196">Définir Amazon en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="90548-196">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="90548-197">Définir LinkedIn en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="90548-197">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="90548-198">Après avoir ajouté les fournisseurs d’identité à votre répertoire B2C, vous devez modifier chacune de vos trois stratégies pour inclure ces nouveaux fournisseurs, comme décrit dans [l’article de référence sur les stratégies](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="90548-198">After you add the identity providers to your B2C directory, you need to edit each of your three policies to include the new IDPs, as described in the [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="90548-199">Après avoir enregistré vos stratégies, exécutez à nouveau l’application.</span><span class="sxs-lookup"><span data-stu-id="90548-199">After you save your policies, run the app again.</span></span> <span data-ttu-id="90548-200">Les nouveaux fournisseurs d’identité doivent être ajoutés comme options d’inscription et de connexion dans chacune de vos expériences relatives à l’identité.</span><span class="sxs-lookup"><span data-stu-id="90548-200">You should see the new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="90548-201">Vous pouvez tester vos stratégies et observer les résultats sur votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="90548-201">You can experiment with your policies and observe the effects on your sample app.</span></span> <span data-ttu-id="90548-202">Ajoutez ou supprimez des fournisseurs d’identité, manipulez des revendications d’application ou modifiez des attributs d’inscription.</span><span class="sxs-lookup"><span data-stu-id="90548-202">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="90548-203">Faites des essais jusqu’à ce que vous compreniez la façon dont les stratégies, les demandes d’authentification et la bibliothèque MSAL sont liées.</span><span class="sxs-lookup"><span data-stu-id="90548-203">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="90548-204">Pour référence, l’exemple terminé [est fourni en tant que fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="90548-204">For reference, the completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="90548-205">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="90548-205">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
