---
title: "Prise en main de l’authentification pour Mobile Apps dans l’application Xamarin Forms | Microsoft Docs"
description: "Découvrez comment utiliser Mobile Apps pour authentifier les utilisateurs de votre application Xamarin Forms via divers fournisseurs d'identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
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
ms.openlocfilehash: 9e14e95793bcc81ad46783fd50ba223eec4ea360
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="add-authentication-to-your-xamarin-forms-app"></a><span data-ttu-id="3e447-103">Ajouter l’authentification à votre application Xamarin Forms</span><span class="sxs-lookup"><span data-stu-id="3e447-103">Add authentication to your Xamarin Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a><span data-ttu-id="3e447-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3e447-104">Overview</span></span>
<span data-ttu-id="3e447-105">Cette rubrique montre comment authentifier les utilisateurs d'une application App Service Mobile App à partir de votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="3e447-105">This topic shows you how to authenticate users of an App Service Mobile App from your client application.</span></span> <span data-ttu-id="3e447-106">Dans ce didacticiel, vous allez ajouter l’authentification au projet de démarrage rapide Xamarin Forms à l’aide d’un fournisseur d’identité pris en charge par App Service.</span><span class="sxs-lookup"><span data-stu-id="3e447-106">In this tutorial, you add authentication to the Xamarin Forms quickstart project using an identity provider that is supported by App Service.</span></span> <span data-ttu-id="3e447-107">Une fois l’utilisateur authentifié et autorisé par votre application Mobile App, la valeur de l’ID utilisateur s’affiche ; vous pouvez alors accéder aux données de table limitées.</span><span class="sxs-lookup"><span data-stu-id="3e447-107">After being successfully authenticated and authorized by your Mobile App, the user ID value is displayed, and you will be able to access restricted table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e447-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3e447-108">Prerequisites</span></span>
<span data-ttu-id="3e447-109">Pour obtenir les meilleurs résultats avec ce didacticiel, nous vous recommandons de commencer par suivre le didacticiel [Créer une application Xamarin.Forms][1].</span><span class="sxs-lookup"><span data-stu-id="3e447-109">For the best result with this tutorial, we recommend that you first complete the [Create a Xamarin Forms app][1] tutorial.</span></span> <span data-ttu-id="3e447-110">Après avoir terminé ce didacticiel, vous disposerez d’un projet Xamarin Forms qui est une application TodoList multiplateforme.</span><span class="sxs-lookup"><span data-stu-id="3e447-110">After you complete this tutorial, you will have a Xamarin Forms project that is a multi-platform TodoList app.</span></span>

<span data-ttu-id="3e447-111">Si vous n’utilisez pas le projet de serveur du démarrage rapide téléchargé, vous devez ajouter le package d’extension d’authentification à votre projet.</span><span class="sxs-lookup"><span data-stu-id="3e447-111">If you do not use the downloaded quick start server project, you must add the authentication extension package to your project.</span></span> <span data-ttu-id="3e447-112">Pour plus d'informations sur les packages d'extension de serveur, consultez [Fonctionnement avec le Kit de développement logiciel (SDK) du serveur principal .NET pour Azure Mobile Apps][2].</span><span class="sxs-lookup"><span data-stu-id="3e447-112">For more information about server extension packages, see [Work with the .NET backend server SDK for Azure Mobile Apps][2].</span></span>

## <a name="register-your-app-for-authentication-and-configure-app-services"></a><span data-ttu-id="3e447-113">Inscription de votre application pour l'authentification et configuration d'App Services</span><span class="sxs-lookup"><span data-stu-id="3e447-113">Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="3e447-114"><a name="redirecturl"></a>Ajouter votre application aux URL de redirection externes autorisées</span><span class="sxs-lookup"><span data-stu-id="3e447-114"><a name="redirecturl"></a>Add your app to the Allowed External Redirect URLs</span></span>

<span data-ttu-id="3e447-115">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="3e447-115">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="3e447-116">Cela permet au système d’authentification de vous rediriger vers votre application une fois le processus d’authentification terminé.</span><span class="sxs-lookup"><span data-stu-id="3e447-116">This allows the authentication system to redirect back to your app once the authentication process is complete.</span></span> <span data-ttu-id="3e447-117">Dans ce didacticiel, nous utilisons le schéma d’URL _appname_.</span><span class="sxs-lookup"><span data-stu-id="3e447-117">In this tutorial, we use the URL scheme _appname_ throughout.</span></span> <span data-ttu-id="3e447-118">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="3e447-118">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="3e447-119">Il doit être propre à votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="3e447-119">It should be unique to your mobile application.</span></span> <span data-ttu-id="3e447-120">Pour activer la redirection côté serveur, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-120">To enable the redirection on the server side:</span></span>

1. <span data-ttu-id="3e447-121">Dans le [portail Azure], sélectionnez votre instance App Service.</span><span class="sxs-lookup"><span data-stu-id="3e447-121">In the [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="3e447-122">Cliquez sur l’option de menu **Authentication/Authorisation**.</span><span class="sxs-lookup"><span data-stu-id="3e447-122">Click the **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="3e447-123">Dans **URL de redirection externes autorisées**, saisissez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="3e447-123">In the **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="3e447-124">La chaîne **url_scheme_of_your_app** de cette chaîne est le schéma d’URL de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="3e447-124">The **url_scheme_of_your_app** in this string is the URL Scheme for your mobile application.</span></span>  <span data-ttu-id="3e447-125">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="3e447-125">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="3e447-126">Vous devez noter la chaîne que vous choisissez, dans la mesure où vous devez ajuster votre code d’application mobile avec le schéma d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="3e447-126">You should make a note of the string that you choose as you will need to adjust your mobile application code with the URL Scheme in several places.</span></span>

4. <span data-ttu-id="3e447-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3e447-127">Click **OK**.</span></span>

5. <span data-ttu-id="3e447-128">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="3e447-128">Click **Save**.</span></span>

## <a name="restrict-permissions-to-authenticated-users"></a><span data-ttu-id="3e447-129">Restriction des autorisations pour les utilisateurs authentifiés</span><span class="sxs-lookup"><span data-stu-id="3e447-129">Restrict permissions to authenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-to-the-portable-class-library"></a><span data-ttu-id="3e447-130">Ajout de l'authentification à la bibliothèque de classes portable</span><span class="sxs-lookup"><span data-stu-id="3e447-130">Add authentication to the portable class library</span></span>
<span data-ttu-id="3e447-131">Mobile Apps utilise la méthode d’extension [LoginAsync][3] sur le [MobileServiceClient][4] pour connecter un utilisateur avec l’authentification App Service.</span><span class="sxs-lookup"><span data-stu-id="3e447-131">Mobile Apps uses the [LoginAsync][3] extension method on the [MobileServiceClient][4] to sign in a user with App Service authentication.</span></span> <span data-ttu-id="3e447-132">Cet exemple utilise un flux d’authentification géré par le serveur qui affiche l’interface de connexion du fournisseur dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-132">This sample uses a server-managed authentication flow that displays the provider's sign-in interface in the app.</span></span> <span data-ttu-id="3e447-133">Pour plus d’informations, voir la rubrique [Authentification gérée par le serveur][5].</span><span class="sxs-lookup"><span data-stu-id="3e447-133">For more information, see [Server-managed authentication][5].</span></span> <span data-ttu-id="3e447-134">Pour offrir une meilleure expérience utilisateur dans votre application de production, vous devez plutôt envisager d’utiliser une [authentification gérée par le client][6].</span><span class="sxs-lookup"><span data-stu-id="3e447-134">To provide a better user experience in your production app, you should consider instead using [Client-managed authentication][6].</span></span>

<span data-ttu-id="3e447-135">Pour vous authentifier auprès d’un projet Xamarin Forms, définissez une interface **IAuthenticate** dans la bibliothèque de classes portable de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-135">To authenticate with a Xamarin Forms project, define an **IAuthenticate** interface in the Portable Class Library for the app.</span></span> <span data-ttu-id="3e447-136">Ensuite, ajoutez un bouton **Connexion** à l’interface utilisateur définie dans la bibliothèque de classes portable que l’utilisateur devra sélectionner pour démarrer l’authentification.</span><span class="sxs-lookup"><span data-stu-id="3e447-136">Then add a **Sign-in** button to the user interface defined in the Portable Class Library, which you click to start authentication.</span></span> <span data-ttu-id="3e447-137">Une fois l’authentification effectuée, les données sont chargées depuis le serveur principal d’application mobile.</span><span class="sxs-lookup"><span data-stu-id="3e447-137">Data is loaded from the mobile app backend after successful authentication.</span></span>

<span data-ttu-id="3e447-138">Implémentez l’interface **IAuthenticate** pour chaque plateforme prise en charge par votre application.</span><span class="sxs-lookup"><span data-stu-id="3e447-138">Implement the **IAuthenticate** interface for each platform supported by your app.</span></span>

1. <span data-ttu-id="3e447-139">Dans Visual Studio ou Xamarin Studio, ouvrez App.cs à partir du projet dont le nom contient le terme **Portable** et qui correspond à un projet de bibliothèque de classes portable. Ajoutez ensuite l’instruction `using` suivante :</span><span class="sxs-lookup"><span data-stu-id="3e447-139">In Visual Studio or Xamarin Studio, open App.cs from the project with **Portable** in the name, which is Portable Class Library project, then  add the following `using` statement:</span></span>

        using System.Threading.Tasks;
2. <span data-ttu-id="3e447-140">Dans App.cs, ajoutez la définition d’interface `IAuthenticate` suivante immédiatement avant la définition de classe `App`.</span><span class="sxs-lookup"><span data-stu-id="3e447-140">In App.cs, add the following `IAuthenticate` interface definition immediately before the `App` class definition.</span></span>

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. <span data-ttu-id="3e447-141">Pour initialiser l’interface avec une implémentation propre à la plateforme, ajoutez les membres statiques suivants à la classe **App**.</span><span class="sxs-lookup"><span data-stu-id="3e447-141">To initialize the interface with a platform-specific implementation, add the following static members to the **App** class.</span></span>

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. <span data-ttu-id="3e447-142">Ouvrez TodoList.xaml à partir du projet de bibliothèque de classes portable, ajoutez l’élément **bouton** suivant dans l’élément de disposition *buttonsPanel* , après le bouton existant :</span><span class="sxs-lookup"><span data-stu-id="3e447-142">Open TodoList.xaml from the Portable Class Library project, add the following **Button** element in the *buttonsPanel* layout element, after the existing button:</span></span>

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    <span data-ttu-id="3e447-143">Ce bouton déclenche l’authentification gérée par le serveur auprès du serveur principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="3e447-143">This button triggers server-managed authentication with your mobile app backend.</span></span>
5. <span data-ttu-id="3e447-144">Ouvrez TodoList.xaml.cs à partir du projet de bibliothèque de classes portable, puis ajoutez le champ suivant à la classe `TodoList` :</span><span class="sxs-lookup"><span data-stu-id="3e447-144">Open TodoList.xaml.cs from the Portable Class Library project, then add the following field to the `TodoList` class:</span></span>

        // Track whether the user has authenticated.
        bool authenticated = false;
6. <span data-ttu-id="3e447-145">Remplacez la méthode **OnAppearing** par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="3e447-145">Replace the **OnAppearing** method with the following code:</span></span>

        protected override async void OnAppearing()
        {
            base.OnAppearing();

            // Refresh items only when authenticated.
            if (authenticated == true)
            {
                // Set syncItems to true in order to synchronize the data
                // on startup when running in offline mode.
                await RefreshItems(true, syncItems: false);

                // Hide the Sign-in button.
                this.loginButton.IsVisible = false;
            }
        }

    <span data-ttu-id="3e447-146">Ce code permet de s’assurer que les données seront actualisées par le service seulement une fois que vous vous serez authentifié.</span><span class="sxs-lookup"><span data-stu-id="3e447-146">This code makes sure that data is only refreshed from the service after you have been authenticated.</span></span>
7. <span data-ttu-id="3e447-147">Ajoutez le gestionnaire suivant pour l’événement **Clicked** à la classe **TodoList** :</span><span class="sxs-lookup"><span data-stu-id="3e447-147">Add the following handler for the **Clicked** event to the **TodoList** class:</span></span>

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems to true to synchronize the data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. <span data-ttu-id="3e447-148">Enregistrez vos modifications et régénérez le projet de bibliothèque de classes portable en vérifiant qu’il ne contient aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="3e447-148">Save your changes and rebuild the Portable Class Library project verifying no errors.</span></span>

## <a name="add-authentication-to-the-android-app"></a><span data-ttu-id="3e447-149">Ajout de l'authentification à l'application Android</span><span class="sxs-lookup"><span data-stu-id="3e447-149">Add authentication to the Android app</span></span>
<span data-ttu-id="3e447-150">Cette section montre comment implémenter l’interface **IAuthenticate** dans le projet d’application Android.</span><span class="sxs-lookup"><span data-stu-id="3e447-150">This section shows how to implement the **IAuthenticate** interface in the Android app project.</span></span> <span data-ttu-id="3e447-151">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Android.</span><span class="sxs-lookup"><span data-stu-id="3e447-151">Skip this section if you are not supporting Android devices.</span></span>

1. <span data-ttu-id="3e447-152">Dans Visual Studio ou Xamarin Studio, cliquez avec le bouton droit sur le projet **droid**, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="3e447-152">In Visual Studio or Xamarin Studio, right-click the **droid** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="3e447-153">Appuyez sur F5 pour démarrer le projet dans le débogueur, puis vérifiez qu’une exception non prise en charge avec le code d’état 401 (Unauthorized) est déclenchée après le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-153">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="3e447-154">Ce code 401 se produit car l’accès au serveur principal est limité aux seuls utilisateurs autorisés.</span><span class="sxs-lookup"><span data-stu-id="3e447-154">The 401 code is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="3e447-155">Ouvrez MainActivity.cs dans le projet Android et ajoutez les instructions `using` suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e447-155">Open MainActivity.cs in the Android project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="3e447-156">Mettez à jour la classe **MainActivity** pour implémenter l’interface **IAuthenticate**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-156">Update the **MainActivity** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. <span data-ttu-id="3e447-157">Mettez à jour la classe **MainActivity** en ajoutant un champ **MobileServiceUser** et une méthode **Authenticate** requise par l’interface **IAuthenticate**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-157">Update the **MainActivity** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            AlertDialog.Builder builder = new AlertDialog.Builder(this);
            builder.SetMessage(message);
            builder.SetTitle("Sign-in result");
            builder.Create().Show();

            return success;
        }

    <span data-ttu-id="3e447-158">Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider][7].</span><span class="sxs-lookup"><span data-stu-id="3e447-158">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider][7].</span></span>

6. <span data-ttu-id="3e447-159">Ajoutez le code suivant à l’intérieur du nœud <application> de AndroidManifest.xml :</span><span class="sxs-lookup"><span data-stu-id="3e447-159">Add the following code inside <application> node of AndroidManifest.xml:</span></span>

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

1. <span data-ttu-id="3e447-160">Ajoutez le code suivant à la méthode **OnCreate** de la classe **MainActivity** avant l’appel à `LoadApplication()` :</span><span class="sxs-lookup"><span data-stu-id="3e447-160">Add the following code to the **OnCreate** method of the **MainActivity** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        App.Init((IAuthenticate)this);

    <span data-ttu-id="3e447-161">Ce code permet de garantir que l’authentificateur sera initialisé avant le chargement de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-161">This code ensures the authenticator is initialized before the app loads.</span></span>
2. <span data-ttu-id="3e447-162">Recompilez et exécutez l’application, puis connectez-vous avec le fournisseur d’authentification choisi et vérifiez que vous êtes en mesure d’accéder aux données en tant qu’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="3e447-162">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-the-ios-app"></a><span data-ttu-id="3e447-163">Ajout de l'authentification à l'application iOS</span><span class="sxs-lookup"><span data-stu-id="3e447-163">Add authentication to the iOS app</span></span>
<span data-ttu-id="3e447-164">Cette section montre comment implémenter l’interface **IAuthenticate** dans le projet d’application iOS.</span><span class="sxs-lookup"><span data-stu-id="3e447-164">This section shows how to implement the **IAuthenticate** interface in the iOS app project.</span></span> <span data-ttu-id="3e447-165">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.</span><span class="sxs-lookup"><span data-stu-id="3e447-165">Skip this section if you are not supporting iOS devices.</span></span>

1. <span data-ttu-id="3e447-166">Dans Visual Studio ou Xamarin Studio, cliquez avec le bouton droit sur le projet **iOS**, puis cliquez sur**Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="3e447-166">In Visual Studio or Xamarin Studio, right-click the **iOS** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="3e447-167">Appuyez sur F5 pour démarrer le projet dans le débogueur, puis vérifiez qu’une exception non prise en charge avec le code d’état 401 (Unauthorized) est déclenchée après le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-167">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="3e447-168">Cette réponse 401 se produit car l’accès au serveur principal est limité aux seuls utilisateurs autorisés.</span><span class="sxs-lookup"><span data-stu-id="3e447-168">The 401 response is produced because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="3e447-169">Ouvrez AppDelegate.cs dans le projet iOS et ajoutez les instructions `using` suivantes :</span><span class="sxs-lookup"><span data-stu-id="3e447-169">Open AppDelegate.cs in the iOS project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. <span data-ttu-id="3e447-170">Mettez à jour la classe **AppDelegate** pour implémenter l’interface **IAuthenticate**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-170">Update the **AppDelegate** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. <span data-ttu-id="3e447-171">Mettez à jour la classe **AppDelegate** en ajoutant un champ **MobileServiceUser** et une méthode **Authenticate** requise par l’interface **IAuthenticate**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-171">Update the **AppDelegate** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            UIAlertView avAlert = new UIAlertView("Sign-in result", message, null, "OK", null);
            avAlert.Show();

            return success;
        }

    <span data-ttu-id="3e447-172">Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="3e447-172">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

6. <span data-ttu-id="3e447-173">Mettre à jour la classe AppDelegate en ajoutant la surcharge de méthode OpenUrl(UIApplication app, NSUrl url, NSDictionary options)</span><span class="sxs-lookup"><span data-stu-id="3e447-173">Update the AppDelegate class by adding OpenUrl(UIApplication app, NSUrl url, NSDictionary options) method overload</span></span>

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. <span data-ttu-id="3e447-174">Ajoutez la ligne de code suivante à la méthode **FinishedLaunching** avant l’appel à `LoadApplication()` :</span><span class="sxs-lookup"><span data-stu-id="3e447-174">Add the following line of code to the **FinishedLaunching** method before the call to `LoadApplication()`:</span></span>

        App.Init(this);

    <span data-ttu-id="3e447-175">Ce code permet de garantir que l’authentificateur sera initialisé avant le chargement de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-175">This code ensures the authenticator is initialized before the app is loaded.</span></span>

6. <span data-ttu-id="3e447-176">Ajoutez **{url_scheme_of_your_app}** aux schémas d’URL dans Info.plist.</span><span class="sxs-lookup"><span data-stu-id="3e447-176">Add **{url_scheme_of_your_app}** to URL Schemes in Info.plist.</span></span>

7. <span data-ttu-id="3e447-177">Recompilez et exécutez l’application, puis connectez-vous avec le fournisseur d’authentification choisi et vérifiez que vous êtes en mesure d’accéder aux données en tant qu’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="3e447-177">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="add-authentication-to-windows-10-including-phone-app-projects"></a><span data-ttu-id="3e447-178">Ajout de l’authentification à des projets d’application Windows 10 (y compris Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="3e447-178">Add authentication to Windows 10 (including Phone) app projects</span></span>
<span data-ttu-id="3e447-179">Cette section montre comment implémenter l’interface **IAuthenticate** dans les projets d’application Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3e447-179">This section shows how to implement the **IAuthenticate** interface in the Windows 10 app projects.</span></span> <span data-ttu-id="3e447-180">Les mêmes étapes s’appliquent aux projets de plateforme Windows universelle (UWP), mais en utilisant le projet **UWP** (comportant des modifications indiquées).</span><span class="sxs-lookup"><span data-stu-id="3e447-180">The same steps apply for Universal Windows Platform (UWP) projects, but using the **UWP** project (with noted changes).</span></span> <span data-ttu-id="3e447-181">Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.</span><span class="sxs-lookup"><span data-stu-id="3e447-181">Skip this section if you are not supporting Windows devices.</span></span>

1. <span data-ttu-id="3e447-182">Dans Visual Studio, cliquez avec le bouton droit sur le projet **UWP**, puis cliquez sur **Définir comme projet de démarrage**.</span><span class="sxs-lookup"><span data-stu-id="3e447-182">"In Visual Studio, right-click either the **UWP** project, then **Set as StartUp Project**.</span></span>
2. <span data-ttu-id="3e447-183">Appuyez sur F5 pour démarrer le projet dans le débogueur, puis vérifiez qu’une exception non prise en charge avec le code d’état 401 (Unauthorized) est déclenchée après le démarrage de l’application.</span><span class="sxs-lookup"><span data-stu-id="3e447-183">Press F5 to start the project in the debugger, then verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after the app starts.</span></span> <span data-ttu-id="3e447-184">Cette réponse 401 se produit car l’accès au serveur principal est limité aux seuls utilisateurs autorisés.</span><span class="sxs-lookup"><span data-stu-id="3e447-184">The 401 response happens because access on the backend is restricted to authorized users only.</span></span>
3. <span data-ttu-id="3e447-185">Ouvrez MainPage.xaml.cs dans le projet d’application Windows et ajoutez l’instruction `using` suivante :</span><span class="sxs-lookup"><span data-stu-id="3e447-185">Open MainPage.xaml.cs for the Windows app project and add the following `using` statements:</span></span>

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    <span data-ttu-id="3e447-186">Remplacez `<your_Portable_Class_Library_namespace>` par l’espace de noms de votre bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="3e447-186">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>
4. <span data-ttu-id="3e447-187">Mettez à jour la classe **MainPage** pour implémenter l’interface **IAuthenticate**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-187">Update the **MainPage** class to implement the **IAuthenticate** interface, as follows:</span></span>

        public sealed partial class MainPage : IAuthenticate
5. <span data-ttu-id="3e447-188">Mettez à jour la classe **MainPage** en ajoutant un champ **MobileServiceUser** et une méthode **Authenticate** requise par l’interface **IAuthenticate**, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3e447-188">Update the **MainPage** class by adding a **MobileServiceUser** field and an **Authenticate** method, which is required by the **IAuthenticate** interface, as follows:</span></span>

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

            // Display the success or failure message.
            await new MessageDialog(message, "Sign-in result").ShowAsync();

            return success;
        }

    <span data-ttu-id="3e447-189">Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider].</span><span class="sxs-lookup"><span data-stu-id="3e447-189">If you are using an identity provider other than Facebook, choose a different value for [MobileServiceAuthenticationProvider].</span></span>

1. <span data-ttu-id="3e447-190">Ajoutez la ligne de code suivante dans le constructeur de la classe **MainPage** avant l’appel à `LoadApplication()` :</span><span class="sxs-lookup"><span data-stu-id="3e447-190">Add the following line of code in the constructor for the **MainPage** class before the call to `LoadApplication()`:</span></span>

        // Initialize the authenticator before loading the app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    <span data-ttu-id="3e447-191">Remplacez `<your_Portable_Class_Library_namespace>` par l’espace de noms de votre bibliothèque de classes portable.</span><span class="sxs-lookup"><span data-stu-id="3e447-191">Replace `<your_Portable_Class_Library_namespace>` with the namespace for your portable class library.</span></span>

3. <span data-ttu-id="3e447-192">Si vous utilisez **UWP**, ajoutez la substitution de méthode **OnActivated** suivante à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="3e447-192">If you are using **UWP**, add the following **OnActivated** method override to the **App** class:</span></span>

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   <span data-ttu-id="3e447-193">Si la substitution de méthode existe déjà, ajoutez le code conditionnel à partir de l’extrait de code précédent.</span><span class="sxs-lookup"><span data-stu-id="3e447-193">When the method override already exists, add the conditional code from the preceding snippet.</span></span>  <span data-ttu-id="3e447-194">Ce code n’est pas requis pour les projets Windows universel.</span><span class="sxs-lookup"><span data-stu-id="3e447-194">This code is not required for Universal Windows projects.</span></span>

3. <span data-ttu-id="3e447-195">Ajoutez **{url_scheme_of_your_app}** dans Package.appxmanifest.</span><span class="sxs-lookup"><span data-stu-id="3e447-195">Add **{url_scheme_of_your_app}** in Package.appxmanifest.</span></span> 

4. <span data-ttu-id="3e447-196">Recompilez et exécutez l’application, puis connectez-vous avec le fournisseur d’authentification choisi et vérifiez que vous êtes en mesure d’accéder aux données en tant qu’utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="3e447-196">Rebuild the app, run it, then sign in with the authentication provider you chose and verify you are able to access data as an authenticated user.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e447-197">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3e447-197">Next steps</span></span>
<span data-ttu-id="3e447-198">Maintenant que vous avez terminé ce didacticiel sur l'authentification de base, vous pouvez passer à l'un des didacticiels suivants :</span><span class="sxs-lookup"><span data-stu-id="3e447-198">Now that you completed this basic authentication tutorial, consider continuing on to one of the following tutorials:</span></span>

* [<span data-ttu-id="3e447-199">Ajouter des notifications Push à votre application Android</span><span class="sxs-lookup"><span data-stu-id="3e447-199">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)

  <span data-ttu-id="3e447-200">Apprenez à ajouter la prise en charge des notifications Push à votre application et à configurer le serveur principal d’applications mobiles pour utiliser Azure Notification Hubs afin d’envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="3e447-200">Learn how to add push notifications support to your app and configure your Mobile App backend to use Azure Notification Hubs to send push notifications.</span></span>
* [<span data-ttu-id="3e447-201">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="3e447-201">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  <span data-ttu-id="3e447-202">Apprenez à ajouter une prise en charge hors connexion à votre application à l’aide d’un serveur principal Mobile App.</span><span class="sxs-lookup"><span data-stu-id="3e447-202">Learn how to add offline support your app using a Mobile App backend.</span></span> <span data-ttu-id="3e447-203">La synchronisation hors connexion permet aux utilisateurs finaux d’interagir avec une application mobile pour afficher, ajouter ou modifier des données, même lorsqu’il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="3e447-203">Offline sync allows end users to interact with a mobile app - viewing, adding, or modifying data - even when there is no network connection.</span></span>

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
