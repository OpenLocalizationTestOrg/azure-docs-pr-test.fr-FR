---
title: "aaaGet démarré avec une authentification pour les applications mobiles dans Xamarin Android"
description: "Découvrez comment toouse Mobile Apps tooauthenticate les utilisateurs de votre application Xamarin Android via une variété de fournisseurs d’identité, notamment AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 570fc12b-46a9-4722-b2e0-0d1c45fb2152
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: 500a4efa816e4f6d75d359e31d6357da56a72f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-xamarinandroid-app"></a><span data-ttu-id="5668b-103">Ajouter une application de Xamarin.Android tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="5668b-103">Add authentication tooyour Xamarin.Android app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

<span data-ttu-id="5668b-104">Cette rubrique vous montre comment les utilisateurs de tooauthenticate d’une application Mobile à partir de votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="5668b-104">This topic shows you how tooauthenticate users of a Mobile App from your client application.</span></span> <span data-ttu-id="5668b-105">Dans ce didacticiel, vous ajoutez des projets de démarrage rapide de toohello d’authentification à l’aide d’un fournisseur d’identité qui est pris en charge par les applications mobiles Azure.</span><span class="sxs-lookup"><span data-stu-id="5668b-105">In this tutorial, you add authentication toohello quickstart project using an identity provider that is supported by Azure Mobile Apps.</span></span> <span data-ttu-id="5668b-106">Après avoir en cours a été authentifié et autorisé Bonjour application Mobile, la valeur d’ID utilisateur hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="5668b-106">After being successfully authenticated and authorized in hello Mobile App, hello user ID value is displayed.</span></span>

<span data-ttu-id="5668b-107">Ce didacticiel est basé sur le démarrage rapide de l’application Mobile hello.</span><span class="sxs-lookup"><span data-stu-id="5668b-107">This tutorial is based on hello Mobile App quickstart.</span></span> <span data-ttu-id="5668b-108">Vous devez également effectuer les didacticiel hello [créer une application de Xamarin.Android].</span><span class="sxs-lookup"><span data-stu-id="5668b-108">You must also first complete hello tutorial [Create a Xamarin.Android app].</span></span> <span data-ttu-id="5668b-109">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter le projet tooyour de package d’extension d’authentification de hello.</span><span class="sxs-lookup"><span data-stu-id="5668b-109">If you do not use hello downloaded quick start server project, you must add hello authentication extension package tooyour project.</span></span> <span data-ttu-id="5668b-110">Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="5668b-110">For more information about server extension packages, see [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).</span></span>

## <span data-ttu-id="5668b-111"><a name="register"></a>Inscription de votre application pour l’authentification et configuration d’App Services</span><span class="sxs-lookup"><span data-stu-id="5668b-111"><a name="register"></a>Register your app for authentication and configure App Services</span></span>
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <span data-ttu-id="5668b-112"><a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application</span><span class="sxs-lookup"><span data-stu-id="5668b-112"><a name="redirecturl"></a>Add your app toohello Allowed External Redirect URLs</span></span>

<span data-ttu-id="5668b-113">L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application.</span><span class="sxs-lookup"><span data-stu-id="5668b-113">Secure authentication requires that you define a new URL scheme for your app.</span></span> <span data-ttu-id="5668b-114">Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="5668b-114">This allows hello authentication system tooredirect back tooyour app once hello authentication process is complete.</span></span> <span data-ttu-id="5668b-115">Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble.</span><span class="sxs-lookup"><span data-stu-id="5668b-115">In this tutorial, we use hello URL scheme _appname_ throughout.</span></span> <span data-ttu-id="5668b-116">Toutefois, vous pouvez utiliser le schéma d’URL de votre choix.</span><span class="sxs-lookup"><span data-stu-id="5668b-116">However, you can use any URL scheme you choose.</span></span> <span data-ttu-id="5668b-117">Il doit être unique tooyour des applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="5668b-117">It should be unique tooyour mobile application.</span></span> <span data-ttu-id="5668b-118">redirection de hello tooenable côté serveur de hello :</span><span class="sxs-lookup"><span data-stu-id="5668b-118">tooenable hello redirection on hello server side:</span></span>

1. <span data-ttu-id="5668b-119">Bonjour [Azure portal], sélectionnez votre application de Service.</span><span class="sxs-lookup"><span data-stu-id="5668b-119">In hello [Azure portal], select your App Service.</span></span>

2. <span data-ttu-id="5668b-120">Cliquez sur hello **l’authentification / autorisation** option de menu.</span><span class="sxs-lookup"><span data-stu-id="5668b-120">Click hello **Authentication / Authorization** menu option.</span></span>

3. <span data-ttu-id="5668b-121">Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.</span><span class="sxs-lookup"><span data-stu-id="5668b-121">In hello **Allowed External Redirect URLs**, enter `url_scheme_of_your_app://easyauth.callback`.</span></span>  <span data-ttu-id="5668b-122">Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="5668b-122">hello **url_scheme_of_your_app** in this string is hello URL Scheme for your mobile application.</span></span>  <span data-ttu-id="5668b-123">Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).</span><span class="sxs-lookup"><span data-stu-id="5668b-123">It should follow normal URL specification for a protocol (use letters and numbers only, and start with a letter).</span></span>  <span data-ttu-id="5668b-124">Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.</span><span class="sxs-lookup"><span data-stu-id="5668b-124">You should make a note of hello string that you choose as you will need tooadjust your mobile application code with hello URL Scheme in several places.</span></span>

4. <span data-ttu-id="5668b-125">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="5668b-125">Click **OK**.</span></span>

5. <span data-ttu-id="5668b-126">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="5668b-126">Click **Save**.</span></span>

## <span data-ttu-id="5668b-127"><a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated</span><span class="sxs-lookup"><span data-stu-id="5668b-127"><a name="permissions"></a>Restrict permissions tooauthenticated users</span></span>
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

<span data-ttu-id="5668b-128">Dans Visual Studio ou Xamarin Studio, exécutez le projet de client de hello sur un périphérique ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="5668b-128">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator.</span></span> <span data-ttu-id="5668b-129">Vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="5668b-129">Verify that an unhandled exception with a status code of 401 (Unauthorized) is raised after hello app starts.</span></span> <span data-ttu-id="5668b-130">Cela se produit, car l’application hello tente tooaccess service principal de votre application Mobile comme un utilisateur non authentifié.</span><span class="sxs-lookup"><span data-stu-id="5668b-130">This happens because hello app attempts tooaccess your Mobile App backend as an unauthenticated user.</span></span> <span data-ttu-id="5668b-131">Hello *TodoItem* table requiert l’authentification.</span><span class="sxs-lookup"><span data-stu-id="5668b-131">hello *TodoItem* table now requires authentication.</span></span>

<span data-ttu-id="5668b-132">Ensuite, vous mettrez à jour des ressources de toorequest application hello client à partir du serveur principal de l’application Mobile hello avec un utilisateur authentifié.</span><span class="sxs-lookup"><span data-stu-id="5668b-132">Next, you will update hello client app toorequest resources from hello Mobile App backend with an authenticated user.</span></span>

## <span data-ttu-id="5668b-133"><a name="add-authentication"></a>Ajouter une application de toohello d’authentification</span><span class="sxs-lookup"><span data-stu-id="5668b-133"><a name="add-authentication"></a>Add authentication toohello app</span></span>
<span data-ttu-id="5668b-134">application Hello est hello de toorequire mis à jour les utilisateurs tootap **connectez-vous** bouton et authentifier avant que les données sont affichées.</span><span class="sxs-lookup"><span data-stu-id="5668b-134">hello app is updated toorequire users tootap hello **Sign in** button and authenticate before data is displayed.</span></span>

1. <span data-ttu-id="5668b-135">Ajouter hello suivant code toohello **TodoActivity** classe :</span><span class="sxs-lookup"><span data-stu-id="5668b-135">Add hello following code toohello **TodoActivity** class:</span></span>
   
        // Define a authenticated user.
        private MobileServiceUser user;
        private async Task<bool> Authenticate()
        {
                var success = false;
                try
                {
                    // Sign in with Facebook login using a server-managed flow.
                    user = await client.LoginAsync(this,
                        MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                    CreateAndShowDialog(string.Format("you are now logged in - {0}",
                        user.UserId), "Logged in!");
   
                    success = true;
                }
                catch (Exception ex)
                {
                    CreateAndShowDialog(ex, "Authentication failed");
                }
                return success;
        }
   
        [Java.Interop.Export()]
        public async void LoginUser(View view)
        {
            // Load data only after authentication succeeds.
            if (await Authenticate())
            {
                //Hide hello button after authentication succeeds.
                FindViewById<Button>(Resource.Id.buttonLoginUser).Visibility = ViewStates.Gone;
   
                // Load hello data.
                OnRefreshItemsSelected();
            }
        }
   
    <span data-ttu-id="5668b-136">Cela crée un nouveau tooauthenticate de méthode à un utilisateur et un gestionnaire de méthode pour un nouveau **connectez-vous** bouton.</span><span class="sxs-lookup"><span data-stu-id="5668b-136">This creates a new method tooauthenticate a user and a method handler for a new **Sign in** button.</span></span> <span data-ttu-id="5668b-137">utilisateur Hello hello exemple de code ci-dessus est authentifié à l’aide d’une connexion Facebook.</span><span class="sxs-lookup"><span data-stu-id="5668b-137">hello user in hello example code above is authenticated by using a Facebook login.</span></span> <span data-ttu-id="5668b-138">Une boîte de dialogue est l’ID d’utilisateur hello toodisplay utilisés une fois authentifié.</span><span class="sxs-lookup"><span data-stu-id="5668b-138">A dialog is used toodisplay hello user ID once authenticated.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5668b-139">Si vous utilisez un fournisseur d’identité autre que Facebook, modifiez la valeur hello passé trop**LoginAsync** ci-dessus tooone suivants de hello : *MicrosoftAccount*, *Twitter*, *Google*, ou *WindowsAzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="5668b-139">If you are using an identity provider other than Facebook, change hello value passed too**LoginAsync** above tooone of hello following: *MicrosoftAccount*, *Twitter*, *Google*, or *WindowsAzureActiveDirectory*.</span></span>
   > 
   > 
2. <span data-ttu-id="5668b-140">Bonjour **OnCreate** (méthode), delete ou hello Commentez la ligne de code suivante :</span><span class="sxs-lookup"><span data-stu-id="5668b-140">In hello **OnCreate** method, delete or comment-out hello following line of code:</span></span>
   
        OnRefreshItemsSelected ();
3. <span data-ttu-id="5668b-141">Dans le fichier de Activity_To_Do.axml hello, ajoutez hello qui suit *LoginUser* bouton définition avant hello existant *AddItem* bouton :</span><span class="sxs-lookup"><span data-stu-id="5668b-141">In hello Activity_To_Do.axml file, add hello following *LoginUser* button definition before hello existing *AddItem* button:</span></span>
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. <span data-ttu-id="5668b-142">Ajoutez hello élément toohello Strings.xml ressources fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="5668b-142">Add hello following element toohello Strings.xml resources file:</span></span>
   
        <string name="login_button_text">Sign in</string>
5. <span data-ttu-id="5668b-143">Ouvrez le fichier AndroidManifest.xml hello, ajouter hello suivant du code à l’intérieur `<application>` élément XML :</span><span class="sxs-lookup"><span data-stu-id="5668b-143">Open hello AndroidManifest.xml file, add hello following code inside `<application>` XML element:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. <span data-ttu-id="5668b-144">Dans Visual Studio ou Xamarin Studio, exécutez le projet de client de hello sur un périphérique ou un émulateur et connectez-vous avec votre fournisseur d’identité choisi.</span><span class="sxs-lookup"><span data-stu-id="5668b-144">In Visual Studio or Xamarin Studio, run hello client project on a device or emulator and sign in with your chosen identity provider.</span></span> <span data-ttu-id="5668b-145">Lorsque vous êtes correctement connecté en, application hello affiche votre ID de connexion et hello liste des éléments de tâche, vous pouvez rendre les données de toohello de mises à jour.</span><span class="sxs-lookup"><span data-stu-id="5668b-145">When you are successfully logged-in, hello app will display your login ID and hello list of todo items, and you can make updates toohello data.</span></span>

<!-- URLs. -->
[créer une application de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md