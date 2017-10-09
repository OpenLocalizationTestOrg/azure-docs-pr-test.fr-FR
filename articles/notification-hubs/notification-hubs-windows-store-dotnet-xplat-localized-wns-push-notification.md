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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="ca960-103">Utiliser les informations de dernière minute toosend localisée de concentrateurs de Notification</span><span class="sxs-lookup"><span data-stu-id="ca960-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ca960-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="ca960-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="ca960-105">iOS</span><span class="sxs-lookup"><span data-stu-id="ca960-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ca960-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ca960-106">Overview</span></span>
<span data-ttu-id="ca960-107">Cette rubrique vous montre comment toouse hello **modèle** fonctionnalité de toobroadcast Azure Notification Hubs avec rupture des notifications de news qui ont été localisées par langue et de périphérique.</span><span class="sxs-lookup"><span data-stu-id="ca960-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="ca960-108">Dans ce didacticiel, vous démarrez avec une application du Windows Store hello créée dans [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="ca960-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="ca960-109">Lorsque vous avez terminé, que vous serez en mesure de tooregister pour les catégories qui que vous intéressez, spécifiez une langue dans les notifications de hello tooreceive et recevoir des notifications push uniquement pour les catégories de hello sélectionné dans cette langue.</span><span class="sxs-lookup"><span data-stu-id="ca960-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="ca960-110">Voici un scénario de toothis deux parties :</span><span class="sxs-lookup"><span data-stu-id="ca960-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="ca960-111">application du Windows Store Hello permet client appareils toospecify une langue et toodifferent toosubscribe avec rupture des catégories d’informations ;</span><span class="sxs-lookup"><span data-stu-id="ca960-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="ca960-112">notifications de hello, à l’aide de hello diffuse Hello principal **balise** et **modèle** profiter de Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ca960-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca960-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ca960-113">Prerequisites</span></span>
<span data-ttu-id="ca960-114">Vous devez avoir déjà terminé hello [toosend utiliser Notification Hubs actualités] didacticiel et code hello disponible, car ce didacticiel s’appuie directement sur ce code.</span><span class="sxs-lookup"><span data-stu-id="ca960-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="ca960-115">Vous avez également besoin de Visual Studio 2012 (ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="ca960-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="ca960-116">Concepts de modèle</span><span class="sxs-lookup"><span data-stu-id="ca960-116">Template concepts</span></span>
<span data-ttu-id="ca960-117">Dans [toosend utiliser Notification Hubs actualités] vous avez créé une application qui a utilisé **balises** toonotifications toosubscribe pour les catégories d’informations différente.</span><span class="sxs-lookup"><span data-stu-id="ca960-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="ca960-118">Cependant, de nombreuses applications sont destinées à plusieurs marchés et doivent donc être localisées.</span><span class="sxs-lookup"><span data-stu-id="ca960-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="ca960-119">Cela signifie que que le contenu des notifications hello eux-mêmes hello ont toobe localisée toohello livré corriger l’ensemble d’appareils.</span><span class="sxs-lookup"><span data-stu-id="ca960-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="ca960-120">Dans cette rubrique, nous allons montrer comment toouse hello **modèle** fonctionnalité de Notification Hubs tooeasily remettre localisée des notifications sur l’actualité.</span><span class="sxs-lookup"><span data-stu-id="ca960-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="ca960-121">Remarque : une façon toosend localisée notifications est toocreate plusieurs versions de ces balises.</span><span class="sxs-lookup"><span data-stu-id="ca960-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="ca960-122">Par exemple, toosupport en anglais, Français et Mandarin, il nous faudrait trois balises différentes pour les nouvelles : « world_en », « world_fr » et « world_ch ».</span><span class="sxs-lookup"><span data-stu-id="ca960-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="ca960-123">Nous devons à toosend ensuite une version localisée de hello world news tooeach de ces balises.</span><span class="sxs-lookup"><span data-stu-id="ca960-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="ca960-124">Dans cette rubrique, nous utilisons prolifération de hello tooavoid modèles de balises et l’exigence de hello envoyer plusieurs messages.</span><span class="sxs-lookup"><span data-stu-id="ca960-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="ca960-125">À un niveau élevé, les modèles sont un moyen toospecify comment un périphérique spécifique doit recevoir une notification.</span><span class="sxs-lookup"><span data-stu-id="ca960-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="ca960-126">modèle de Hello Spécifie le format de charge utile exacte de hello en vous reportant tooproperties qui font partie de message de type hello envoyée par votre serveur principal d’application.</span><span class="sxs-lookup"><span data-stu-id="ca960-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="ca960-127">Aux fins de notre exemple, nous allons envoyer un message de paramètres régionaux contenant toutes les langues prises en charge :</span><span class="sxs-lookup"><span data-stu-id="ca960-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="ca960-128">Ensuite, nous nous assurons qu’appareils auprès d’un modèle qui fait référence de propriété correcte de toohello.</span><span class="sxs-lookup"><span data-stu-id="ca960-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="ca960-129">Par exemple, une application du Windows Store qui veut tooreceive un message simple notification toast s’inscrivent pour hello suivant le modèle avec des balises correspondantes :</span><span class="sxs-lookup"><span data-stu-id="ca960-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="ca960-130">Les modèles sont une fonctionnalité très puissante sur laquelle vous pouvez obtenir plus d’informations en lisant notre article [Modèles](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="ca960-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="ca960-131">interface utilisateur d’application Hello</span><span class="sxs-lookup"><span data-stu-id="ca960-131">hello app user interface</span></span>
<span data-ttu-id="ca960-132">Maintenant, nous allons modifier hello dernières nouvelles applications que vous avez créé dans la rubrique de hello [toosend utiliser Notification Hubs actualités] toosend localisée des informations de dernière minute à l’aide de modèles.</span><span class="sxs-lookup"><span data-stu-id="ca960-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="ca960-133">Dans votre application Windows Store :</span><span class="sxs-lookup"><span data-stu-id="ca960-133">In your Windows Store app:</span></span>

<span data-ttu-id="ca960-134">Modifier votre tooinclude MainPage.xaml un combobox de paramètres régionaux :</span><span class="sxs-lookup"><span data-stu-id="ca960-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

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

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="ca960-135">Création d’application de client hello du Windows Store</span><span class="sxs-lookup"><span data-stu-id="ca960-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="ca960-136">Dans votre classe de Notifications, ajouter un tooyour de paramètre de paramètres régionaux *StoreCategoriesAndSubscribe* et *SubscribeToCateories* méthodes.</span><span class="sxs-lookup"><span data-stu-id="ca960-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
   
    <span data-ttu-id="ca960-137">Notez que, au lieu de l’appel hello *RegisterNativeAsync* méthode que nous appelons *RegisterTemplateAsync*: nous enregistrons un format de notification spécifique dans le hello modèle dépend des paramètres régionaux de hello.</span><span class="sxs-lookup"><span data-stu-id="ca960-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="ca960-138">Nous avons également fournir un nom pour le modèle hello (« localizedWNSTemplateExample »), car nous souhaitions tooregister plusieurs modèles (par exemple un pour les notifications de toast) et l’autre pour les vignettes et nous devons tooname dans tooupdate en mesure de toobe de commande ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="ca960-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="ca960-139">Notez que si un appareil inscrit plusieurs modèles avec hello même balise, un message entrant de ciblage que balise entraîne plusieurs remettre les notifications d’appareil toohello (un pour chaque modèle).</span><span class="sxs-lookup"><span data-stu-id="ca960-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="ca960-140">Ce comportement est utile lorsque hello message logique même a tooresult dans plusieurs notifications visuelles, par exemple avec un badge et un toast dans une application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="ca960-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="ca960-141">Ajoutez hello suivant les paramètres régionaux stocké méthode tooretrieve hello :</span><span class="sxs-lookup"><span data-stu-id="ca960-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="ca960-142">Dans votre MainPage.xaml.cs, mettre à jour de votre bouton Gestionnaire click par la récupération de hello de valeur actuelle de la zone de liste déroulante de paramètres régionaux hello et il fournit la classe de Notifications de toohello appel toohello, comme indiqué :</span><span class="sxs-lookup"><span data-stu-id="ca960-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="ca960-143">Enfin, assurez-vous que tooupdate dans votre fichier App.xaml.cs, votre `InitNotificationsAsync` méthode tooretrieve hello des paramètres régionaux et l’utiliser lors de l’abonnement :</span><span class="sxs-lookup"><span data-stu-id="ca960-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
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

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="ca960-144">Envoi de notifications localisées à partir de votre serveur principal</span><span class="sxs-lookup"><span data-stu-id="ca960-144">Send localized notifications from your back-end</span></span>
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
