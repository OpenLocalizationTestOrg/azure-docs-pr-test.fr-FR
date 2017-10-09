---
title: "aaaAzure concentrateurs de Notification d’avertir les utilisateurs avec le serveur principal .NET"
description: "Découvrez comment toosend sécurisée des notifications push dans Azure. Exemples de code écrits en c# à l’aide des API .NET de hello."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Notification des utilisateurs via Azure Notification Hubs avec service principal .NET
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Vue d'ensemble
Prise en charge des notifications push dans Azure vous permet de tooaccess un facile à utiliser, multiplateforme et infrastructure par émission de données à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes. Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push utilisateur de notifications tooa application spécifique sur un périphérique spécifique. Un serveur principal ASP.NET WebAPI est utilisé tooauthenticate clients. À l’aide de hello authentifié l’utilisateur du client, et étiquette est automatiquement ajoutée par l’inscription de toonotification hello principale. Cette balise sera toosend utilisé par les notifications de toogenerate hello principal pour un utilisateur spécifique. Pour plus d’informations sur l’inscription aux notifications à l’aide d’un serveur principal d’application, consultez la rubrique de guide de hello [l’inscription à partir de votre serveur principal d’application](http://msdn.microsoft.com/library/dn743807.aspx). Ce didacticiel s’appuie sur le concentrateur de notification hello et de projet que vous avez créé dans hello [prise en main des concentrateurs de Notification] didacticiel.

Ce didacticiel est également toohello requis de hello [Secure Push] didacticiel. Après avoir terminé les étapes de hello dans ce didacticiel, vous pouvez passer toohello [Secure Push] didacticiel qui montre comment toomodify hello de code dans ce didacticiel toosend une notification push en toute sécurité.

## <a name="before-you-begin"></a>Avant de commencer
Nous accordons de l’importance à vos commentaires. Si vous avez des difficultés à la fin de cette rubrique, ou des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello.

code Hello terminée pour ce didacticiel se trouve sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel, vous devez suivre les didacticiels Mobile Services suivants :

* [prise en main des concentrateurs de Notification]<br/>Vous créez votre hub de notification et réservez le nom de l’application hello et enregistrez les notifications de tooreceive dans ce didacticiel. Ce didacticiel part du principe que vous avez déjà effectué ces étapes. Dans le cas contraire, suivez les étapes de hello dans [mise en route avec Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); plus précisément, hello sections [inscrire votre application pour hello du Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) et [configurer votre concentrateur de Notification](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). En particulier, assurez-vous que vous avez entré hello **SID du Package** et **clé secrète Client** valeurs dans le portail de hello hello **configurer** onglet votre hub de notification. Cette procédure de configuration est décrite dans la section de hello [configurer votre concentrateur de Notification](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Il s’agit d’une étape importante : si les informations d’identification hello sur le portail hello ne correspondent pas celles spécifiées pour le nom de l’application hello choisie, les notifications de push hello ne réussissent pas.

> [!NOTE]
> Si vous utilisez des applications mobiles dans Azure App Service en tant que votre service principal, consultez hello [version des applications mobiles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) de ce didacticiel.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Mettre à jour le code hello pour le projet de client hello
Dans cette section, vous mettez à jour code hello dans le projet hello pour hello [prise en main des concentrateurs de Notification] didacticiel. Hello doit déjà être associée au magasin hello et configuré pour votre concentrateur de notification. Dans cette section, vous ajouter code toocall hello WebAPI serveur principal et l’utiliser pour l’inscription et l’envoi de notifications.

1. Dans Visual Studio, ouvrez la solution de hello de hello vous avez créé pour hello [prise en main des concentrateurs de Notification] didacticiel.
2. Dans l’Explorateur de solutions, cliquez sur hello **(Windows 8.1)** de projet, puis cliquez sur **gérer les Packages NuGet**.
3. Dans la partie gauche hello, cliquez sur **Online**.
4. Bonjour **recherche** , tapez **Http Client**.
5. Dans la liste des résultats hello, cliquez sur **Microsoft HTTP Client Libraries**, puis cliquez sur **installer**. Terminer l’installation de hello.
6. Dans hello NuGet **recherche** , tapez **Json.net**. Installer hello **Json.NET** package et la fenêtre du Gestionnaire de Package NuGet hello puis fermer.
7. Répétez les étapes de hello ci-dessus pour hello **(8.1 de Windows Phone)** hello tooinstall de projet **JSON.NET** package NuGet pour le projet Windows Phone de hello.
8. Dans l’Explorateur de solutions, Bonjour **(Windows 8.1)** de projet, double-cliquez sur **MainPage.xaml** tooopen dans l’éditeur de Visual Studio hello.
9. Bonjour **MainPage.xaml** code XML, remplacer hello `<Grid>` section avec hello suivant de code. Ce code ajoute une zone de texte Nom d’utilisateur et mot de passe utilisateur de hello authentifiera avec. Il ajoute également des zones de texte pour le message de notification hello et étiquette de nom d’utilisateur hello qui doit recevoir une notification hello :
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. Dans l’Explorateur de solutions, Bonjour **(8.1 de Windows Phone)** projet, ouvrez **MainPage.xaml** et remplacer hello Windows Phone 8.1 `<Grid>` section avec ce même code ci-dessus. interface de Hello doit ressembler toowhats comme indiqué ci-dessous.
    
    ![][13]
11. Dans l’Explorateur de solutions, ouvrez hello **MainPage.xaml.cs** fichier hello **(Windows 8.1)** et **(8.1 de Windows Phone)** projets. Ajoutez hello suit `using` instructions haut hello des deux fichiers :
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. Dans **MainPage.xaml.cs** pour hello **(Windows 8.1)** et **(8.1 de Windows Phone)** projets, ajouter hello suivant membre toohello `MainPage` classe. Être vraiment tooreplace `<Enter Your Backend Endpoint>` avec hello votre point de terminaison principal réel obtenu précédemment. Par exemple, `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Ajoutez le code hello sous la classe MainPage toohello **MainPage.xaml.cs** pour hello **(Windows 8.1)** et **(8.1 de Windows Phone)** projets.
    
    Hello `PushClick` méthode est hello Gestionnaire click pour hello **envoi Push** bouton. Il appelle hello principal tootrigger un tooall de notification des appareils avec une étiquette de nom d’utilisateur qui correspond à hello `to_tag` paramètre. message de notification Hello est envoyé en tant que contenu JSON dans le corps de la demande hello.
    
    Hello `LoginAndRegisterClick` méthode est hello Gestionnaire click pour hello **connectez-vous et inscrivez** bouton. Il stocke basic de hello jeton d’authentification dans le stockage local (Notez que cela représente n’importe quel jeton utilise de votre schéma d’authentification), puis utilise `RegisterClient` tooregister pour les notifications à l’aide de hello principal.

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. Dans l’Explorateur de solutions, sous hello **Shared** projet, ouvrez hello **App.xaml.cs** fichier. Rechercher les appels hello trop`InitNotificationsAsync()` Bonjour `OnLaunched()` Gestionnaire d’événements. Commentez ou supprimer les appels hello trop`InitNotificationsAsync()`. Gestionnaire de bouton Hello ajoutée ci-dessus initialisera les inscriptions de notification.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. Dans l’Explorateur de solutions, cliquez sur hello **Shared** de projet, puis cliquez sur **ajouter**, puis cliquez sur **classe**. Nom de classe hello **RegisterClient.cs**, puis cliquez sur **OK** classe hello de toogenerate.
   
   Cette classe encapsule hello REST appelle toocontact requis hello serveur principal d’application, dans tooregister d’ordre pour les notifications push. Il stocke également localement hello *registrationIds* créé par hello Hub de Notification comme détaillé dans [l’inscription à partir de votre serveur principal d’application](http://msdn.microsoft.com/library/dn743807.aspx). Notez qu’il utilise un jeton d’autorisation stocké dans le stockage local lorsque vous cliquez sur hello **connectez-vous et inscrivez** bouton.
2. Ajoutez hello suit `using` instructions haut hello du fichier de RegisterClient.cs hello :
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Ajouter hello suivant du code à l’intérieur de hello `RegisterClient` définition de classe.
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. Enregistrez toutes vos modifications.

## <a name="testing-hello-application"></a>Hello Application de test
1. Lancez l’application hello sur Windows 8.1 et Windows Phone 8.1. Pour Windows Phone 8.1, vous pouvez exécuter les instance hello dans l’émulateur de hello ou un appareil réel.
2. Dans l’instance de hello Windows 8.1 d’application hello, entrez un **nom d’utilisateur** et **mot de passe** comme indiqué dans l’écran hello ci-dessous. Il doit différer de nom d’utilisateur hello et le mot de passe entré sur Windows Phone.
3. Cliquez sur **Se connecter et s’inscrire** et vérifiez le contenu de la boîte de dialogue indiquant que vous êtes connecté. Cela permettra également hello **envoi Push** bouton.
   
    ![][14]
4. Sur l’instance de hello Windows Phone 8.1, entrez une chaîne de nom d’utilisateur dans les deux hello **nom d’utilisateur** et **mot de passe** champs puis cliquez sur **connexion et inscription**.
5. Ensuite, dans hello **balise de nom d’utilisateur destinataire** , entrez le nom d’utilisateur hello inscrit sur Windows 8.1. Entrez un message de notification, puis cliquez sur **Envoyer des notifications Push**.
   
    ![][16]
6. Seuls les appareils hello qui ont été inscrits auprès de balise de nom d’utilisateur hello recevoir message de notification de hello.
   
    ![][15]

## <a name="next-steps"></a>Étapes suivantes
* Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, consultez [toosend utiliser Notification Hubs actualités].
* consultez des concentrateurs de Notification toouse, toolearn plus sur la façon [des conseils de concentrateurs de Notification].

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[prise en main des concentrateurs de Notification]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
