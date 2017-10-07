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
# <a name="add-authentication-tooyour-xamarinios-app"></a>Ajouter une application de l’authentification tooyour Xamarin.iOS
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Cette rubrique vous montre comment les utilisateurs de tooauthenticate d’une application Service d’applications mobiles à partir de votre application cliente. Dans ce didacticiel, vous ajoutez de projet de démarrage rapide d’authentification toohello Xamarin.iOS à l’aide d’un fournisseur d’identité qui est pris en charge par le Service d’applications. Une fois en cours a été authentifié et autorisé par votre application Mobile, la valeur d’ID utilisateur hello s’affiche et vous serez en mesure de tooaccess restreint les données de table.

Vous devez d’abord terminer le didacticiel de hello [créer une application Xamarin.iOS]. Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter le projet tooyour de package d’extension d’authentification de hello. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register-your-app-for-authentication-and-configure-app-services"></a>Inscription de votre application pour l'authentification et configuration d'App Services
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="add-your-app-toohello-allowed-external-redirect-urls"></a>Ajouter votre URL de redirection externe d’autorisé toohello application

L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application. Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée. Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble. Toutefois, vous pouvez utiliser le schéma d’URL de votre choix. Il doit être unique tooyour des applications mobiles. redirection de hello tooenable côté serveur de hello :

1. Bonjour [Azure portal], sélectionnez votre application de Service.

2. Cliquez sur hello **l’authentification / autorisation** option de menu.

3. Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.  Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).  Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.

4. Cliquez sur **OK**.

5. Cliquez sur **Enregistrer**.

## <a name="restrict-permissions-tooauthenticated-users"></a>Restreindre les autorisations des utilisateurs tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

&nbsp;&nbsp;4. Dans Visual Studio ou Xamarin Studio, exécutez le projet de client de hello sur un périphérique ou un émulateur. Vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello. Échec de Hello est console connecté toohello du débogueur de hello. Par conséquent, dans Visual Studio, vous devez voir un échec hello dans la fenêtre de sortie hello.

&nbsp;&nbsp;Cet échec non autorisé se produit, car l’application hello tente tooaccess service principal de votre application Mobile comme un utilisateur non authentifié. Hello *TodoItem* table requiert l’authentification.

Ensuite, vous mettrez à jour des ressources de toorequest application hello client à partir du serveur principal de l’application Mobile hello avec un utilisateur authentifié.

## <a name="add-authentication-toohello-app"></a>Ajouter une application de toohello d’authentification
Dans cette section, vous allez modifier hello application toodisplay un écran de connexion avant d’afficher des données. Au démarrage de l’application hello, il se connecte pas pas tooyour du Service d’applications et n’affichera pas les données. Après hello première hello effectuées par l’utilisateur hello actualisation mouvement, écran de connexion hello s’affiche. après l’ouverture de session réussie hello liste des éléments de tâche s’affiche.

1. Dans le projet de client hello, ouvrez le fichier de hello **QSTodoService.cs** et ajoutez hello qui suit à l’aide d’instruction et `MobileServiceUser` avec un accesseur toohello QSTodoService classe :
 
        using UIKit;
       
        // Logged in user
        private MobileServiceUser user;
        public MobileServiceUser User { get { return user; } }
2. Ajouter la nouvelle méthode nommée **authentifier** trop**QSTodoService** avec hello définition :

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

    >[AZURE.NOTE] Si vous utilisez un fournisseur d’identité autre qu’un Facebook, modifiez la valeur hello passé trop**LoginAsync** ci-dessus tooone suivants de hello : _MicrosoftAccount_, _Twitter_, _Google_, ou _WindowsAzureActiveDirectory_.

3. Ouvrez **QSTodoListViewController.cs**. Modifier la définition de méthode hello de **ViewDidLoad** suppression trop d’appels de hello**RefreshAsync()** près de fin de hello :
   
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
4. Modifier la méthode hello **RefreshAsync** tooauthenticate si hello **utilisateur** propriété a la valeur null. Ajoutez hello suivant code haut hello de définition de méthode hello :
   
        // start of RefreshAsync method
        if (todoService.User == null) {
            await QSTodoService.DefaultService.Authenticate(this);
            if (todoService.User == null) {
                Console.WriteLine("couldn't login!!");
                return;
            }
        }
        // rest of RefreshAsync method
5. Ouvrez **AppDelegate.cs**, ajouter hello suivant de méthode :

        public static Func<NSUrl, bool> ResumeWithURL;

        public override bool OpenUrl(UIApplication app, NSUrl url, NSDictionary options)
        {
            return ResumeWithURL != null && ResumeWithURL(url);
        }
6. Ouvrez **Info.plist** de fichiers, accédez trop**Types d’URL** Bonjour **avancé** section. À présent configurer hello **identificateur** et hello **schémas d’URL** de votre Type d’URL et un clic **ajouter un Type URL**. **Schémas d’URL** doit être le même hello en tant que votre {url_scheme_of_your_app}.
7. Dans Visual Studio ou Xamarin Studio connecté tooyour hôte de Build Xamarin sur votre Mac, exécutez projet de client hello ciblant un périphérique ou un émulateur. Vérifiez que cette application hello n’affiche aucune donnée.
   
    Effectuer des mouvements d’actualisation hello en les extrayant hello liste déroulante d’éléments, ce qui provoque l’hello connexion écran tooappear. Une fois que vous avez correctement entré les informations d’identification valides, application hello affiche liste hello des éléments de tâche, et vous pouvez apporter des mises à jour toohello données.

<!-- URLs. -->
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[créer une application Xamarin.iOS]: app-service-mobile-xamarin-ios-get-started.md