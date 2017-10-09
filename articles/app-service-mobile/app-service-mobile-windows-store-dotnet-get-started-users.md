---
title: application de plateforme Windows universelle (UWP) aaaAdd authentication tooyour | Documents Microsoft
description: "Découvrez comment toouse Azure App Service Mobile Apps tooauthenticate les utilisateurs de votre application de plateforme Windows universelle (UWP) à l’aide de divers modules fournisseurs d’identité, y compris : AAD, Google, Facebook, Twitter et Microsoft."
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: panarasi
editor: 
ms.assetid: 6cffd951-893e-4ce5-97ac-86e3f5ad9466
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 07/05/2017
ms.author: panarasi
ms.openlocfilehash: ad4477e9509f1c40c33e71818e268f6857fe1e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-authentication-tooyour-windows-app"></a>Ajouter l’application Windows authentification tooyour
[!INCLUDE [app-service-mobile-selector-get-started-users](../../includes/app-service-mobile-selector-get-started-users.md)]

Cette rubrique vous montre comment application mobile du tooyour tooadd l’authentification basée sur le cloud. Dans ce didacticiel, vous ajouter le projet de démarrage rapide de l’authentification toohello plateforme Windows universelle (UWP) pour les applications mobiles à l’aide d’un fournisseur d’identité qui est pris en charge par le Service d’applications Azure. Après avoir en cours a été authentifié et autorisé par votre serveur principal de l’application Mobile, la valeur d’ID utilisateur hello s’affiche.

Ce didacticiel est basé sur le démarrage rapide pour des applications mobiles hello. Vous devez d’abord terminer le didacticiel de hello [prise en main les applications mobiles](app-service-mobile-windows-store-dotnet-get-started.md).

## <a name="register"></a>Inscrire votre application pour l’authentification et de configurer hello du Service d’applications
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

Maintenant, vous pouvez vérifier que ce principal de tooyour l’accès anonyme a été désactivé. Avec le projet d’application UWP hello définir comme projet de démarrage hello, déployer et exécuter l’application hello ; Vérifiez qu’une exception non gérée avec un code d’état de 401 (non autorisé) est déclenchée après le démarrage de l’application hello. Cela se produit car l’application hello tente tooaccess le Code de votre application Mobile comme un utilisateur non authentifié, mais hello *TodoItem* table requiert l’authentification.

Ensuite, vous mettrez à jour les utilisateurs de hello application tooauthenticate avant de demander des ressources à partir de votre application de Service.

## <a name="add-authentication"></a>Ajouter une application de toohello d’authentification
1. Dans le projet d’application UWP hello MainPage.xaml.cs et ajoutez hello suivant extrait de code :
   
        // Define a member variable for storing hello signed-in user. 
        private MobileServiceUser user;
   
        // Define a method that performs hello authentication process
        // using a Facebook sign-in. 
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
            try
            {
                // Change 'MobileService' toohello name of your MobileServiceClient instance.
                // Sign-in using Facebook authentication.
                user = await App.MobileService
                    .LoginAsync(MobileServiceAuthenticationProvider.Facebook, "{url_scheme_of_your_app}");
                message =
                    string.Format("You are now signed in - {0}", user.UserId);
   
                success = true;
            }
            catch (InvalidOperationException)
            {
                message = "You must log in. Login Required";
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
            return success;
        }
   
    Ce code s’authentifie l’utilisateur hello avec une connexion Facebook. Si vous utilisez un fournisseur d’identité autre que Facebook, modifiez la valeur hello **MobileServiceAuthenticationProvider** au-dessus de valeur toohello pour votre fournisseur.
2. Remplacez hello **OnNavigatedTo()** méthode dans MainPage.xaml.cs. Ensuite, vous allez ajouter un **connectez-vous** application toohello bouton qui déclenche l’authentification.

        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            if (e.Parameter is Uri)
            {
                App.MobileService.ResumeWithURL(e.Parameter as Uri);
            }
        }

3. Ajoutez hello suivant extrait de code toohello MainPage.xaml.cs :
   
        private async void ButtonLogin_Click(object sender, RoutedEventArgs e)
        {
            // Login hello user and then load data from hello mobile app.
            if (await AuthenticateAsync())
            {
                // Switch hello buttons and load items from hello mobile app.
                ButtonLogin.Visibility = Visibility.Collapsed;
                ButtonSave.Visibility = Visibility.Visible;
                //await InitLocalStoreAsync(); //offline sync support.
                await RefreshTodoItems();
            }
        }
4. Ouvrir le fichier de projet hello MainPage.xaml, recherchez des élément hello qui définit hello **enregistrer** bouton et remplacez-le par hello suivant de code :
   
        <Button Name="ButtonSave" Visibility="Collapsed" Margin="0,8,8,0" 
                Click="ButtonSave_Click">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Add"/>
                <TextBlock Margin="5">Save</TextBlock>
            </StackPanel>
        </Button>
        <Button Name="ButtonLogin" Visibility="Visible" Margin="0,8,8,0" 
                Click="ButtonLogin_Click" TabIndex="0">
            <StackPanel Orientation="Horizontal">
                <SymbolIcon Symbol="Permissions"/>
                <TextBlock Margin="5">Sign in</TextBlock> 
            </StackPanel>
        </Button>
5. Ajoutez hello suivant extrait de code toohello App.xaml.cs :

        protected override void OnActivated(IActivatedEventArgs args)
        {
            if (args.Kind == ActivationKind.Protocol)
            {
                ProtocolActivatedEventArgs protocolArgs = args as ProtocolActivatedEventArgs;
                Frame content = Window.Current.Content as Frame;
                if (content.Content.GetType() == typeof(MainPage))
                {
                    content.Navigate(typeof(MainPage), protocolArgs.Uri);
                }
            }
            Window.Current.Activate();
            base.OnActivated(args);
        }
6. Ouvrez le fichier Package.appxmanifest, accédez trop**déclarations**, dans **déclarations disponibles** liste déroulante, sélectionnez **protocole** et cliquez sur **ajouter** bouton. À présent configurer hello **propriétés** Hello **protocole** déclaration. Dans **nom d’affichage**, ajoutez le nom hello toousers toodisplay de votre application. Dans **Nom**, ajoutez votre {url_scheme_of_your_app}.
7. Appuyez sur la touche application de hello hello F5 toorun clé, cliquez sur hello **connectez-vous** bouton et connectez-vous à application hello avec votre fournisseur d’identité choisi. Une fois que votre connexion est réussie, application hello s’exécute sans erreur et sont en mesure de tooquery votre serveur principal et d’effectuer des mises à jour toodata.

## <a name="tokens"></a>Jeton d’authentification hello banque d’informations sur le client de hello
Hello l’exemple précédent a montré une standard sign-in, ce qui nécessite hello client toocontact à la fois le fournisseur d’identité hello et hello App Service chaque fois que cette application hello démarre. Est non seulement cette méthode inefficace, vous pouvez exécuter dans l’utilisation-se rapporte les problèmes de nombreux clients essayez toostart votre application à hello même temps. Une meilleure approche est le jeton d’autorisation toocache hello retournées par votre Service d’applications et essayez toouse cela tout d’abord avant d’utiliser un fournisseur connectez-vous.

> [!NOTE]
> Vous pouvez mettre en cache jeton hello émis par les Services d’application, quelle que soit la que vous utilisez l’authentification de client géré ou par le service. Ce didacticiel utilise cette dernière.
> 
> 

[!INCLUDE [mobile-windows-universal-dotnet-authenticate-app-with-token](../../includes/mobile-windows-universal-dotnet-authenticate-app-with-token.md)]

## <a name="next-steps"></a>Étapes suivantes
Maintenant que vous terminé ce didacticiel de l’authentification de base, pensez à poursuivre sur tooone Hello suivant didacticiels :

* [Ajouter une application de tooyour de notifications push](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Découvrez comment les notifications push tooadd prennent en charge tooyour application et configurer votre application Mobile back-end toouse Azure Notification Hubs toosend les notifications de transmission.
* [Activer la synchronisation hors connexion pour votre application](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un serveur principal de l’application Mobile. Synchronisation hors connexion permet de toointeract les utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.

<!-- URLs. -->
[Get started with your mobile app]: app-service-mobile-windows-store-dotnet-get-started.md
