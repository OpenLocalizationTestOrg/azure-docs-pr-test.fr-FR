---
title: "Didacticiel sur l’utilisation de Notification Hubs pour envoyer les dernières nouvelles localisées"
description: "Découvrez comment utiliser Azure Notification Hubs pour envoyer des notifications de dernières nouvelles localisées."
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
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="ada95-103">Utilisation de Notification Hubs pour envoyer les dernières nouvelles localisées</span><span class="sxs-lookup"><span data-stu-id="ada95-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ada95-104">Windows Store C#</span><span class="sxs-lookup"><span data-stu-id="ada95-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="ada95-105">iOS</span><span class="sxs-lookup"><span data-stu-id="ada95-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="ada95-106">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ada95-106">Overview</span></span>
<span data-ttu-id="ada95-107">Cette rubrique montre comment utiliser la fonctionnalité de **modèle** d’Azure Notification Hubs pour diffuser des notifications relatives aux dernières nouvelles qui ont été localisées par langue et par appareil.</span><span class="sxs-lookup"><span data-stu-id="ada95-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="ada95-108">Vous devez commencer ce didacticiel avec l'application Windows Store que vous avez créée dans le cadre du didacticiel [Utilisation de Notification Hubs pour envoyer les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="ada95-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="ada95-109">Lorsque vous aurez terminé, vous pourrez vous inscrire aux catégories qui vous intéressent, spécifier une langue dans laquelle recevoir les notifications et recevoir uniquement des notifications Push pour les catégories sélectionnées dans cette langue.</span><span class="sxs-lookup"><span data-stu-id="ada95-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="ada95-110">Ce scénario comporte deux parties :</span><span class="sxs-lookup"><span data-stu-id="ada95-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="ada95-111">L'application Windows Store permet aux appareils clients de spécifier une langue et de s'abonner à différentes catégories de dernières nouvelles.</span><span class="sxs-lookup"><span data-stu-id="ada95-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="ada95-112">Le serveur principal diffuse les notifications à l’aide des fonctionnalités de **balise** et de **modèle** d’Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="ada95-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ada95-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ada95-113">Prerequisites</span></span>
<span data-ttu-id="ada95-114">Vous devez avoir suivi le didacticiel [Utilisation de Notification Hubs pour envoyer les dernières nouvelles] et avoir le code à disposition, car le présent didacticiel est basé sur ce code.</span><span class="sxs-lookup"><span data-stu-id="ada95-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="ada95-115">Vous avez également besoin de Visual Studio 2012 (ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="ada95-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="ada95-116">Concepts de modèle</span><span class="sxs-lookup"><span data-stu-id="ada95-116">Template concepts</span></span>
<span data-ttu-id="ada95-117">Dans le didacticiel [Utilisation de Notification Hubs pour envoyer les dernières nouvelles] , vous avez créé une application qui se sert de **balises** pour s'abonner aux notifications relatives à différentes catégories de nouvelles.</span><span class="sxs-lookup"><span data-stu-id="ada95-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="ada95-118">Cependant, de nombreuses applications sont destinées à plusieurs marchés et doivent donc être localisées.</span><span class="sxs-lookup"><span data-stu-id="ada95-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="ada95-119">Cela signifie que le contenu des notifications proprement dites doit lui aussi être localisé et envoyé au bon ensemble d’appareils.</span><span class="sxs-lookup"><span data-stu-id="ada95-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="ada95-120">Dans cette rubrique, nous allons vous montrer comment utiliser la fonctionnalité de **modèle** de Notification Hubs pour facilement envoyer des notifications de dernières nouvelles localisées.</span><span class="sxs-lookup"><span data-stu-id="ada95-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="ada95-121">Remarque : pour envoyer des notifications localisées, vous pouvez notamment créer plusieurs versions de chaque balise.</span><span class="sxs-lookup"><span data-stu-id="ada95-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="ada95-122">Par exemple, pour prendre en charge l'anglais, le français et le mandarin, nous aurions besoin de trois balises différentes pour les nouvelles internationales : « world_en », « world_fr » et « world_ch ».</span><span class="sxs-lookup"><span data-stu-id="ada95-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="ada95-123">Il faudrait ensuite que nous envoyions une version localisée des nouvelles internationales à chacune de ces balises.</span><span class="sxs-lookup"><span data-stu-id="ada95-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="ada95-124">Dans cette rubrique, nous utilisons des modèles afin d'éviter la prolifération de balises et d'éliminer la nécessité d'envoyer plusieurs messages.</span><span class="sxs-lookup"><span data-stu-id="ada95-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="ada95-125">À un haut niveau, les modèles permettent de spécifier comment un appareil particulier reçoit une notification.</span><span class="sxs-lookup"><span data-stu-id="ada95-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="ada95-126">Le modèle spécifie le format de charge utile exact en se référant aux propriétés qui font partie du message envoyé par le serveur principal de votre application.</span><span class="sxs-lookup"><span data-stu-id="ada95-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="ada95-127">Aux fins de notre exemple, nous allons envoyer un message de paramètres régionaux contenant toutes les langues prises en charge :</span><span class="sxs-lookup"><span data-stu-id="ada95-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="ada95-128">Ensuite, nous allons nous assurer que les appareils s'inscrivent avec un modèle qui se réfère à la bonne propriété.</span><span class="sxs-lookup"><span data-stu-id="ada95-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="ada95-129">Par exemple, une application Windows Store qui veut recevoir un simple message toast doit s’inscrire pour le modèle suivant, avec les balises correspondantes :</span><span class="sxs-lookup"><span data-stu-id="ada95-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="ada95-130">Les modèles sont une fonctionnalité très puissante sur laquelle vous pouvez obtenir plus d’informations en lisant notre article [Modèles](notification-hubs-templates-cross-platform-push-messages.md) .</span><span class="sxs-lookup"><span data-stu-id="ada95-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="ada95-131">Interface utilisateur de l’application</span><span class="sxs-lookup"><span data-stu-id="ada95-131">The app user interface</span></span>
<span data-ttu-id="ada95-132">Nous allons maintenant modifier l’application de dernières nouvelles que vous avez créée à la rubrique [Utilisation de Notification Hubs pour envoyer les dernières nouvelles] pour envoyer les dernières nouvelles localisées à l’aide de modèles.</span><span class="sxs-lookup"><span data-stu-id="ada95-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="ada95-133">Dans votre application Windows Store :</span><span class="sxs-lookup"><span data-stu-id="ada95-133">In your Windows Store app:</span></span>

<span data-ttu-id="ada95-134">Modifiez le fichier MainPage.xaml pour qu'il inclue une zone de liste modifiable pour les paramètres régionaux :</span><span class="sxs-lookup"><span data-stu-id="ada95-134">Change your MainPage.xaml to include a locale combobox:</span></span>

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

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="ada95-135">Création de l’application cliente Windows Store</span><span class="sxs-lookup"><span data-stu-id="ada95-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="ada95-136">Dans la classe Notifications, ajoutez un paramètre régional aux méthodes *StoreCategoriesAndSubscribe* et *SubscribeToCateories*.</span><span class="sxs-lookup"><span data-stu-id="ada95-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="ada95-137">Notez qu’au lieu d’appeler la méthode *RegisterNativeAsync*, nous appelons *RegisterTemplateAsync* : nous inscrivons un format de notification spécifique dans lequel le modèle dépend des paramètres régionaux.</span><span class="sxs-lookup"><span data-stu-id="ada95-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="ada95-138">Nous avons également fourni un nom pour le modèle (« localizedWNSTemplateExample »), parce qu’il est possible que nous inscrivions plusieurs modèles (par exemple un pour les notifications toast et un pour les vignettes) et nous devons donc les nommer pour pouvoir les mettre à jour ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="ada95-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="ada95-139">Notez que si un appareil inscrit plusieurs modèles avec la même balise, un message entrant ciblant cette balise entraînera l'envoi de plusieurs notifications à l'appareil (un pour chaque modèle).</span><span class="sxs-lookup"><span data-stu-id="ada95-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="ada95-140">Ce comportement s'avère utile lorsque le même message logique doit générer plusieurs notifications visuelles, par exemple affichant un badge et un toast dans une application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="ada95-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="ada95-141">Ajoutez la méthode suivante pour extraire les paramètres régionaux stockés :</span><span class="sxs-lookup"><span data-stu-id="ada95-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="ada95-142">Dans le fichier MainPage.xaml.cs, mettez le gestionnaire de clics de bouton à jour en extrayant la valeur actuelle de la zone de liste déroulante Paramètres régionaux et en la fournissant à l’appel de la classe Notifications, comme indiqué ci-après :</span><span class="sxs-lookup"><span data-stu-id="ada95-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="ada95-143">Enfin, dans votre fichier App.xaml.cs, veillez à mettre à jour votre méthode `InitNotificationsAsync` pour extraire les paramètres régionaux et les utiliser lors de l’abonnement :</span><span class="sxs-lookup"><span data-stu-id="ada95-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="ada95-144">Envoi de notifications localisées à partir de votre serveur principal</span><span class="sxs-lookup"><span data-stu-id="ada95-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="ada95-145">[Utilisation de Notification Hubs pour envoyer les dernières nouvelles]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="ada95-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
