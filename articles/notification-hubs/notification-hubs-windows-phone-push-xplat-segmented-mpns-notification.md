---
title: "toosend de concentrateurs de Notification aaaUse dernières actualités (Windows Phone)"
description: Utilisez la balise de toouse de Azure Notification Hubs dans toosend inscriptions avec rupture news tooa Windows Phone application.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilisez toosend concentrateurs de Notification dernières actualités
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toouse Azure Notification Hubs toobroadcast avec rupture nouvelles notifications tooa Windows Phone 8.0/8.1 Silverlight application. Si vous ciblez Windows Store ou Windows Phone 8.1, consultez tootoohello [Windows universel](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version. Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories. Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications pour des ventilateurs de musique, etc..

Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello. Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello. Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance. Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Composants requis
Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification]. Avant de commencer ce didacticiel, vous devez suivre celui intitulé [prise en main des concentrateurs de Notification].

## <a name="add-category-selection-toohello-app"></a>Ajouter une application de toohello de sélection de catégorie
première étape de Hello est tooadd hello UI éléments tooyour principale page existante qui permettent de hello utilisateur tooselect catégories tooregister. catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello. Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.

1. Ouvrir le fichier de projet hello MainPage.xaml, puis remplacez hello **grille** éléments nommés `TitlePanel` et `ContentPanel` avec hello suivant de code :
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. Dans le projet de hello, créez une nouvelle classe nommée **Notifications**, ajouter hello **public** modificateur toohello définition de classe, puis ajoutez hello suivant **à l’aide de** instructions nouveau fichier de code toohello :
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. De code suivant de hello de copie dans hello nouvelle **Notifications** classe :
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    Cette classe utilise hello isolé stockage toostore hello catégories de news que cet appareil est tooreceive. Il contient également des tooregister des méthodes pour ces catégories en utilisant un [modèle](notification-hubs-templates-cross-platform-push-messages.md) l’enregistrement des notifications.


1. Dans le fichier de projet App.xaml.cs hello, ajouter hello suivant propriété toohello **application** classe. Remplacez hello `<hub name>` et `<connection string with listen access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature* que vous avez obtenu précédemment.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente. Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées. clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.
   > 
   > 
2. Dans votre MainPage.xaml.cs, ajoutez hello ligne suivante :
   
        using Windows.UI.Popups;
3. Dans le fichier de projet hello MainPage.xaml.cs, ajoutez hello suivant de méthode :
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    Cette méthode crée une liste de catégories et les utilisations hello **Notifications** classe liste de hello toostore dans le stockage local hello et inscrire les balises correspondantes hello avec votre concentrateur de notification. Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.

Votre application est maintenant en mesure de toostore un ensemble de catégories dans le stockage local sur l’appareil de hello ; inscrire auprès de hub de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories

## <a name="register-for-notifications"></a>Inscription à des notifications
Ces étapes auprès du hub de notification hello au démarrage à l’aide de catégories hello qui ont été stockés dans le stockage local.

> [!NOTE]
> Étant donné que le canal hello URI affecté par hello services de notifications Push Microsoft (MPNS) peut changer à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification. Cet exemple s’inscrit aux notifications à chaque démarrage de cette application hello. Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.
> 
> 

1. Ouvrez le fichier App.xaml.cs de hello et ajouter hello **async** modificateur trop**Application_Launching** méthode replace hello concentrateurs de Notification d’enregistrement code et que vous avez ajouté dans [prise en main des concentrateurs de Notification] avec hello suivant de code :
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Cela permet de s’assurer que chaque démarrage d’application hello, il récupère les catégories hello du stockage local et un enregistrement pour ces catégories de demande.
2. Dans le fichier de projet hello MainPage.xaml.cs, ajouter hello suivant le code qui implémente hello **OnNavigatedTo** méthode :
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
        }
   
    Cette page principale de hello mises à jour selon l’état hello précédemment enregistré des catégories.

application Hello est maintenant terminée et permettre de stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories. Ensuite, nous allons définir un serveur principal qui peut envoyer catégorie notifications toothis application.

## <a name="sending-tagged-notifications"></a>Envoi des notifications avec balises
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Exécutez l’application hello et générer des notifications
1. Dans Visual Studio, appuyez sur F5 toocompile et démarrer l’application hello.
   
    ![][1]
   
    Notez que cette application hello de que l’interface utilisateur fournit un ensemble bascule qui permet de choisir toosubscribe de catégories hello pour.
2. Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.
   
    application Hello convertit les catégories de hello sélectionné en balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello. Hello catégories inscrits sont retournés et affichés dans une boîte de dialogue.
   
    ![][2]
3. Après avoir reçu une confirmation que vos catégories ont été abonnement terminé, exécutez hello console application toosend des notifications pour chaque catégories. Vérifiez que vous recevez uniquement une notification pour les catégories hello à que vous êtes abonné.
   
    ![][3]

Vous avez terminé cette rubrique.

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[prise en main des concentrateurs de Notification]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

