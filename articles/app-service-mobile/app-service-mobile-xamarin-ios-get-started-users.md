---
title: Prise en main de l'authentification pour Mobile Apps dans Xamarin iOS
description: "Découvrez comment utiliser Mobile Apps pour authentifier les utilisateurs de votre application Xamarin iOS via divers fournisseurs d'identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 180cc61b-19c5-48bf-a16c-7181aef3eacc
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: glenga
ms.openlocfilehash: 454b2df5a9bf8cfba93befea54370957ab044d95
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="add-authentication-to-your-xamarinios-app"></a><span data-ttu-id="9fbe6-103">Ajout de l'authentification à votre application Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="9fbe6-103">Add authentication to your Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="9fbe6-104">Cette rubrique montre comment authentifier les utilisateurs d'une application App Service Mobile App à partir de votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-104">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="9fbe6-105">Dans ce didacticiel, vous allez ajouter l’authentification au projet de démarrage rapide Xamarin.iOS à l’aide d’un fournisseur d’identité pris en charge par App Service.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-105">In this tutorial, you add authentication to the Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="9fbe6-106">Une fois l’utilisateur authentifié et autorisé par votre application Mobile App, la valeur de l’ID utilisateur s’affiche ; vous pouvez alors accéder aux données de table limitées.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-106">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed and you will be able to access restricted table data.</span></span>

<span data-ttu-id="9fbe6-107">Vous devez commencer par suivre le didacticiel [Création d’une application Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="9fbe6-107">You must first complete the tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="9fbe6-108">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devez ajouter le package d’extension d’authentification à votre projet.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-108">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="9fbe6-109">Pour plus d'informations sur les packages d'extension de serveur, consultez [Utiliser le kit SDK du serveur backend .NET pour Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="9fbe6-109">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="9fbe6-110">Inscription de votre application pour l'authentification et configuration d'App Services</span><span class="sxs-lookup"><span data-stu-id="9fbe6-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-to-the-allowed-external-redirect-urls"></a><span data-ttu-id="9fbe6-111">Ajouter votre application aux URL de redirection externes autorisées</span><span class="sxs-lookup"><span data-stu-id="9fbe6-111">Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="9fbe6-112">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="9fbe6-113">Cela permet au système d’authentification de vous rediriger vers votre application une fois le processus d’authentification terminé.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-113">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="9fbe6-114">Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-114">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="9fbe6-115">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="9fbe6-116">Il doit être propre à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-116">It should be unique to your mobile application.</span></span> <span data-ttu-id="9fbe6-117">Pour activer la redirection côté serveur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9fbe6-117">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="9fbe6-118">Dans le [portail Azure], sélectionnez votre instance App Service.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-118">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="9fbe6-119">Cliquez sur l’option de menu **Authentication/Authorisation**.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-119">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="9fbe6-120">Dans **URL de redirection externes autorisées**, saisissez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-120">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="9fbe6-121">La chaîne **url_scheme_of_your_app** de cette chaîne est le schéma d’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-121">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="9fbe6-122">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="9fbe6-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="9fbe6-123">Vous devez noter la chaîne que vous choisissez, dans la mesure où vous devez ajuster votre code d’application mobile avec le schéma d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-123">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="9fbe6-124">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-124">Click **OK**.</span></span>

5. <span data-ttu-id="9fbe6-125">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-125">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="9fbe6-126">Restriction des autorisations pour les utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="9fbe6-126">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="9fbe6-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="9fbe6-128">Dans Visual Studio ou Xamarin Studio, exécutez le projet client sur un appareil ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-128">In Visual Studio or Xamarin Studio, run the client project on a device or emulator.</span></span> <span data-ttu-id="9fbe6-129">Vérifiez qu'une exception non gérée avec un code d'état 401 (Non autorisé) est générée après le démarrage de l'application.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="9fbe6-130">L’échec est consigné dans la console du débogueur.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-130">The failure is logged to the console of the debugger.</span></span> <span data-ttu-id="9fbe6-131">Ainsi, dans Visual Studio, vous devez voir l’échec dans la fenêtre de sortie.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-131">So in Visual Studio, you should see the failure in the output window.</span></span>

<span data-ttu-id="9fbe6-132">&nbsp;&nbsp;Cet échec non autorisé se produit, car l’application tente d’accéder à votre backend Mobile App en tant qu’utilisateur non authentifié.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-132">&nbsp;&nbsp;This unauthorized failure happens because the app attempts to access your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="9fbe6-133">La table *TodoItem* nécessite désormais l’authentification.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-133">The *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="9fbe6-134">Ensuite, vous mettrez à jour l’application cliente pour demander des ressources au backend Mobile App avec un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-134">Next, you will update the client app to request resources from the Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-to-the-app"></a><span data-ttu-id="9fbe6-135">Ajout de l'authentification à l'application</span><span class="sxs-lookup"><span data-stu-id="9fbe6-135">Add authentication to the app</span></span>
<span data-ttu-id="9fbe6-136">Dans cette section, vous allez modifier l'application de façon à afficher un écran de connexion avant d'afficher des données.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-136">In this section, you will modify the app to display a login screen before displaying data.</span></span> <span data-ttu-id="9fbe6-137">Quand l'application démarre, elle ne se connecte pas à votre service App Service et n'affiche pas de données.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-137">When the app starts, it will not not connect to your App Service and will not display any data.</span></span> <span data-ttu-id="9fbe6-138">Après le premier geste d'actualisation de l'utilisateur, l'écran de connexion s'affiche. Une fois la connexion réussie, la liste des tâches s'affiche.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-138">After the first time that the user performs the refresh gesture, the login screen will appear; after successful login the list of todo items will be displayed.</span></span>

1. <span data-ttu-id="9fbe6-139">Dans le projet client, ouvrez le fichier **QSTodoService.cs** et ajoutez l’instruction suivante et `MobileServiceUser` avec l’accesseur à la classe QSTodoService :</span><span class="sxs-lookup"><span data-stu-id="9fbe6-139">In the client project, open the file **QSTodoService.cs** and add the following using statement and `MobileServiceUser` with accessor to the QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="9fbe6-140">Ajoutez une nouvelle méthode nommée **Authenticate** à **QSTodoService** avec la définition suivante :</span><span class="sxs-lookup"><span data-stu-id="9fbe6-140">Add new method named **Authenticate** to **QSTodoService** with the following definition:</span></span>

        public async Task Authenticate(UIViewController view)
        {
            try
            {
                AppDelegate.ResumeWithURL = url => url.Scheme == "zumoe2etestapp" && client.ResumeWithURL(url);
                user = await client.LoginAsync(view, MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine (@"ERROR - AUTHENTICATION FAILED {0}", ex.Message);
            }
        }

    >[AZURE.NOTE] <span data-ttu-id="9fbe6-141">Si vous utilisez un autre fournisseur d’identité que Facebook, remplacez la valeur passée à la méthode **LoginAsync** ci-dessus par l’une des valeurs suivantes : _MicrosoftAccount_, _Twitter_, _Google_ ou _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-141">If you are using an identity provider other than a Facebook, change the value passed to **LoginAsync** above to one of the following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="9fbe6-142">Ouvrez **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="9fbe6-143">Modifiez la définition de méthode de **ViewDidLoad** pour supprimer l’appel à **RefreshAsync()** vers la fin :</span><span class="sxs-lookup"><span data-stu-id="9fbe6-143">Modify the method definition of **ViewDidLoad** removing the call to **RefreshAsync()** near the end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out the call to RefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="9fbe6-144">Modifiez la méthode **RefreshAsync** pour vous authentifier si la propriété **User** a la valeur null.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-144">Modify the method **RefreshAsync** to authenticate if the **User** property is null.</span></span> <span data-ttu-id="9fbe6-145">Ajoutez le code suivant en haut de la définition de méthode :</span><span class="sxs-lookup"><span data-stu-id="9fbe6-145">Add the following code at the top of the method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="9fbe6-146">Ouvrez **AppDelegate.cs** et ajoutez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="9fbe6-146">Open **AppDelegate.cs**, add the following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="9fbe6-147">Ouvrez le fichier **Info.plist** et accédez à **Types d’URL** dans la section **Avancé**.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-147">Open **Info.plist** file, navigate to **URL Types** in the **Advanced** section.</span></span> <span data-ttu-id="9fbe6-148">À présent, configurez l’**identificateur** et les **schémas d’URL** de votre type d’URL et cliquez sur **Ajouter un type d’URL**.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-148">Now configure the **Identifier** and the **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="9fbe6-149">Les **schémas d’URL** doivent être les mêmes que votre {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-149">**URL Schemes** should be the same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="9fbe6-150">Dans Visual Studio ou Xamarin Studio connecté à votre hôte de build Xamarin sur votre Mac, exécutez le projet client ciblant un périphérique ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-150">In Visual Studio or Xamarin Studio connected to your Xamarin Build Host on your Mac, run the client project targeting a device or emulator.</span></span> <span data-ttu-id="9fbe6-151">Vérifiez que l'application n'affiche aucune donnée.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-151">Verify that the app displays no data.</span></span>
   
    <span data-ttu-id="9fbe6-152">Effectuez le geste d'actualisation en affichant la liste des éléments, ce qui fait apparaître l'écran de connexion.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-152">Perform the refresh gesture by pulling down the list of items, which will cause the login screen to appear.</span></span> <span data-ttu-id="9fbe6-153">Une fois que vous avez entré des informations d'identification valides, l'application affiche la liste des tâches et vous pouvez mettre à jour les données.</span><span class="sxs-lookup"><span data-stu-id="9fbe6-153">Once you have successfully entered valid credentials, the app will display the list of todo items, and you can make updates to the data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
<span data-ttu-id="9fbe6-154">[Création d’une application Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md</span><span class="sxs-lookup"><span data-stu-id="9fbe6-154">[Create a Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started.md</span></span>