---
title: aaaAzure Active Directory B2C | Documents Microsoft
description: "Comment toobuild une application de bureau Windows qui inclut la connexion, d’inscription et gestion de profil à l’aide d’Azure Active Directory B2C."
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
ms.openlocfilehash: f22b0299ff74bfba2f3fea88f006da609859dda5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-build-a-windows-desktop-app"></a><span data-ttu-id="fd7ac-103">Azure AD B2C : création d’une application de bureau Windows</span><span class="sxs-lookup"><span data-stu-id="fd7ac-103">Azure AD B2C: Build a Windows desktop app</span></span>
<span data-ttu-id="fd7ac-104">À l’aide de B2C d’Azure Active Directory (Azure AD), vous pouvez ajouter des identités en libre-service puissantes fonctionnalités tooyour bureau application de gestion dans quelques étapes.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-104">By using Azure Active Directory (Azure AD) B2C, you can add powerful self-service identity management features tooyour desktop app in a few short steps.</span></span> <span data-ttu-id="fd7ac-105">Cet article vous indiquent comment toocreate une application .NET Windows Presentation Foundation (WPF) « liste de tâches » qui inclut l’utilisateur d’abonnement, connectez-vous et la gestion de profil.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-105">This article will show you how toocreate a .NET Windows Presentation Foundation (WPF) "to-do list" app that includes user sign-up, sign-in, and profile management.</span></span> <span data-ttu-id="fd7ac-106">application Hello inclut la prise en charge pour l’inscription et connectez-vous à l’aide d’un nom d’utilisateur ou un e-mail.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-106">hello app will include support for sign-up and sign-in by using a user name or email.</span></span> <span data-ttu-id="fd7ac-107">Elle prendra également en charge l’inscription et la connexion à l’aide d’un compte de réseau social comme Facebook et Google.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-107">It will also include support for sign-up and sign-in by using social accounts such as Facebook and Google.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="fd7ac-108">Obtention d'un répertoire Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="fd7ac-108">Get an Azure AD B2C directory</span></span>
<span data-ttu-id="fd7ac-109">Avant de pouvoir utiliser Azure AD B2C, vous devez créer un répertoire ou un client.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-109">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="fd7ac-110">Un répertoire est un conteneur destiné à recevoir tous vos utilisateurs, applications, groupes, etc.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-110">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="fd7ac-111">Si vous n’en possédez pas déjà un, [créez un répertoire B2C](active-directory-b2c-get-started.md) avant d’aller plus loin dans ce guide.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-111">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="fd7ac-112">Création d'une application</span><span class="sxs-lookup"><span data-stu-id="fd7ac-112">Create an application</span></span>
<span data-ttu-id="fd7ac-113">Ensuite, vous devez toocreate une application dans votre répertoire B2C.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-113">Next, you need toocreate an app in your B2C directory.</span></span> <span data-ttu-id="fd7ac-114">Cela fournit des informations AD Azure qu’il a besoin toosecurely communiquer avec votre application.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-114">This gives Azure AD information that it needs toosecurely communicate with your app.</span></span> <span data-ttu-id="fd7ac-115">toocreate une application, procédez comme [ces instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-115">toocreate an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span>  <span data-ttu-id="fd7ac-116">Veillez à effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-116">Be sure to:</span></span>

* <span data-ttu-id="fd7ac-117">Inclure un **native client** dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-117">Include a **native client** in hello application.</span></span>
* <span data-ttu-id="fd7ac-118">Hello de copie **URI de redirection** `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-118">Copy hello **Redirect URI** `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="fd7ac-119">Il s’agit d’URL par défaut de hello pour cet exemple de code.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-119">It is hello default URL for this code sample.</span></span>
* <span data-ttu-id="fd7ac-120">Hello de copie **ID d’Application** qui est attribué tooyour application.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-120">Copy hello **Application ID** that is assigned tooyour app.</span></span> <span data-ttu-id="fd7ac-121">Vous en aurez besoin ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-121">You will need it later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="fd7ac-122">Création de vos stratégies</span><span class="sxs-lookup"><span data-stu-id="fd7ac-122">Create your policies</span></span>
<span data-ttu-id="fd7ac-123">Dans Azure AD B2C, chaque expérience utilisateur est définie par une [stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-123">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="fd7ac-124">Cet exemple de code contient trois expériences liées à l’identité : l’inscription, la connexion et la modification du profil.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-124">This code sample contains three identity experiences: sign up, sign in, and edit profile.</span></span> <span data-ttu-id="fd7ac-125">Vous devez toocreate une stratégie pour chaque type, comme décrit dans la [article de référence de stratégie](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-125">You need toocreate a policy for each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="fd7ac-126">Lorsque vous créez trois stratégies de hello, veillez à :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-126">When you create hello three policies, be sure to:</span></span>

* <span data-ttu-id="fd7ac-127">Choisissez **ID d’utilisateur d’abonnement** ou **par courrier électronique d’abonnement** dans le panneau de fournisseurs d’identité hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-127">Choose either **User ID sign-up** or **Email sign-up** in hello identity providers blade.</span></span>
* <span data-ttu-id="fd7ac-128">Choisir **Nom d’affichage** et d’autres attributs d’inscription dans votre stratégie d’inscription.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-128">Choose **Display name** and other sign-up attributes in your sign-up policy.</span></span>
* <span data-ttu-id="fd7ac-129">Choisir les revendications **Nom d’affichage** et **ID d’objet** comme revendications d’application pour chaque stratégie.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-129">Choose **Display name** and **Object ID** claims as application claims for every policy.</span></span> <span data-ttu-id="fd7ac-130">Vous pouvez aussi choisir d'autres revendications.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-130">You can choose other claims as well.</span></span>
* <span data-ttu-id="fd7ac-131">Hello de copie **nom** de chaque stratégie après l’avoir créée.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-131">Copy hello **Name** of each policy after you create it.</span></span> <span data-ttu-id="fd7ac-132">Il doit avoir le préfixe de hello `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-132">It should have hello prefix `b2c_1_`.</span></span>  <span data-ttu-id="fd7ac-133">Vous aurez besoin des noms de ces stratégies ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-133">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="fd7ac-134">Une fois que vous avez créé hello trois stratégies, vous êtes prêt toobuild votre application.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-134">After you have successfully created hello three policies, you're ready toobuild your app.</span></span>

## <a name="download-hello-code"></a><span data-ttu-id="fd7ac-135">Télécharger le code de hello</span><span class="sxs-lookup"><span data-stu-id="fd7ac-135">Download hello code</span></span>
<span data-ttu-id="fd7ac-136">Hello du code pour ce didacticiel [est conservée sur GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-136">hello code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet).</span></span> <span data-ttu-id="fd7ac-137">exemple de hello toobuild en tant que vous accédez, vous pouvez [télécharger un projet sous forme de fichier .zip de squelette](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-137">toobuild hello sample as you go, you can [download a skeleton project as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/skeleton.zip).</span></span> <span data-ttu-id="fd7ac-138">Vous pouvez également dupliquer le squelette de hello :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-138">You can also clone hello skeleton:</span></span>

```
git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git
```

<span data-ttu-id="fd7ac-139">application Hello terminée est également [disponible sous forme de fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) ou sur hello `complete` branche Hello même référentiel.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-139">hello completed app is also [available as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip) or on hello `complete` branch of hello same repository.</span></span>

<span data-ttu-id="fd7ac-140">Après avoir téléchargé l’exemple de code hello, ouvrez hello tooget du fichier .sln de Visual Studio a démarré.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-140">After you download hello sample code, open hello Visual Studio .sln file tooget started.</span></span> <span data-ttu-id="fd7ac-141">Hello `TaskClient` projet est hello application de bureau WPF hello utilisateur interagit avec.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-141">hello `TaskClient` project is hello WPF desktop application that hello user interacts with.</span></span> <span data-ttu-id="fd7ac-142">Pour des raisons de hello de ce didacticiel, il appelle une tâche de back-end API web, hébergé dans Azure, qui stocke la liste des actions de chaque utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-142">For hello purposes of this tutorial, it calls a back-end task web API, hosted in Azure, that stores each user's to-do list.</span></span>  <span data-ttu-id="fd7ac-143">Vous n’avez pas besoin de toobuild hello web API, nous avons déjà qu’il est en cours d’exécution pour vous.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-143">You do not need toobuild hello web API, we already have it running for you.</span></span>

<span data-ttu-id="fd7ac-144">toolearn comment une API web authentifie en toute sécurité les requêtes à l’aide d’Azure AD B2C, consultez le [API web mise en route article](active-directory-b2c-devquickstarts-api-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-144">toolearn how a web API securely authenticates requests by using Azure AD B2C, check out the [web API getting started article](active-directory-b2c-devquickstarts-api-dotnet.md).</span></span>

## <a name="execute-policies"></a><span data-ttu-id="fd7ac-145">Exécuter des stratégies</span><span class="sxs-lookup"><span data-stu-id="fd7ac-145">Execute policies</span></span>
<span data-ttu-id="fd7ac-146">Votre application communique avec Azure AD B2C en envoyant des messages d’authentification qui spécifient la stratégie hello qu’ils souhaitent tooexecute dans le cadre de la demande de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-146">Your app communicates with Azure AD B2C by sending authentication messages that specify hello policy they want tooexecute as part of hello HTTP request.</span></span> <span data-ttu-id="fd7ac-147">Pour les applications de bureau .NET, vous pouvez utiliser hello afficher un aperçu des messages d’authentification de bibliothèque d’authentification Microsoft (MSAL) toosend OAuth 2.0, exécution des stratégies et obtenir des jetons qui appellent des API web.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-147">For .NET desktop applications, you can use hello preview Microsoft Authentication Library (MSAL) toosend OAuth 2.0 authentication messages, execute policies, and get tokens that call web APIs.</span></span>

### <a name="install-msal"></a><span data-ttu-id="fd7ac-148">Installation de la bibliothèque MSAL</span><span class="sxs-lookup"><span data-stu-id="fd7ac-148">Install MSAL</span></span>
<span data-ttu-id="fd7ac-149">Ajouter MSAL toohello `TaskClient` projet à l’aide de hello Console du Gestionnaire de Package Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-149">Add MSAL toohello `TaskClient` project by using hello Visual Studio Package Manager Console.</span></span>

```
PM> Install-Package Microsoft.Identity.Client -IncludePrerelease
```

### <a name="enter-your-b2c-details"></a><span data-ttu-id="fd7ac-150">saisissez les informations B2C</span><span class="sxs-lookup"><span data-stu-id="fd7ac-150">Enter your B2C details</span></span>
<span data-ttu-id="fd7ac-151">Les fichiers ouverts hello `Globals.cs` et chacune des valeurs de propriété hello remplacer par les vôtres.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-151">Open hello file `Globals.cs` and replace each of hello property values with your own.</span></span> <span data-ttu-id="fd7ac-152">Cette classe est utilisée tout au long de `TaskClient` les valeurs tooreference couramment utilisée.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-152">This class is used throughout `TaskClient` tooreference commonly used values.</span></span>

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

### <a name="create-hello-publicclientapplication"></a><span data-ttu-id="fd7ac-153">Créer hello PublicClientApplication</span><span class="sxs-lookup"><span data-stu-id="fd7ac-153">Create hello PublicClientApplication</span></span>
<span data-ttu-id="fd7ac-154">Hello la classe principale de MSAL est `PublicClientApplication`.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-154">hello primary class of MSAL is `PublicClientApplication`.</span></span> <span data-ttu-id="fd7ac-155">Cette classe représente votre application dans le système de hello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-155">This class represents your application in hello Azure AD B2C system.</span></span> <span data-ttu-id="fd7ac-156">Lorsque hello initialise de l’application, créez une instance de `PublicClientApplication` dans `MainWindow.xaml.cs`.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-156">When hello app initalizes, create an instance of `PublicClientApplication` in `MainWindow.xaml.cs`.</span></span> <span data-ttu-id="fd7ac-157">Cela peut être utilisé dans la fenêtre hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-157">This can be used throughout hello window.</span></span>

```C#
protected async override void OnInitialized(EventArgs e)
{
    base.OnInitialized(e);

    pca = new PublicClientApplication(Globals.clientId)
    {
        // MSAL implements an in-memory cache by default.  Since we want tokens toopersist when hello user closes hello app,
        // we've extended hello MSAL TokenCache and created a simple FileCache in this app.
        UserTokenCache = new FileCache(),
    };

    ...
```

### <a name="initiate-a-sign-up-flow"></a><span data-ttu-id="fd7ac-158">Lancement d’un flux d'inscription</span><span class="sxs-lookup"><span data-stu-id="fd7ac-158">Initiate a sign-up flow</span></span>
<span data-ttu-id="fd7ac-159">Lorsqu’un utilisateur choisit toosigns haut, vous souhaitez tooinitiate un flux d’abonnement qui utilise la stratégie d’inscription de hello que vous avez créé.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-159">When a user opts toosigns up, you want tooinitiate a sign-up flow that uses hello sign-up policy you created.</span></span> <span data-ttu-id="fd7ac-160">À l’aide de la bibliothèque MSAL, il vous suffit d’appeler `pca.AcquireTokenAsync(...)`.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-160">By using MSAL, you just call `pca.AcquireTokenAsync(...)`.</span></span> <span data-ttu-id="fd7ac-161">Hello les paramètres que vous transmettez trop`AcquireTokenAsync(...)` déterminer quel jeton vous recevez, stratégie de hello utilisée dans la demande d’authentification hello et bien plus encore.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-161">hello parameters you pass too`AcquireTokenAsync(...)` determine which token you receive, hello policy used in hello authentication request, and more.</span></span>

```C#
private async void SignUp(object sender, RoutedEventArgs e)
{
    AuthenticationResult result = null;
    try
    {
        // Use hello app's clientId here as hello scope parameter, indicating that
        // you want a token toohello your app's backend web API (represented by
        // hello cloud hosted task API).  Use hello UiOptions.ForceLogin flag to
        // indicate tooMSAL that it should show a sign-up UI no matter what.
        result = await pca.AcquireTokenAsync(new string[] { Globals.clientId },
                string.Empty, UiOptions.ForceLogin, null, null, Globals.authority,
                Globals.signUpPolicy);

        // Upon success, indicate in hello app that hello user is signed in.
        SignInButton.Visibility = Visibility.Collapsed;
        SignUpButton.Visibility = Visibility.Collapsed;
        EditProfileButton.Visibility = Visibility.Visible;
        SignOutButton.Visibility = Visibility.Visible;

        // When hello request completes successfully, you can get user
        // information from hello AuthenticationResult
        UsernameLabel.Content = result.User.Name;

        // After hello sign up successfully completes, display hello user's To-Do List
        GetTodoList();
    }

    // Handle any exeptions that occurred during execution of hello policy.
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

### <a name="initiate-a-sign-in-flow"></a><span data-ttu-id="fd7ac-162">Lancement d’un flux de connexion</span><span class="sxs-lookup"><span data-stu-id="fd7ac-162">Initiate a sign-in flow</span></span>
<span data-ttu-id="fd7ac-163">Vous pouvez lancer un flux de connexion Bonjour même façon que vous lancez un flux d’inscription.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-163">You can initiate a sign-in flow in hello same way that you initiate a sign-up flow.</span></span> <span data-ttu-id="fd7ac-164">Lorsqu’un utilisateur se connecte, rendre hello même appeler tooMSAL, cette fois à l’aide de votre stratégie d’authentification :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-164">When a user signs in, make hello same call tooMSAL, this time by using your sign-in policy:</span></span>

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

### <a name="initiate-an-edit-profile-flow"></a><span data-ttu-id="fd7ac-165">Lancement d’un flux de modification de profil</span><span class="sxs-lookup"><span data-stu-id="fd7ac-165">Initiate an edit-profile flow</span></span>
<span data-ttu-id="fd7ac-166">Là encore, vous pouvez exécuter une stratégie de modifier le profil Bonjour même manière :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-166">Again, you can execute an edit-profile policy in hello same fashion:</span></span>

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

<span data-ttu-id="fd7ac-167">Dans tous ces cas, la bibliothèque MSAL retourne un jeton dans `AuthenticationResult` ou lève une exception.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-167">In all of these cases, MSAL either returns a token in `AuthenticationResult` or throws an exception.</span></span> <span data-ttu-id="fd7ac-168">Chaque fois que vous obtenez un jeton à partir de MSAL, vous pouvez utiliser hello `AuthenticationResult.User` tooupdate hello données utilisateur contenues dans application hello, par exemple hello l’interface utilisateur de l’objet.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-168">Each time you get a token from MSAL, you can use hello `AuthenticationResult.User` object tooupdate hello user data in hello app, such as hello UI.</span></span> <span data-ttu-id="fd7ac-169">La bibliothèque ADAL également les caches hello jeton pour l’utiliser dans d’autres parties de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-169">ADAL also caches hello token for use in other parts of hello application.</span></span>

### <a name="check-for-tokens-on-app-start"></a><span data-ttu-id="fd7ac-170">Vérification des jetons sur le démarrage de l’application</span><span class="sxs-lookup"><span data-stu-id="fd7ac-170">Check for tokens on app start</span></span>
<span data-ttu-id="fd7ac-171">Vous pouvez également utiliser le suivi de tookeep MSAL de l’état de connexion de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-171">You can also use MSAL tookeep track of hello user's sign-in state.</span></span>  <span data-ttu-id="fd7ac-172">Dans cette application, nous souhaitons hello utilisateur tooremain est signé le même après leur fermer l’application hello et ouvrez à nouveau.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-172">In this app, we want hello user tooremain signed in even after they close hello app & re-open it.</span></span>  <span data-ttu-id="fd7ac-173">Retour à l’intérieur de hello `OnInitialized` remplacer, utilisez de MSAL `AcquireTokenSilent` toocheck de méthode pour les jetons mis en cache :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-173">Back inside hello `OnInitialized` override, use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
AuthenticationResult result = null;
try
{
    // If hello user has has a token cached with any policy, we'll display them as signed-in.
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
        // There are no tokens in hello cache.  Proceed without calling hello tooDo list service.
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

## <a name="call-hello-task-api"></a><span data-ttu-id="fd7ac-174">Appeler des API de tâche hello</span><span class="sxs-lookup"><span data-stu-id="fd7ac-174">Call hello task API</span></span>
<span data-ttu-id="fd7ac-175">Vous avez utilisé stratégies de tooexecute MSAL et obtenez des jetons.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-175">You have now used MSAL tooexecute policies and get tokens.</span></span>  <span data-ttu-id="fd7ac-176">Lorsque vous souhaitez toouse une ces API de tâche de jetons toocall hello, vous pouvez réutiliser du MSAL `AcquireTokenSilent` toocheck de méthode pour les jetons mis en cache :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-176">When you want toouse one these tokens toocall hello task API, you can again use MSAL's `AcquireTokenSilent` method toocheck for cached tokens:</span></span>

```C#
private async void GetTodoList()
{
    AuthenticationResult result = null;
    try
    {
        // Here we want toocheck for a cached token, independent of whatever policy was used tooacquire it.
        TokenCacheItem tci = pca.UserTokenCache.ReadItems(Globals.clientId).Where(i => i.Scope.Contains(Globals.clientId) && !string.IsNullOrEmpty(i.Policy)).FirstOrDefault();
        string existingPolicy = tci == null ? null : tci.Policy;

        // Use AcquireTokenSilent tooindicate that MSAL should throw an exception if a token cannot be acquired
        result = await pca.AcquireTokenSilentAsync(new string[] { Globals.clientId }, string.Empty, Globals.authority, existingPolicy, false);

    }
    // If a token could not be acquired silently, we'll catch hello exception and show hello user a message.
    catch (MsalException ex)
    {
        // There is no access token in hello cache, so prompt hello user toosign-in.
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

<span data-ttu-id="fd7ac-177">Lorsque de trop hello appel`AcquireTokenSilentAsync(...)` réussit et un jeton est trouvé dans le cache de hello, vous pouvez ajouter toohello de jeton hello `Authorization` en-tête de demande de hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-177">When hello call too`AcquireTokenSilentAsync(...)` succeeds and a token is found in hello cache, you can add hello token toohello `Authorization` header of hello HTTP request.</span></span> <span data-ttu-id="fd7ac-178">API web de tâche Hello utilisera la liste de tâches en-tête tooauthenticate hello demande tooread hello de cet utilisateur :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-178">hello task web API will use this header tooauthenticate hello request tooread hello user's to-do list:</span></span>

```C#
    ...
    // Once hello token has been returned by MSAL, add it toohello http authorization header, before making hello call tooaccess hello tooDo list service.
    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.Token);

    // Call hello tooDo list service.
    HttpResponseMessage response = await httpClient.GetAsync(Globals.taskServiceUrl + "/api/tasks");
    ...
```

## <a name="sign-hello-user-out"></a><span data-ttu-id="fd7ac-179">Utilisateur de hello signe out</span><span class="sxs-lookup"><span data-stu-id="fd7ac-179">Sign hello user out</span></span>
<span data-ttu-id="fd7ac-180">Enfin, vous pouvez utiliser MSAL tooend une session de l’utilisateur avec l’application hello lorsque hello utilisateur sélectionne **se déconnecter**.  Lorsque vous utilisez MSAL, cela s’effectue en effaçant tous les jetons hello à partir du cache de jetons hello de :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-180">Finally, you can use MSAL tooend a user's session with hello app when hello user selects **Sign out**.  When using MSAL, this is accomplished by clearing all of hello tokens from hello token cache:</span></span>

```C#
private void SignOut(object sender, RoutedEventArgs e)
{
    // Clear any remnants of hello user's session.
    pca.UserTokenCache.Clear(Globals.clientId);

    // This is a helper method that clears browser cookies in hello browser control that MSAL uses, it is not part of MSAL.
    ClearCookies();

    // Update hello UI tooshow hello user as signed out.
    TaskList.ItemsSource = string.Empty;
    SignInButton.Visibility = Visibility.Visible;
    SignUpButton.Visibility = Visibility.Visible;
    EditProfileButton.Visibility = Visibility.Collapsed;
    SignOutButton.Visibility = Visibility.Collapsed;
    return;
}
```

## <a name="run-hello-sample-app"></a><span data-ttu-id="fd7ac-181">Exécutez l’exemple d’application hello</span><span class="sxs-lookup"><span data-stu-id="fd7ac-181">Run hello sample app</span></span>
<span data-ttu-id="fd7ac-182">Enfin, générez et exécutez l’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-182">Finally, build and run hello sample.</span></span>  <span data-ttu-id="fd7ac-183">Inscrivez-vous pour une application hello à l’aide d’un nom d’utilisateur ou une adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-183">Sign up for hello app by using an email address or user name.</span></span> <span data-ttu-id="fd7ac-184">Se déconnecter et reconnecter en tant que hello même utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-184">Sign out and sign back in as hello same user.</span></span> <span data-ttu-id="fd7ac-185">Modifiez le profil de cet utilisateur.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-185">Edit that user's profile.</span></span> <span data-ttu-id="fd7ac-186">Déconnectez-vous et connectez-vous en utilisant un utilisateur différent.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-186">Sign out and sign up by using a different user.</span></span>

## <a name="add-social-idps"></a><span data-ttu-id="fd7ac-187">Ajout d’IDP sociaux</span><span class="sxs-lookup"><span data-stu-id="fd7ac-187">Add social IDPs</span></span>
<span data-ttu-id="fd7ac-188">Actuellement, application hello prend en charge uniquement inscription de l’utilisateur et de connexion qui utilisent **comptes locaux**.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-188">Currently, hello app supports only user sign-up and sign-in that use **local accounts**.</span></span> <span data-ttu-id="fd7ac-189">Il s’agit de comptes stockés dans votre répertoire B2C qui utilisent un nom d’utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-189">These are accounts stored in your B2C directory that use a user name and password.</span></span> <span data-ttu-id="fd7ac-190">Avec Azure AD B2C, vous pouvez ajouter la prise en charge d’autres fournisseurs d’identité sans modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-190">By using Azure AD B2C, you can add support for other identity providers (IDPs) without changing any of your code.</span></span>

<span data-ttu-id="fd7ac-191">tooadd sociaux IDPs tooyour application, commencez par suivre hello des instructions dans ces articles.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-191">tooadd social IDPs tooyour app, begin by following hello detailed instructions in these articles.</span></span> <span data-ttu-id="fd7ac-192">Pour chaque IDP vous toosupport, vous devez tooregister une application de ce système et obtenez un ID client.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-192">For each IDP you want toosupport, you need tooregister an application in that system and obtain a client ID.</span></span>

* [<span data-ttu-id="fd7ac-193">Définir Facebook en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="fd7ac-193">Set up Facebook as an IDP</span></span>](active-directory-b2c-setup-fb-app.md)
* [<span data-ttu-id="fd7ac-194">Définir Google en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="fd7ac-194">Set up Google as an IDP</span></span>](active-directory-b2c-setup-goog-app.md)
* [<span data-ttu-id="fd7ac-195">Définir Amazon en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="fd7ac-195">Set up Amazon as an IDP</span></span>](active-directory-b2c-setup-amzn-app.md)
* [<span data-ttu-id="fd7ac-196">Définir LinkedIn en tant qu’IDP</span><span class="sxs-lookup"><span data-stu-id="fd7ac-196">Set up LinkedIn as an IDP</span></span>](active-directory-b2c-setup-li-app.md)

<span data-ttu-id="fd7ac-197">Après avoir ajouté le répertoire de tooyour B2C hello identité fournisseurs, vous devez tooedit chacun de vos trois stratégies tooinclude hello IDPs nouveau, comme décrit dans hello [article de référence de stratégie](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-197">After you add hello identity providers tooyour B2C directory, you need tooedit each of your three policies tooinclude hello new IDPs, as described in hello [policy reference article](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="fd7ac-198">Après avoir enregistré vos stratégies, exécutez à nouveau application hello.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-198">After you save your policies, run hello app again.</span></span> <span data-ttu-id="fd7ac-199">Vous devez voir hello Qu'idps nouveau ajoutés en tant qu’options de connexion et d’inscription dans chacun de vos expériences d’identité.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-199">You should see hello new IDPs added as sign-in and sign-up options in each of your identity experiences.</span></span>

<span data-ttu-id="fd7ac-200">Vous pouvez faire des essais avec vos stratégies et observer les effets de hello sur votre exemple d’application.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-200">You can experiment with your policies and observe hello effects on your sample app.</span></span> <span data-ttu-id="fd7ac-201">Ajoutez ou supprimez des fournisseurs d’identité, manipulez des revendications d’application ou modifiez des attributs d’inscription.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-201">Add or remove IDPs, manipulate application claims, or change sign-up attributes.</span></span> <span data-ttu-id="fd7ac-202">Faites des essais jusqu’à ce que vous compreniez la façon dont les stratégies, les demandes d’authentification et la bibliothèque MSAL sont liées.</span><span class="sxs-lookup"><span data-stu-id="fd7ac-202">Experiment until you can see how policies, authentication requests, and MSAL tie together.</span></span>

<span data-ttu-id="fd7ac-203">Pour référence, hello effectuée exemple [est fournie comme un fichier .zip](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="fd7ac-203">For reference, hello completed sample [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet/archive/complete.zip).</span></span> <span data-ttu-id="fd7ac-204">Vous pouvez également le cloner à partir de GitHub :</span><span class="sxs-lookup"><span data-stu-id="fd7ac-204">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-NativeClient-DotNet.git```
