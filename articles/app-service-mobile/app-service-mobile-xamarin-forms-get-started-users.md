---
title: "aaaGet démarré avec une authentification pour les applications mobiles dans une application Xamarin Forms | Documents Microsoft"
description: "Découvrez comment toouse Mobile Apps tooauthenticate les utilisateurs de votre application Xamarin Forms via une variété de fournisseurs d’identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: panarasi
manager: syntaxc4
editor: 
ms.assetid: 9c55e192-c761-4ff2-8d88-72260e9f6179
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: panarasi
ms.openlocfilehash: 7f6716619f33d9cc4f866c41effba8f048dc49fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarin-forms-app"></a><span data-ttu-id="cde2c-103">Ajouter une application de Xamarin Forms tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="cde2c-103">Add authentication tooyour Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="cde2c-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cde2c-104">Overview</span></span>
<span data-ttu-id="cde2c-105">Cette rubrique vous montre comment les utilisateurs de tooauthenticate d’une application Service d’applications mobiles à partir de votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="cde2c-105">This topic shows you how tooauthenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="cde2c-106">Dans ce didacticiel, vous ajoutez l’authentification au projet de démarrage rapide de Xamarin Forms hello à l’aide d’un fournisseur d’identité qui est pris en charge par le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="cde2c-106">In this tutorial, you add authentication to hello Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="cde2c-107">Une fois en cours a été authentifié et autorisé par votre application Mobile, la valeur d’ID utilisateur hello s’affiche, et vous serez en mesure de tooaccess restreint les données de table.</span><span class="sxs-lookup"><span data-stu-id="cde2c-107">After being successfully authenticated and authorized by your Mobile App, hello user ID value is displayed, and you will be able tooaccess restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cde2c-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cde2c-108">Prerequisites</span></span>
<span data-ttu-id="cde2c-109">Pour un résultat optimal de hello avec ce didacticiel, nous vous recommandons d’effectuer tout d’abord hello [créer une application Xamarin Forms] [ 1] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="cde2c-109">For hello best result with this tutorial, we recommend that you first complete hello [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="cde2c-110">Après avoir terminé ce didacticiel, vous disposerez d’un projet Xamarin Forms qui est une application TodoList multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="cde2c-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="cde2c-111">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter le projet tooyour de package d’extension d’authentification de hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-111">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="cde2c-112">Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][2].</span><span class="sxs-lookup"><span data-stu-id="cde2c-112">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="cde2c-113">Inscription de votre application pour l'authentification et configuration d'App Services</span><span class="sxs-lookup"><span data-stu-id="cde2c-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="cde2c-114"><a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application</span><span class="sxs-lookup"><span data-stu-id="cde2c-114"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="cde2c-115">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="cde2c-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="cde2c-116">Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="cde2c-116">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="cde2c-117">Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="cde2c-117">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="cde2c-118">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="cde2c-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="cde2c-119">Il doit être unique tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="cde2c-119">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="cde2c-120">redirection de hello tooenable côté serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="cde2c-120">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="cde2c-121">Bonjour [Azure portal], sélectionnez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="cde2c-121">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="cde2c-122">Cliquez sur hello **l’authentification / autorisation** option de menu.</span><span class="sxs-lookup"><span data-stu-id="cde2c-122">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="cde2c-123">Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="cde2c-123">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="cde2c-124">Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="cde2c-124">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="cde2c-125">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="cde2c-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="cde2c-126">Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="cde2c-126">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="cde2c-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="cde2c-127">Click **OK**.</span></span>

5. <span data-ttu-id="cde2c-128">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="cde2c-128">Click **Save**.</span></span>

## <a name="restrict-permissions-tooauthenticated-users"></a><span data-ttu-id="cde2c-129">Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="cde2c-129">Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a><span data-ttu-id="cde2c-130">Ajout d’une bibliothèque de classes portable toohello d’authentification</span><span class="sxs-lookup"><span data-stu-id="cde2c-130">Add authentication toohello portable class library</span></span>
<span data-ttu-id="cde2c-131">Applications mobiles utilise hello [LoginAsync] [ 3] méthode d’extension sur hello [MobileServiceClient] [ 4] toosign un utilisateur avec le Service d’applications authentification.</span><span class="sxs-lookup"><span data-stu-id="cde2c-131">Mobile Apps uses hello [LoginAsync][3] extension method on hello [MobileServiceClient][4] toosign in a user with App Service authentication.</span></span> <span data-ttu-id="cde2c-132">Cet exemple utilise un flux d’authentification de serveur géré qui affiche l’interface de connexion du fournisseur hello dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-132">This sample uses a server-managed authentication flow that displays hello provider's sign-in interface in hello app.</span></span> <span data-ttu-id="cde2c-133">Pour plus d’informations, voir la rubrique [Authentification gérée par le serveur][5].</span><span class="sxs-lookup"><span data-stu-id="cde2c-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="cde2c-134">Pour offrir une meilleure expérience utilisateur dans votre application de production, vous devez plutôt envisager d’utiliser une [authentification gérée par le client][6].</span><span class="sxs-lookup"><span data-stu-id="cde2c-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="cde2c-135">tooauthenticate avec un projet Xamarin Forms, définir un **IAuthenticate** interface Bonjour bibliothèque de classes Portable pour une application hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-135">tooauthenticate with a Xamarin Forms project, define an **IAuthenticate** interface in hello Portable Class Library for hello app.</span></span> <span data-ttu-id="cde2c-136">Ajoutez ensuite une **connectez-vous** défini dans hello bibliothèque de classes portables, ce qui vous cliquez sur l’interface utilisateur toohello bouton toostart authentification.</span><span class="sxs-lookup"><span data-stu-id="cde2c-136">Then add a **Sign-in** button toohello user interface defined in hello Portable Class Library, which you click toostart authentication.</span></span> <span data-ttu-id="cde2c-137">Après une authentification réussie, les données sont chargées à partir du serveur principal d’application mobile hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-137">Data is loaded from hello mobile app backend after successful authentication.</span></span>

<span data-ttu-id="cde2c-138">Hello d’implémenter **IAuthenticate** interface pour chaque plateforme prise en charge par votre application.</span><span class="sxs-lookup"><span data-stu-id="cde2c-138">Implement hello **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="cde2c-139">Dans Visual Studio ou Xamarin Studio, ouvrez App.cs du projet hello avec **Portable** dans nom hello, qui est un projet de bibliothèque de classes portables, puis ajoutez hello suivant `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="cde2c-139">In Visual Studio or Xamarin Studio, open App.cs from hello project with **Portable** in hello name, which is Portable Class Library project, then  add hello following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="cde2c-140">Dans App.cs, ajoutez hello qui suit `IAuthenticate` définition immédiatement avant hello d’interface `App` définition de classe.</span><span class="sxs-lookup"><span data-stu-id="cde2c-140">In App.cs, add hello following `IAuthenticate` interface definition immediately before hello `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="cde2c-141">interface de hello tooinitialize avec une implémentation spécifique à la plateforme, ajouter hello suivant des membres statiques toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="cde2c-141">tooinitialize hello interface with a platform-specific implementation, add hello following static members toohello **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="cde2c-142">Ouvrez TodoList.xaml à partir du projet de bibliothèque de classes portables hello, ajoutez hello **bouton** élément Bonjour *buttonsPanel* layout (élément), après le bouton hello :</span><span class="sxs-lookup"><span data-stu-id="cde2c-142">Open TodoList.xaml from hello Portable Class Library project, add hello following **Button** element in hello *buttonsPanel* layout element, after hello existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="cde2c-143">Ce bouton déclenche l’authentification gérée par le serveur auprès du serveur principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="cde2c-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="cde2c-144">Ouvrez TodoList.xaml.cs à partir du projet de bibliothèque de classes portables hello, puis ajoutez les hello suivant champ toohello `TodoList` classe :</span><span class="sxs-lookup"><span data-stu-id="cde2c-144">Open TodoList.xaml.cs from hello Portable Class Library project, then add hello following field toohello `TodoList` class:</span></span>

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="cde2c-145">Remplacez hello **OnAppearing** méthode avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="cde2c-145">Replace hello **OnAppearing** method with hello following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems tootrue in order toosynchronize hello data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide hello Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="cde2c-146">Ce code permet de s’assurer que les données sont uniquement actualisées à partir du service de hello une fois que vous avez été authentifié.</span><span class="sxs-lookup"><span data-stu-id="cde2c-146">This code makes sure that data is only refreshed from hello service after you have been authenticated.</span></span>
7. <span data-ttu-id="cde2c-147">Ajouter hello suivant gestionnaire pour hello **Clicked** événement toohello **TodoList** classe :</span><span class="sxs-lookup"><span data-stu-id="cde2c-147">Add hello following handler for hello **Clicked** event toohello **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="cde2c-148">Enregistrez vos modifications et régénérer le projet de bibliothèque de classes portables hello vérification sans erreurs.</span><span class="sxs-lookup"><span data-stu-id="cde2c-148">Save your changes and rebuild hello Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-toohello-android-app"></a><span data-ttu-id="cde2c-149">Ajouter une application Android de l’authentification toohello</span><span class="sxs-lookup"><span data-stu-id="cde2c-149">Add authentication toohello Android app</span></span>
<span data-ttu-id="cde2c-150">Cette section montre comment tooimplement hello **IAuthenticate** interface dans un projet d’application Android hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-150">This section shows how tooimplement hello **IAuthenticate** interface in hello Android app project.</span></span> <span data-ttu-id="cde2c-151">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Android.</span><span class="sxs-lookup"><span data-stu-id="cde2c-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="cde2c-152">Dans Visual Studio ou Xamarin Studio, avec le bouton droit hello **droid** de projet, puis **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="cde2c-152">In Visual Studio or Xamarin Studio, right-click hello **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="cde2c-153">Hello de toostart appuyez sur F5 dans le débogueur de hello du projet, puis vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="cde2c-153">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="cde2c-154">code de 401 Hello se produit car l’accès sur les principaux hello est utilisateurs tooauthorized restreint uniquement.</span><span class="sxs-lookup"><span data-stu-id="cde2c-154">hello 401 code is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="cde2c-155">Ouvrez MainActivity.cs dans les projets Android hello et ajoutez hello suit `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="cde2c-155">Open MainActivity.cs in hello Android project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="cde2c-156">Hello de mise à jour **MainActivity** hello tooimplement de classe **IAuthenticate** d’interface, comme suit :</span><span class="sxs-lookup"><span data-stu-id="cde2c-156">Update hello **MainActivity** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="cde2c-157">Hello de mise à jour **MainActivity** classe en ajoutant une **MobileServiceUser** champ et un **authentifier** (méthode), ce qui est requis par hello **IAuthenticate**  d’interface, comme suit :</span><span class="sxs-lookup"><span data-stu-id="cde2c-157">Update hello **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                user = await TodoItemManager.DefaultManager.CurrentClient.LoginAsync(this, 
                    MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                if (user != null)
                {
                    message = string.Format("you are now signed-in as {0}.",
                        user.UserId);
                    success = true;
                }
            }
            catch (Exception ex)
            {
                message = ex.Message;
            }

            // Display hello success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="cde2c-158">Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="cde2c-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="cde2c-159">Ajouter hello suivant du code à l’intérieur <application> nœud de AndroidManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="cde2c-159">Add hello following code inside <application> node of AndroidManifest.xml:</span></span>

```xml
    <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
      <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
      </intent-filter>
    </activity>
```

1. <span data-ttu-id="cde2c-160">Ajouter hello suivant code toohello **OnCreate** méthode Hello **MainActivity** trop de classe avant l’appel de hello`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="cde2c-160">Add hello following code toohello **OnCreate** method of hello **MainActivity** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="cde2c-161">Ce code garantit l’authentificateur de hello est initialisée avant application hello charge.</span><span class="sxs-lookup"><span data-stu-id="cde2c-161">This code ensures hello authenticator is initialized before hello app loads.</span></span>
2. <span data-ttu-id="cde2c-162">Régénérer l’application hello, exécutez-le, puis connectez-vous avec le fournisseur d’authentification hello vous avez choisi et vérifiez que vous tooaccess en mesure des données sous la forme d’un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="cde2c-162">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toohello-ios-app"></a><span data-ttu-id="cde2c-163">Ajouter une application de l’authentification toohello iOS</span><span class="sxs-lookup"><span data-stu-id="cde2c-163">Add authentication toohello iOS app</span></span>
<span data-ttu-id="cde2c-164">Cette section montre comment tooimplement hello **IAuthenticate** interface dans un projet d’application iOS hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-164">This section shows how tooimplement hello **IAuthenticate** interface in hello iOS app project.</span></span> <span data-ttu-id="cde2c-165">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="cde2c-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="cde2c-166">Dans Visual Studio ou Xamarin Studio, avec le bouton droit hello **iOS** de projet, puis **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="cde2c-166">In Visual Studio or Xamarin Studio, right-click hello **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="cde2c-167">Hello de toostart appuyez sur F5 dans le débogueur de hello du projet, puis vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-167">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="cde2c-168">les réponses 401 Hello se produit car l’accès sur les principaux hello est utilisateurs tooauthorized restreint uniquement.</span><span class="sxs-lookup"><span data-stu-id="cde2c-168">hello 401 response is produced because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="cde2c-169">Ouvrez AppDelegate.cs dans projet iOS, hello et ajoutez hello suit `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="cde2c-169">Open AppDelegate.cs in hello iOS project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="cde2c-170">Hello de mise à jour **AppDelegate** hello tooimplement de classe **IAuthenticate** d’interface, comme suit :</span><span class="sxs-lookup"><span data-stu-id="cde2c-170">Update hello **AppDelegate** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="cde2c-171">Hello de mise à jour **AppDelegate** classe en ajoutant une **MobileServiceUser** champ et un **authentifier** (méthode), ce qui est requis par hello **IAuthenticate**  d’interface, comme suit :</span><span class="sxs-lookup"><span data-stu-id="cde2c-171">Update hello **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            var success = false;
            var message = string.Empty;
            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(UIApplication.SharedApplication.KeyWindow.RootViewController,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                        success = true;
                    }
                }
            }
            catch (Exception ex)
            {
               message = ex.Message;
            }

            // Display hello success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="cde2c-172">Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="cde2c-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="cde2c-173">Mettre à jour de la classe de AppDelegate hello en ajoutant la surcharge de méthode OpenUrl (options du NSDictionary application, les url NSUrl, UIApplication)</span><span class="sxs-lookup"><span data-stu-id="cde2c-173">Update hello AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="cde2c-174">Ajouter hello suivant la ligne de code toohello **FinishedLaunching** méthode hello avant d’appeler trop`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="cde2c-174">Add hello following line of code toohello **FinishedLaunching** method before hello call too`LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="cde2c-175">Ce code garantit l’authentificateur de hello est initialisée avant l’application hello est chargée.</span><span class="sxs-lookup"><span data-stu-id="cde2c-175">This code ensures hello authenticator is initialized before hello app is loaded.</span></span>

6. <span data-ttu-id="cde2c-176">Ajouter **{url_scheme_of_your_app}** tooURL des schémas dans le fichier Info.plist.</span><span class="sxs-lookup"><span data-stu-id="cde2c-176">Add **{url_scheme_of_your_app}** tooURL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="cde2c-177">Régénérer l’application hello, exécutez-le, puis connectez-vous avec le fournisseur d’authentification hello vous avez choisi et vérifiez que vous tooaccess en mesure des données sous la forme d’un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="cde2c-177">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a><span data-ttu-id="cde2c-178">Ajouter l’authentification tooWindows 10 (y compris téléphone) projets d’application</span><span class="sxs-lookup"><span data-stu-id="cde2c-178">Add authentication tooWindows 10 (including Phone) app projects</span></span>
<span data-ttu-id="cde2c-179">Cette section montre comment tooimplement hello **IAuthenticate** interface dans les projets d’application hello Windows 10.</span><span class="sxs-lookup"><span data-stu-id="cde2c-179">This section shows how tooimplement hello **IAuthenticate** interface in hello Windows 10 app projects.</span></span> <span data-ttu-id="cde2c-180">Hello mêmes étapes s’appliquent aux projets de plateforme Windows universelle (UWP), mais à l’aide de hello **UWP** projet (avec les modifications indiquées).</span><span class="sxs-lookup"><span data-stu-id="cde2c-180">hello same steps apply for Universal Windows Platform (UWP) projects, but using hello **UWP** project (with noted changes).</span></span> <span data-ttu-id="cde2c-181">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="cde2c-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="cde2c-182">« Dans Visual Studio, avec le bouton droit soit hello **UWP** de projet, puis **définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="cde2c-182">"In Visual Studio, right-click either hello **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="cde2c-183">Hello de toostart appuyez sur F5 dans le débogueur de hello du projet, puis vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="cde2c-183">Press F5 toostart hello project in hello debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="cde2c-184">les réponses 401 Hello se produit car l’accès sur les principaux hello est utilisateurs tooauthorized restreint uniquement.</span><span class="sxs-lookup"><span data-stu-id="cde2c-184">hello 401 response happens because access on hello backend is restricted tooauthorized users only.</span></span>
3. <span data-ttu-id="cde2c-185">Ouvrez MainPage.xaml.cs pour le projet d’application Windows hello et ajoutez hello suit `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="cde2c-185">Open MainPage.xaml.cs for hello Windows app project and add hello following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="cde2c-186">Remplacez `<your_Portable_Class_Library_namespace>` avec l’espace de noms hello pour votre bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="cde2c-186">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>
4. <span data-ttu-id="cde2c-187">Hello de mise à jour **MainPage** hello tooimplement de classe **IAuthenticate** d’interface, comme suit :</span><span class="sxs-lookup"><span data-stu-id="cde2c-187">Update hello **MainPage** class tooimplement hello **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="cde2c-188">Hello de mise à jour **MainPage** classe en ajoutant une **MobileServiceUser** champ et un **authentifier** (méthode), ce qui est requis par hello **IAuthenticate** de l’interface, comme suit :</span><span class="sxs-lookup"><span data-stu-id="cde2c-188">Update hello **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by hello **IAuthenticate** interface, as follows:</span></span>

        // Define a authenticated user.
        private MobileServiceUser user;

        public async Task<bool> Authenticate()
        {
            string message = string.Empty;
            var success = false;

            try
            {
                // Sign in with Facebook login using a server-managed flow.
                if (user == null)
                {
                    user = await TodoItemManager.DefaultManager.CurrentClient
                        .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    if (user != null)
                    {
                        success = true;
                        message = string.Format("You are now signed-in as {0}.", user.UserId);
                    }
                }

            }
            catch (Exception ex)
            {
                message = string.Format("Authentication Failed: {0}", ex.Message);
            }

            // Display hello success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="cde2c-189">Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="cde2c-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="cde2c-190">Ajouter hello suivant la ligne de code dans le constructeur hello pour hello **MainPage** trop de classe avant l’appel de hello`LoadApplication()`:</span><span class="sxs-lookup"><span data-stu-id="cde2c-190">Add hello following line of code in hello constructor for hello **MainPage** class before hello call too`LoadApplication()`:</span></span>

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="cde2c-191">Remplacez `<your_Portable_Class_Library_namespace>` avec l’espace de noms hello pour votre bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="cde2c-191">Replace `<your_Portable_Class_Library_namespace>` with hello namespace for your portable class library.</span></span>

3. <span data-ttu-id="cde2c-192">Si vous utilisez **UWP**, ajoutez hello suivant **OnActivated** toohello de substitution de méthode **application** classe :</span><span class="sxs-lookup"><span data-stu-id="cde2c-192">If you are using **UWP**, add hello following **OnActivated** method override toohello **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="cde2c-193">Lors de la substitution de méthode hello existe déjà, ajoutez le code de conditionnelle de hello de hello précédant l’extrait de code.</span><span class="sxs-lookup"><span data-stu-id="cde2c-193">When hello method override already exists, add hello conditional code from hello preceding snippet.</span></span>  <span data-ttu-id="cde2c-194">Ce code n’est pas requis pour les projets Windows universel.</span><span class="sxs-lookup"><span data-stu-id="cde2c-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="cde2c-195">Ajoutez **{url_scheme_of_your_app}** dans Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="cde2c-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="cde2c-196">Régénérer l’application hello, exécutez-le, puis connectez-vous avec le fournisseur d’authentification hello vous avez choisi et vérifiez que vous tooaccess en mesure des données sous la forme d’un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="cde2c-196">Rebuild hello app, run it, then sign in with hello authentication provider you chose and verify you are able tooaccess data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cde2c-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cde2c-197">Next steps</span></span>
<span data-ttu-id="cde2c-198">Maintenant que vous terminé ce didacticiel de l’authentification de base, pensez à poursuivre sur tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="cde2c-198">Now that you completed this basic authentication tutorial, consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="cde2c-199">Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="cde2c-199">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="cde2c-200">Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer votre application Mobile back-end toouse Azure Notification Hubs toosend les notifications de transmission.</span><span class="sxs-lookup"><span data-stu-id="cde2c-200">Learn how tooadd push notifications support tooyour app and configure your Mobile App backend toouse Azure Notification Hubs toosend push notifications.</span></span>
* [<span data-ttu-id="cde2c-201">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="cde2c-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="cde2c-202">Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un service principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="cde2c-202">Learn how tooadd offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="cde2c-203">Synchronisation hors connexion permet de toointeract des utilisateurs finaux avec une application mobile - affichage, l’ajout ou la modification de données - même quand il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="cde2c-203">Offline sync allows end users toointeract with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
