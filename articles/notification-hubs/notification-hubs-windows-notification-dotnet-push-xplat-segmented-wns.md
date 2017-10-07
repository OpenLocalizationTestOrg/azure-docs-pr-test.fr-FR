---
title: "toosend de concentrateurs de Notification aaaUse dernières actualités (Windows universel)"
description: "Utilisez Azure Notification Hubs avec balises dans toosend d’inscription hello dernières actualités tooa l’application Windows universelle."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Utilisez toosend concentrateurs de Notification dernières actualités
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toobroadcast d’Azure Notification Hubs toouse dernières nouvelles notifications tooa Windows Store ou Windows Phone 8.1 (non Silverlight). Si vous ciblez Windows Phone 8.1 Silverlight, consultez toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version. Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories. Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications de ventilateurs de musique et ainsi de suite. 

Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello. Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello. Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance. Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Les projets Windows Store et Windows Phone version 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017.  Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Composants requis
Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification][get-started]. Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].

## <a name="add-category-selection-toohello-app"></a>Ajouter une application de toohello de sélection de catégorie
première étape de Hello est tooadd hello UI éléments tooyour principale page existante qui permettent de hello utilisateur tooselect catégories tooregister. catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello. Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.

1. Ouvrez le fichier de projet hello MainPage.xaml, puis hello copie suivant code Bonjour **grille** élément :
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. Cliquez avec le bouton droit sur hello **Shared** de projet et ajoutez une nouvelle classe nommée **Notifications**, ajouter hello **public** modificateur toohello définition de classe, puis ajoutez hello suivant **à l’aide de** instructions toohello nouveau fichier de code :
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. De code suivant de hello de copie dans hello nouvelle **Notifications** classe :
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    Cette classe utilise hello stockage local des catégories de hello toostore de news que ce périphérique a tooreceive. Notez que, au lieu de l’appel hello *RegisterNativeAsync* méthode que nous appelons *RegisterTemplateAsync* tooregister pour les catégories de hello à l’aide d’une inscription de modèle. 
   
    Nous avons également fournir un nom pour le modèle hello (« simpleWNSTemplateExample »), car nous souhaitions tooregister plusieurs modèles (par exemple un pour les notifications de toast) et l’autre pour les vignettes et nous devons tooname dans tooupdate en mesure de toobe de commande ou les supprimer.
   
    Notez que si un appareil inscrit plusieurs modèles avec hello même balise, un message entrant de ciblage que balise entraîne plusieurs remettre les notifications d’appareil toohello (un pour chaque modèle). Ce comportement est utile lorsque hello message logique même a tooresult dans plusieurs notifications visuelles, par exemple avec un badge et un toast dans une application du Windows Store.
   
    Pour plus d’informations sur les modèles, consultez la rubrique [Modèles](notification-hubs-templates-cross-platform-push-messages.md).
4. Dans le fichier de projet App.xaml.cs hello, ajouter hello suivant propriété toohello **application** classe :
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Cette propriété est utilisée toocreate et accès un **Notifications** instance.
   
    Bonjour au-dessus de code, remplacez hello `<hub name>` et `<connection string with listen access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature* que vous avez obtenu précédemment.
   
   > [!NOTE]
   > Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente. Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées. clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.
   > 
   > 
5. Dans votre MainPage.xaml.cs, ajoutez hello ligne suivante :
   
        using Windows.UI.Popups;
6. Dans le fichier de projet hello MainPage.xaml.cs, ajoutez hello suivant de méthode :
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    Cette méthode crée une liste de catégories et les utilisations hello **Notifications** classe liste de hello toostore dans le stockage local hello et inscrire les balises correspondantes hello avec votre concentrateur de notification. Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.

Votre application est maintenant en mesure de toostore un ensemble de catégories dans le stockage local sur l’appareil de hello ; inscrire auprès de hub de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories

## <a name="register-for-notifications"></a>Inscription à des notifications
Ces étapes auprès du hub de notification hello au démarrage à l’aide de catégories hello qui ont été stockés dans le stockage local.

> [!NOTE]
> Étant donné que le canal hello URI affecté par hello Service de Notification de Windows (WNS) permettre changer à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification. Cet exemple inscrit pour la notification chaque fois que cette application hello démarre. Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.
> 
> 

1. Hello de fichier et de mise à jour de App.xaml.cs hello ouvrir **InitNotificationsAsync** hello toouse de méthode `notifications` toosubscribe de classe en fonction de catégories.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Cela permet de s’assurer que chaque démarrage d’application hello, il récupère les catégories hello du stockage local et demande une inscription pour ces catégories. Hello **InitNotificationsAsync** méthode a été créée dans le cadre de hello [prise en main des concentrateurs de Notification] [ get-started] didacticiel.
2. Dans le fichier de projet hello MainPage.xaml.cs, ajouter hello suivant code toohello *OnNavigatedTo* méthode :
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
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
   
    ![][19]
3. Envoyer une nouvelle notification de back-end hello dans un des hello suivant façons :
   
   * **Application console :** démarrer l’application de console hello.
   * **Java/PHP :** exécutez votre application/script.
     
     Les notifications pour les catégories de hello sélectionné s’affichent sous forme de notifications de toast.
     
     ![][14]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, nous l’avons vu comment toobroadcast actualités par catégorie. Envisager d’effectuer une des hello suivant des didacticiels qui mettent en évidence les autres scénarios avancés de concentrateurs de Notification :

* [Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]
  
    Découvrez comment hello tooexpand dernières actualités application tooenable envoi localisée des notifications.

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
