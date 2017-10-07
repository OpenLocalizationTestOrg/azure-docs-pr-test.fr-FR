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
# <a name="add-authentication-tooyour-xamarinandroid-app"></a>Ajouter une application de Xamarin.Android tooyour d’authentification
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Cette rubrique vous montre comment les utilisateurs de tooauthenticate d’une application Mobile à partir de votre application cliente. Dans ce didacticiel, vous ajoutez des projets de démarrage rapide de toohello d’authentification à l’aide d’un fournisseur d’identité qui est pris en charge par les applications mobiles Azure. Après avoir en cours a été authentifié et autorisé Bonjour application Mobile, la valeur d’ID utilisateur hello s’affiche.

Ce didacticiel est basé sur le démarrage rapide de l’application Mobile hello. Vous devez également effectuer les didacticiel hello [créer une application de Xamarin.Android]. Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez ajouter le projet tooyour de package d’extension d’authentification de hello. Pour plus d’informations sur les packages d’extension de serveur, consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md).

## <a name="register"></a>Inscription de votre application pour l’authentification et configuration d’App Services
[!INCLUDE [app-service-mobile-register-authentication](../../includes/app-service-mobile-register-authentication.md)]

## <a name="redirecturl"></a>Ajouter votre URL de redirection externe d’autorisé toohello application

L’authentification sécurisée nécessite de définir un nouveau schéma d’URL pour votre application. Cela permet de hello authentification système tooredirect tooyour arrière application une fois le processus d’authentification hello est terminée. Dans ce didacticiel, nous utilisons le modèle d’URL hello _appname_ dans l’ensemble. Toutefois, vous pouvez utiliser le schéma d’URL de votre choix. Il doit être unique tooyour des applications mobiles. redirection de hello tooenable côté serveur de hello :

1. Bonjour [Azure portal], sélectionnez votre application de Service.

2. Cliquez sur hello **l’authentification / autorisation** option de menu.

3. Bonjour **autorisé des URL de redirection externe**, entrez `url_scheme_of_your_app://easyauth.callback`.  Hello **url_scheme_of_your_app** de cette chaîne est hello le modèle d’URL pour votre application mobile.  Elle doit être conforme à la spécification d’URL normale pour un protocole (utiliser des lettres et des chiffres uniquement et commencer par une lettre).  Vous devez vous note de la chaîne hello que vous choisissez car vous en aurez besoin tooadjust votre code d’application mobile avec hello modèle d’URL à plusieurs endroits.

4. Cliquez sur **OK**.

5. Cliquez sur **Enregistrer**.

## <a name="permissions"></a>Restreindre les autorisations des utilisateurs tooauthenticated
[!INCLUDE [app-service-mobile-restrict-permissions-dotnet-backend](../../includes/app-service-mobile-restrict-permissions-dotnet-backend.md)]

Dans Visual Studio ou Xamarin Studio, exécutez le projet de client de hello sur un périphérique ou un émulateur. Vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello. Cela se produit, car l’application hello tente tooaccess service principal de votre application Mobile comme un utilisateur non authentifié. Hello *TodoItem* table requiert l’authentification.

Ensuite, vous mettrez à jour des ressources de toorequest application hello client à partir du serveur principal de l’application Mobile hello avec un utilisateur authentifié.

## <a name="add-authentication"></a>Ajouter une application de toohello d’authentification
application Hello est hello de toorequire mis à jour les utilisateurs tootap **connectez-vous** bouton et authentifier avant que les données sont affichées.

1. Ajouter hello suivant code toohello **TodoActivity** classe :
   
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
   
    Cela crée un nouveau tooauthenticate de méthode à un utilisateur et un gestionnaire de méthode pour un nouveau **connectez-vous** bouton. utilisateur Hello hello exemple de code ci-dessus est authentifié à l’aide d’une connexion Facebook. Une boîte de dialogue est l’ID d’utilisateur hello toodisplay utilisés une fois authentifié.
   
   > [!NOTE]
   > Si vous utilisez un fournisseur d’identité autre que Facebook, modifiez la valeur hello passé trop**LoginAsync** ci-dessus tooone suivants de hello : *MicrosoftAccount*, *Twitter*, *Google*, ou *WindowsAzureActiveDirectory*.
   > 
   > 
2. Bonjour **OnCreate** (méthode), delete ou hello Commentez la ligne de code suivante :
   
        OnRefreshItemsSelected ();
3. Dans le fichier de Activity_To_Do.axml hello, ajoutez hello qui suit *LoginUser* bouton définition avant hello existant *AddItem* bouton :
   
          <Button
            android:id="@+id/buttonLoginUser"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:onClick="LoginUser"
            android:text="@string/login_button_text" />
4. Ajoutez hello élément toohello Strings.xml ressources fichier suivant :
   
        <string name="login_button_text">Sign in</string>
5. Ouvrez le fichier AndroidManifest.xml hello, ajouter hello suivant du code à l’intérieur `<application>` élément XML :

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity" android:launchMode="singleTop" android:noHistory="true">
          <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback" />
          </intent-filter>
        </activity>

6. Dans Visual Studio ou Xamarin Studio, exécutez le projet de client de hello sur un périphérique ou un émulateur et connectez-vous avec votre fournisseur d’identité choisi. Lorsque vous êtes correctement connecté en, application hello affiche votre ID de connexion et hello liste des éléments de tâche, vous pouvez rendre les données de toohello de mises à jour.

<!-- URLs. -->
[créer une application de Xamarin.Android]: app-service-mobile-xamarin-android-get-started.md