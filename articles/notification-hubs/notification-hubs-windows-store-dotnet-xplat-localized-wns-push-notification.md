---
title: "aaaNotification concentrateurs localisée didacticiel News avec rupture"
description: "Découvrez comment toouse Azure Notification Hubs toosend localisée des notifications sur l’actualité."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Utiliser les informations de dernière minute toosend localisée de concentrateurs de Notification
> [!div class="op_single_selector"]
> * [Windows Store C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
Cette rubrique vous montre comment toouse hello **modèle** fonctionnalité de toobroadcast Azure Notification Hubs avec rupture des notifications de news qui ont été localisées par langue et de périphérique. Dans ce didacticiel, vous démarrez avec une application du Windows Store hello créée dans [toosend utiliser Notification Hubs actualités]. Lorsque vous avez terminé, que vous serez en mesure de tooregister pour les catégories qui que vous intéressez, spécifiez une langue dans les notifications de hello tooreceive et recevoir des notifications push uniquement pour les catégories de hello sélectionné dans cette langue.

Voici un scénario de toothis deux parties :

* application du Windows Store Hello permet client appareils toospecify une langue et toodifferent toosubscribe avec rupture des catégories d’informations ;
* notifications de hello, à l’aide de hello diffuse Hello principal **balise** et **modèle** profiter de Azure Notification Hubs.

## <a name="prerequisites"></a>Composants requis
Vous devez avoir déjà terminé hello [toosend utiliser Notification Hubs actualités] didacticiel et code hello disponible, car ce didacticiel s’appuie directement sur ce code.

Vous avez également besoin de Visual Studio 2012 (ou version ultérieure).

## <a name="template-concepts"></a>Concepts de modèle
Dans [toosend utiliser Notification Hubs actualités] vous avez créé une application qui a utilisé **balises** toonotifications toosubscribe pour les catégories d’informations différente.
Cependant, de nombreuses applications sont destinées à plusieurs marchés et doivent donc être localisées. Cela signifie que que le contenu des notifications hello eux-mêmes hello ont toobe localisée toohello livré corriger l’ensemble d’appareils.
Dans cette rubrique, nous allons montrer comment toouse hello **modèle** fonctionnalité de Notification Hubs tooeasily remettre localisée des notifications sur l’actualité.

Remarque : une façon toosend localisée notifications est toocreate plusieurs versions de ces balises. Par exemple, toosupport en anglais, Français et Mandarin, il nous faudrait trois balises différentes pour les nouvelles : « world_en », « world_fr » et « world_ch ». Nous devons à toosend ensuite une version localisée de hello world news tooeach de ces balises. Dans cette rubrique, nous utilisons prolifération de hello tooavoid modèles de balises et l’exigence de hello envoyer plusieurs messages.

À un niveau élevé, les modèles sont un moyen toospecify comment un périphérique spécifique doit recevoir une notification. modèle de Hello Spécifie le format de charge utile exacte de hello en vous reportant tooproperties qui font partie de message de type hello envoyée par votre serveur principal d’application. Aux fins de notre exemple, nous allons envoyer un message de paramètres régionaux contenant toutes les langues prises en charge :

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Ensuite, nous nous assurons qu’appareils auprès d’un modèle qui fait référence de propriété correcte de toohello. Par exemple, une application du Windows Store qui veut tooreceive un message simple notification toast s’inscrivent pour hello suivant le modèle avec des balises correspondantes :

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Les modèles sont une fonctionnalité très puissante sur laquelle vous pouvez obtenir plus d’informations en lisant notre article [Modèles](notification-hubs-templates-cross-platform-push-messages.md) . 

## <a name="hello-app-user-interface"></a>interface utilisateur d’application Hello
Maintenant, nous allons modifier hello dernières nouvelles applications que vous avez créé dans la rubrique de hello [toosend utiliser Notification Hubs actualités] toosend localisée des informations de dernière minute à l’aide de modèles.

Dans votre application Windows Store :

Modifier votre tooinclude MainPage.xaml un combobox de paramètres régionaux :

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a>Création d’application de client hello du Windows Store
1. Dans votre classe de Notifications, ajouter un tooyour de paramètre de paramètres régionaux *StoreCategoriesAndSubscribe* et *SubscribeToCateories* méthodes.
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    Notez que, au lieu de l’appel hello *RegisterNativeAsync* méthode que nous appelons *RegisterTemplateAsync*: nous enregistrons un format de notification spécifique dans le hello modèle dépend des paramètres régionaux de hello. Nous avons également fournir un nom pour le modèle hello (« localizedWNSTemplateExample »), car nous souhaitions tooregister plusieurs modèles (par exemple un pour les notifications de toast) et l’autre pour les vignettes et nous devons tooname dans tooupdate en mesure de toobe de commande ou les supprimer.
   
    Notez que si un appareil inscrit plusieurs modèles avec hello même balise, un message entrant de ciblage que balise entraîne plusieurs remettre les notifications d’appareil toohello (un pour chaque modèle). Ce comportement est utile lorsque hello message logique même a tooresult dans plusieurs notifications visuelles, par exemple avec un badge et un toast dans une application du Windows Store.
2. Ajoutez hello suivant les paramètres régionaux stocké méthode tooretrieve hello :
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. Dans votre MainPage.xaml.cs, mettre à jour de votre bouton Gestionnaire click par la récupération de hello de valeur actuelle de la zone de liste déroulante de paramètres régionaux hello et il fournit la classe de Notifications de toohello appel toohello, comme indiqué :
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. Enfin, assurez-vous que tooupdate dans votre fichier App.xaml.cs, votre `InitNotificationsAsync` méthode tooretrieve hello des paramètres régionaux et l’utiliser lors de l’abonnement :
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a>Envoi de notifications localisées à partir de votre serveur principal
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[toosend utiliser Notification Hubs actualités]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
