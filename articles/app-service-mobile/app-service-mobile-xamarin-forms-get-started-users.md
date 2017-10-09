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
# <a name="add-authentication-tooyour-xamarin-forms-app"></a>Ajouter une application de Xamarin Forms tooyour d’authentification
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment les utilisateurs de tooauthenticate d’une application Service d’applications mobiles à partir de votre application cliente. Dans ce didacticiel, vous ajoutez l’authentification au projet de démarrage rapide de Xamarin Forms hello à l’aide d’un fournisseur d’identité qui est pris en charge par le Service d’applications. Une fois en cours a été authentifié et autorisé par votre application Mobile, la valeur d’ID utilisateur hello s’affiche, et vous serez en mesure de tooaccess restreint les données de table.

## <a name="prerequisites"></a>Composants requis
Pour un résultat optimal de hello avec ce didacticiel, nous vous recommandons d’effectuer tout d’abord hello [créer une application Xamarin Forms] [ 1] didacticiel. Après avoir terminé ce didacticiel, vous disposerez d’un projet Xamarin Forms qui est une application TodoList multiplateforme.

Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter le projet tooyour de package d’extension d’authentification de hello. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure][2].

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Inscription de votre application pour l'authentification et configuration d'App Services
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application

L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application. Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée. Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble. Toutefois, vous pouvez utiliser le schéma d’URL de votre choix. Il doit être unique tooyour des applications mobiles. redirection de hello tooenable côté serveur de hello :

1. Bonjour [Azure portal], sélectionnez votre application de Service.

2. Cliquez sur hello **l’authentification / autorisation** option de menu.

3. Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.  Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).  Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.

4. Cliquez sur **OK**.

5. Cliquez sur **Enregistrer**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Restreindre les autorisations des utilisateurs tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

## <a name="add-authentication-toohello-portable-class-library"></a>Ajout d’une bibliothèque de classes portable toohello d’authentification
Applications mobiles utilise hello [LoginAsync] [ 3] méthode d’extension sur hello [MobileServiceClient] [ 4] toosign un utilisateur avec le Service d’applications authentification. Cet exemple utilise un flux d’authentification de serveur géré qui affiche l’interface de connexion du fournisseur hello dans l’application hello. Pour plus d’informations, voir la rubrique [Authentification gérée par le serveur][5]. Pour offrir une meilleure expérience utilisateur dans votre application de production, vous devez plutôt envisager d’utiliser une [authentification gérée par le client][6].

tooauthenticate avec un projet Xamarin Forms, définir un **IAuthenticate** interface Bonjour bibliothèque de classes Portable pour une application hello. Ajoutez ensuite une **connectez-vous** défini dans hello bibliothèque de classes portables, ce qui vous cliquez sur l’interface utilisateur toohello bouton toostart authentification. Après une authentification réussie, les données sont chargées à partir du serveur principal d’application mobile hello.

Hello d’implémenter **IAuthenticate** interface pour chaque plateforme prise en charge par votre application.

1. Dans Visual Studio ou Xamarin Studio, ouvrez App.cs du projet hello avec **Portable** dans nom hello, qui est un projet de bibliothèque de classes portables, puis ajoutez hello suivant `using` instruction :

        using System.Threading.Tasks;
2. Dans App.cs, ajoutez hello qui suit `IAuthenticate` définition immédiatement avant hello d’interface `App` définition de classe.

        public interface IAuthenticate
        {
            Task<bool> Authenticate();
        }
3. interface de hello tooinitialize avec une implémentation spécifique à la plateforme, ajouter hello suivant des membres statiques toohello **application** classe.

        public static IAuthenticate Authenticator { get; private set; }

        public static void Init(IAuthenticate authenticator)
        {
            Authenticator = authenticator;
        }
4. Ouvrez TodoList.xaml à partir du projet de bibliothèque de classes portables hello, ajoutez hello **bouton** élément Bonjour *buttonsPanel* layout (élément), après le bouton hello :

          <Button x:Name="loginButton" Text="Sign-in" MinimumHeightRequest="30"
            Clicked="loginButton_Clicked"/>

    Ce bouton déclenche l’authentification gérée par le serveur auprès du serveur principal de votre application mobile.
5. Ouvrez TodoList.xaml.cs à partir du projet de bibliothèque de classes portables hello, puis ajoutez les hello suivant champ toohello `TodoList` classe :

        // Track whether hello user has authenticated.
        bool authenticated = false;
6. Remplacez hello **OnAppearing** méthode avec hello suivant de code :

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

    Ce code permet de s’assurer que les données sont uniquement actualisées à partir du service de hello une fois que vous avez été authentifié.
7. Ajouter hello suivant gestionnaire pour hello **Clicked** événement toohello **TodoList** classe :

        async void loginButton_Clicked(object sender, EventArgs e)
        {
            if (App.Authenticator != null)
                authenticated = await App.Authenticator.Authenticate();

            // Set syncItems tootrue toosynchronize hello data on startup when offline is enabled.
            if (authenticated == true)
                await RefreshItems(true, syncItems: false);
        }
8. Enregistrez vos modifications et régénérer le projet de bibliothèque de classes portables hello vérification sans erreurs.

## <a name="add-authentication-toohello-android-app"></a>Ajouter une application Android de l’authentification toohello
Cette section montre comment tooimplement hello **IAuthenticate** interface dans un projet d’application Android hello. Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Android.

1. Dans Visual Studio ou Xamarin Studio, avec le bouton droit hello **droid** de projet, puis **définir comme projet de démarrage**.
2. Hello de toostart appuyez sur F5 dans le débogueur de hello du projet, puis vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application. code de 401 Hello se produit car l’accès sur les principaux hello est utilisateurs tooauthorized restreint uniquement.
3. Ouvrez MainActivity.cs dans les projets Android hello et ajoutez hello suit `using` instructions :

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Hello de mise à jour **MainActivity** hello tooimplement de classe **IAuthenticate** d’interface, comme suit :

        public class MainActivity : global::Xamarin.Forms.Platform.Android.FormsApplicationActivity, IAuthenticate
5. Hello de mise à jour **MainActivity** classe en ajoutant une **MobileServiceUser** champ et un **authentifier** (méthode), ce qui est requis par hello **IAuthenticate**  d’interface, comme suit :

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

    Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider][7].

6. Ajouter hello suivant du code à l’intérieur <application> nœud de AndroidManifest.xml :

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

1. Ajouter hello suivant code toohello **OnCreate** méthode Hello **MainActivity** trop de classe avant l’appel de hello`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        App.Init((IAuthenticate)this);

    Ce code garantit l’authentificateur de hello est initialisée avant application hello charge.
2. Régénérer l’application hello, exécutez-le, puis connectez-vous avec le fournisseur d’authentification hello vous avez choisi et vérifiez que vous tooaccess en mesure des données sous la forme d’un utilisateur authentifié.

## <a name="add-authentication-toohello-ios-app"></a>Ajouter une application de l’authentification toohello iOS
Cette section montre comment tooimplement hello **IAuthenticate** interface dans un projet d’application iOS hello. Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils iOS.

1. Dans Visual Studio ou Xamarin Studio, avec le bouton droit hello **iOS** de projet, puis **définir comme projet de démarrage**.
2. Hello de toostart appuyez sur F5 dans le débogueur de hello du projet, puis vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello. les réponses 401 Hello se produit car l’accès sur les principaux hello est utilisateurs tooauthorized restreint uniquement.
3. Ouvrez AppDelegate.cs dans projet iOS, hello et ajoutez hello suit `using` instructions :

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
4. Hello de mise à jour **AppDelegate** hello tooimplement de classe **IAuthenticate** d’interface, comme suit :

        public partial class AppDelegate : global::Xamarin.Forms.Platform.iOS.FormsApplicationDelegate, IAuthenticate
5. Hello de mise à jour **AppDelegate** classe en ajoutant une **MobileServiceUser** champ et un **authentifier** (méthode), ce qui est requis par hello **IAuthenticate**  d’interface, comme suit :

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

    Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider].

6. Mettre à jour de la classe de AppDelegate hello en ajoutant la surcharge de méthode OpenUrl (options du NSDictionary application, les url NSUrl, UIApplication)

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(url);
        }

6. Ajouter hello suivant la ligne de code toohello **FinishedLaunching** méthode hello avant d’appeler trop`LoadApplication()`:

        App.Init(this);

    Ce code garantit l’authentificateur de hello est initialisée avant l’application hello est chargée.

6. Ajouter **{url_scheme_of_your_app}** tooURL des schémas dans le fichier Info.plist.

7. Régénérer l’application hello, exécutez-le, puis connectez-vous avec le fournisseur d’authentification hello vous avez choisi et vérifiez que vous tooaccess en mesure des données sous la forme d’un utilisateur authentifié.

## <a name="add-authentication-toowindows-10-including-phone-app-projects"></a>Ajouter l’authentification tooWindows 10 (y compris téléphone) projets d’application
Cette section montre comment tooimplement hello **IAuthenticate** interface dans les projets d’application hello Windows 10. Hello mêmes étapes s’appliquent aux projets de plateforme Windows universelle (UWP), mais à l’aide de hello **UWP** projet (avec les modifications indiquées). Vous pouvez ignorer cette section si vous n’utilisez pas d’appareils Windows.

1. « Dans Visual Studio, avec le bouton droit soit hello **UWP** de projet, puis **définir comme projet de démarrage**.
2. Hello de toostart appuyez sur F5 dans le débogueur de hello du projet, puis vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello. les réponses 401 Hello se produit car l’accès sur les principaux hello est utilisateurs tooauthorized restreint uniquement.
3. Ouvrez MainPage.xaml.cs pour le projet d’application Windows hello et ajoutez hello suit `using` instructions :

        using Microsoft.WindowsAzure.MobileServices;
        using System.Threading.Tasks;
        using Windows.UI.Popups;
        using <your_Portable_Class_Library_namespace>;

    Remplacez `<your_Portable_Class_Library_namespace>` avec l’espace de noms hello pour votre bibliothèque de classes portable.
4. Hello de mise à jour **MainPage** hello tooimplement de classe **IAuthenticate** d’interface, comme suit :

        public sealed partial class MainPage : IAuthenticate
5. Hello de mise à jour **MainPage** classe en ajoutant une **MobileServiceUser** champ et un **authentifier** (méthode), ce qui est requis par hello **IAuthenticate** de l’interface, comme suit :

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

    Si vous utilisez un fournisseur d’identité différent de Facebook, choisissez une autre valeur pour [MobileServiceAuthenticationProvider].

1. Ajouter hello suivant la ligne de code dans le constructeur hello pour hello **MainPage** trop de classe avant l’appel de hello`LoadApplication()`:

        // Initialize hello authenticator before loading hello app.
        <your_Portable_Class_Library_namespace>.App.Init(this);

    Remplacez `<your_Portable_Class_Library_namespace>` avec l’espace de noms hello pour votre bibliothèque de classes portable.

3. Si vous utilisez **UWP**, ajoutez hello suivant **OnActivated** toohello de substitution de méthode **application** classe :

       protected override void OnActivated(IActivatedEventArgs args)
       {
           base.OnActivated(args);

            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                TodoItemManager.DefaultManager.CurrentClient.ResumeWithURL(protocolArgs.Uri);
            }

       }

   Lors de la substitution de méthode hello existe déjà, ajoutez le code de conditionnelle de hello de hello précédant l’extrait de code.  Ce code n’est pas requis pour les projets Windows universel.

3. Ajoutez **{url_scheme_of_your_app}** dans Package.appxmanifest. 

4. Régénérer l’application hello, exécutez-le, puis connectez-vous avec le fournisseur d’authentification hello vous avez choisi et vérifiez que vous tooaccess en mesure des données sous la forme d’un utilisateur authentifié.

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous terminé ce didacticiel de l’authentification de base, pensez à poursuivre sur tooone Hello suivant didacticiels :

* [Ajouter une application de tooyour de notifications push](app-service-mobile-xamarin-forms-get-started-push.md)

  Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer votre application Mobile back-end toouse Azure Notification Hubs toosend les notifications de transmission.
* [Activer la synchronisation hors connexion pour votre application](app-service-mobile-xamarin-forms-get-started-offline-data.md)

  Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un service principal de l’application Mobile. Synchronisation hors connexion permet de toointeract des utilisateurs finaux avec une application mobile - affichage, l’ajout ou la modification de données - même quand il n’existe aucune connexion réseau.

<!-- Images. -->

<!-- URLs. -->
[1]: app-service-mobile-xamarin-forms-get-started.md
[2]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[3]: https://msdn.microsoft.com/library/azure/dn268341(v=azure.10).aspx
[4]: https://msdn.microsoft.com/library/azure/JJ553674(v=azure.10).aspx
[5]: app-service-mobile-dotnet-how-to-use-client-library.md#serverflow
[6]: app-service-mobile-dotnet-how-to-use-client-library.md#clientflow
[7]: https://msdn.microsoft.com/library/azure/jj730936(v=azure.10).aspx
