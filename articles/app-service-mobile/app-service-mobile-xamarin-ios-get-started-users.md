---
title: "aaaGet démarré avec une authentification pour les applications mobiles dans Xamarin iOS"
description: "Découvrez comment toouse Mobile Apps tooauthenticate les utilisateurs de votre application Xamarin iOS via une variété de fournisseurs d’identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
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
ms.openlocfilehash: 6458e9651b03df61c86b88b11953792e04bfa5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinios-app"></a><span data-ttu-id="88f1e-103">Ajouter une application de l’authentification tooyour Xamarin.iOS</span><span class="sxs-lookup"><span data-stu-id="88f1e-103">Add authentication tooyour Xamarin.iOS app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="88f1e-104">Cette rubrique vous montre comment les utilisateurs de tooauthenticate d’une application Service d’applications mobiles à partir de votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="88f1e-104">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="88f1e-105">Dans ce didacticiel, vous ajoutez de projet de démarrage rapide d’authentification toohello Xamarin.iOS à l’aide d’un fournisseur d’identité qui est pris en charge par le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="88f1e-105">In this tutorial, you add authentication toohello Xamarin.iOS quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="88f1e-106">Une fois en cours a été authentifié et autorisé par votre application Mobile, la valeur d’ID utilisateur hello s’affiche et vous serez en mesure de tooaccess restreint les données de table.</span><span class="sxs-lookup"><span data-stu-id="88f1e-106">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed and you will be able tooaccess restricted table data.</span></span>

<span data-ttu-id="88f1e-107">Vous devez d’abord terminer le didacticiel de hello [créer une application Xamarin.iOS].</span><span class="sxs-lookup"><span data-stu-id="88f1e-107">You must first complete hello tutorial [Create a Xamarin.iOS app].</span></span> <span data-ttu-id="88f1e-108">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter le projet tooyour de package d’extension d’authentification de hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-108">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="88f1e-109">Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="88f1e-109">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="88f1e-110">Inscription de votre application pour l'authentification et configuration d'App Services</span><span class="sxs-lookup"><span data-stu-id="88f1e-110">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a><span data-ttu-id="88f1e-111">Ajouter votre URL de redirection externe d’autorisé toohello application</span><span class="sxs-lookup"><span data-stu-id="88f1e-111">Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="88f1e-112">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="88f1e-112">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="88f1e-113">Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="88f1e-113">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="88f1e-114">Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="88f1e-114">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="88f1e-115">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="88f1e-115">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="88f1e-116">Il doit être unique tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="88f1e-116">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="88f1e-117">redirection de hello tooenable côté serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="88f1e-117">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="88f1e-118">Bonjour [Azure portal], sélectionnez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="88f1e-118">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="88f1e-119">Cliquez sur hello **l’authentification / autorisation** option de menu.</span><span class="sxs-lookup"><span data-stu-id="88f1e-119">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="88f1e-120">Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="88f1e-120">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="88f1e-121">Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="88f1e-121">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="88f1e-122">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="88f1e-122">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="88f1e-123">Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="88f1e-123">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="88f1e-124">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="88f1e-124">Click **OK**.</span></span>

5. <span data-ttu-id="88f1e-125">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="88f1e-125">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="88f1e-126">Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="88f1e-126">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="88f1e-127">&nbsp;&nbsp;4.</span><span class="sxs-lookup"><span data-stu-id="88f1e-127">&nbsp;&nbsp;4.</span></span> <span data-ttu-id="88f1e-128">Dans Visual Studio ou Xamarin Studio, exécutez le projet de client de hello sur un périphérique ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="88f1e-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="88f1e-129">Vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="88f1e-130">Échec de Hello est console connecté toohello du débogueur de hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-130">hello failure is logged toohello console of hello debugger.</span></span> <span data-ttu-id="88f1e-131">Par conséquent, dans Visual Studio, vous devez voir un échec hello dans la fenêtre de sortie hello.</span><span class="sxs-lookup"><span data-stu-id="88f1e-131">So in Visual Studio, you should see hello failure in hello output window.</span></span>

<span data-ttu-id="88f1e-132">&nbsp;&nbsp;Cet échec non autorisé se produit, car l’application hello tente tooaccess service principal de votre application Mobile comme un utilisateur non authentifié.</span><span class="sxs-lookup"><span data-stu-id="88f1e-132">&nbsp;&nbsp;This unauthorized failure happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="88f1e-133">Hello *TodoItem* table requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="88f1e-133">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="88f1e-134">Ensuite, vous mettrez à jour des ressources de toorequest application hello client à partir du serveur principal de l’application Mobile hello avec un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="88f1e-134">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <a name="add-authentication-toohello-app"></a><span data-ttu-id="88f1e-135">Ajouter une application de toohello d’authentification</span><span class="sxs-lookup"><span data-stu-id="88f1e-135">Add authentication toohello app</span></span>
<span data-ttu-id="88f1e-136">Dans cette section, vous allez modifier hello application toodisplay un écran de connexion avant d’afficher des données.</span><span class="sxs-lookup"><span data-stu-id="88f1e-136">In this section, you will modify hello app toodisplay a login screen before displaying data.</span></span> <span data-ttu-id="88f1e-137">Au démarrage de l’application hello, il se connecte pas pas tooyour du Service d’applications et n’affichera pas les données.</span><span class="sxs-lookup"><span data-stu-id="88f1e-137">When hello app starts, it will not not connect tooyour App Service and will not display any data.</span></span> <span data-ttu-id="88f1e-138">Après hello première hello effectuées par l’utilisateur hello actualisation mouvement, écran de connexion hello s’affiche. après l’ouverture de session réussie hello liste des éléments de tâche s’affiche.</span><span class="sxs-lookup"><span data-stu-id="88f1e-138">After hello first time that hello user performs hello refresh gesture, hello login screen will appear; after successful login hello list of todo items will be displayed.</span></span>

1. <span data-ttu-id="88f1e-139">Dans le projet de client hello, ouvrez le fichier de hello **QSTodoService.cs** et ajoutez hello qui suit à l’aide d’instruction et `MobileServiceUser` avec un accesseur toohello QSTodoService classe :</span><span class="sxs-lookup"><span data-stu-id="88f1e-139">In hello client project, open hello file **QSTodoService.cs** and add hello following using statement and `MobileServiceUser` with accessor toohello QSTodoService class:</span></span>
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. <span data-ttu-id="88f1e-140">Ajouter la nouvelle méthode nommée **authentifier** trop**QSTodoService** avec hello définition :</span><span class="sxs-lookup"><span data-stu-id="88f1e-140">Add new method named **Authenticate** too**QSTodoService** with hello following definition:</span></span>

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

    >[AZURE.NOTE] <span data-ttu-id="88f1e-141">Si vous utilisez un fournisseur d’identité autre qu’un Facebook, modifiez la valeur hello passé trop**LoginAsync** ci-dessus tooone suivants de hello : _MicrosoftAccount_, _Twitter_, _Google_, ou _WindowsAzureActiveDirectory_.</span><span class="sxs-lookup"><span data-stu-id="88f1e-141">If you are using an identity provider other than a Facebook, change hello value passed too**LoginAsync** above tooone of hello following: _MicrosoftAccount_, _Twitter_, _Google_, or _WindowsAzureActiveDirectory_.</span></span>

3. <span data-ttu-id="88f1e-142">Ouvrez **QSTodoListViewController.cs**.</span><span class="sxs-lookup"><span data-stu-id="88f1e-142">Open **QSTodoListViewController.cs**.</span></span> <span data-ttu-id="88f1e-143">Modifier la définition de méthode hello de **ViewDidLoad** suppression trop d’appels de hello**RefreshAsync()** près de fin de hello :</span><span class="sxs-lookup"><span data-stu-id="88f1e-143">Modify hello method definition of **ViewDidLoad** removing hello call too**RefreshAsync()** near hello end:</span></span>
   
        public override async void ViewDidLoad ()
        {
            base.ViewDidLoad ();
   
            todoService = QSTodoService.DefaultService;
            await todoService.InitializeStoreAsync();
   
            RefreshControl.ValueChanged += async (sender, e) => {
                await RefreshAsync();
            }
   
            // Comment out hello call tooRefreshAsync
            // await RefreshAsync();
        }
4. <span data-ttu-id="88f1e-144">Modifier la méthode hello **RefreshAsync** tooauthenticate si hello **utilisateur** propriété a la valeur null.</span><span class="sxs-lookup"><span data-stu-id="88f1e-144">Modify hello method **RefreshAsync** tooauthenticate if hello **User** property is null.</span></span> <span data-ttu-id="88f1e-145">Ajoutez hello suivant code haut hello de définition de méthode hello :</span><span class="sxs-lookup"><span data-stu-id="88f1e-145">Add hello following code at hello top of hello method definition:</span></span>
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. <span data-ttu-id="88f1e-146">Ouvrez **AppDelegate.cs**, ajouter hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="88f1e-146">Open **AppDelegate.cs**, add hello following method:</span></span>

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. <span data-ttu-id="88f1e-147">Ouvrez **Info.plist** de fichiers, accédez trop**Types d’URL** Bonjour **avancé** section.</span><span class="sxs-lookup"><span data-stu-id="88f1e-147">Open **Info.plist** file, navigate too**URL Types** in hello **Advanced** section.</span></span> <span data-ttu-id="88f1e-148">À présent configurer hello **identificateur** et hello **schémas d’URL** de votre Type d’URL et un clic **ajouter un Type URL**.</span><span class="sxs-lookup"><span data-stu-id="88f1e-148">Now configure hello **Identifier** and hello **URL Schemes** of your URL Type and click **Add URL Type**.</span></span> <span data-ttu-id="88f1e-149">**Schémas d’URL** doit être le même hello en tant que votre {url_scheme_of_your_app}.</span><span class="sxs-lookup"><span data-stu-id="88f1e-149">**URL Schemes** should be hello same as your {url_scheme_of_your_app}.</span></span>
7. <span data-ttu-id="88f1e-150">Dans Visual Studio ou Xamarin Studio connecté tooyour hôte de Build Xamarin sur votre Mac, exécutez projet de client hello ciblant un périphérique ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="88f1e-150">In Visual Studio or Xamarin Studio connected tooyour Xamarin Build Host on your Mac, run hello client project targeting a device or emulator.</span></span> <span data-ttu-id="88f1e-151">Vérifiez que cette application hello n’affiche aucune donnée.</span><span class="sxs-lookup"><span data-stu-id="88f1e-151">Verify that hello app displays no data.</span></span>
   
    <span data-ttu-id="88f1e-152">Effectuer des mouvements d’actualisation hello en les extrayant hello liste déroulante d’éléments, ce qui provoque l’hello connexion écran tooappear.</span><span class="sxs-lookup"><span data-stu-id="88f1e-152">Perform hello refresh gesture by pulling down hello list of items, which will cause hello login screen tooappear.</span></span> <span data-ttu-id="88f1e-153">Une fois que vous avez correctement entré les informations d’identification valides, application hello affiche liste hello des éléments de tâche, et vous pouvez apporter des mises à jour toohello données.</span><span class="sxs-lookup"><span data-stu-id="88f1e-153">Once you have successfully entered valid credentials, hello app will display hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[créer une application Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md