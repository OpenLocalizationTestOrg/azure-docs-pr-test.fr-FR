---
title: "Utilisation de Notification Hubs pour diffuser les dernières nouvelles (Windows Universal)"
description: "Utilisez Azure Notification Hubs avec des balises dans l’inscription pour envoyer les dernières nouvelles à une application Windows universelle."
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
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="b3733-103">Utilisation de Notification Hubs pour diffuser les dernières nouvelles</span><span class="sxs-lookup"><span data-stu-id="b3733-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="b3733-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b3733-104">Overview</span></span>
<span data-ttu-id="b3733-105">Cette rubrique montre comment utiliser Azure Notification Hubs pour diffuser des notifications relatives aux dernières nouvelles vers une application Windows Store ou Windows Phone 8.1 (non-Silverlight).</span><span class="sxs-lookup"><span data-stu-id="b3733-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="b3733-106">Si vous ciblez Windows Phone 8.1 Silverlight, consultez la version [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="b3733-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="b3733-107">Lorsque vous aurez terminé, vous pourrez vous inscrire aux catégories de dernières nouvelles qui vous intéressent et recevoir uniquement des notifications Push pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="b3733-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="b3733-108">Ce scénario est un modèle courant pour de nombreuses applications pour lesquelles des notifications doivent être envoyées à des groupes d’utilisateurs qui ont manifesté antérieurement leur intérêt : lecteur RSS, applications pour fans de musique, etc.</span><span class="sxs-lookup"><span data-stu-id="b3733-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="b3733-109">Les scénarios de diffusion sont activés en incluant une ou plusieurs *balises* durant la création d’une inscription dans le hub de notification.</span><span class="sxs-lookup"><span data-stu-id="b3733-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="b3733-110">Lorsque des notifications sont envoyées à une balise, tous les appareils pour lesquels cette balise est inscrite reçoivent la notification.</span><span class="sxs-lookup"><span data-stu-id="b3733-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="b3733-111">Les balises étant de simples chaînes, il n’est pas nécessaire de les mettre en service à l’avance.</span><span class="sxs-lookup"><span data-stu-id="b3733-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="b3733-112">Pour plus d’informations sur les balises, consultez [Routage et expressions de balise Notification Hubs](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="b3733-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="b3733-113">Les projets Windows Store et Windows Phone version 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b3733-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="b3733-114">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="b3733-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="b3733-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b3733-115">Prerequisites</span></span>
<span data-ttu-id="b3733-116">Cette rubrique s'appuie sur l'application que vous avez créée dans [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="b3733-116">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="b3733-117">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="b3733-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="b3733-118">Ajout d’une sélection de catégories à l’application</span><span class="sxs-lookup"><span data-stu-id="b3733-118">Add category selection to the app</span></span>
<span data-ttu-id="b3733-119">La première étape consiste à ajouter des éléments de l’interface utilisateur à votre page principale existante qui permettent à l’utilisateur de sélectionner des catégories auxquelles s’inscrire.</span><span class="sxs-lookup"><span data-stu-id="b3733-119">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="b3733-120">Les catégories sélectionnées par un utilisateur sont stockées sur l'appareil.</span><span class="sxs-lookup"><span data-stu-id="b3733-120">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="b3733-121">Lorsque l'application démarre, une inscription d'appareil est créée dans votre Notification Hub avec les catégories sélectionnées sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="b3733-121">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="b3733-122">Ouvrez le fichier projet MainPage.xaml, puis copiez le code suivant dans l'élément **Grid** :</span><span class="sxs-lookup"><span data-stu-id="b3733-122">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
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
2. <span data-ttu-id="b3733-123">Cliquez avec le bouton droit sur le projet **Partagé**, ajoutez une nouvelle classe nommée **Notifications**, ajoutez le modificateur **public** à la définition de la classe, puis ajoutez les instructions **using** suivantes au nouveau fichier de code :</span><span class="sxs-lookup"><span data-stu-id="b3733-123">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="b3733-124">Ajoutez le code suivant dans la nouvelle classe **Notifications** :</span><span class="sxs-lookup"><span data-stu-id="b3733-124">Copy the following code into the new **Notifications** class:</span></span>
   
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
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    <span data-ttu-id="b3733-125">Cette classe utilise le stockage local pour stocker les catégories de nouvelles que cet appareil doit recevoir.</span><span class="sxs-lookup"><span data-stu-id="b3733-125">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="b3733-126">Notez que, au lieu d’appeler la méthode *RegisterNativeAsync*, nous appelons *RegisterTemplateAsync* pour enregistrer les catégories à l’aide d’un modèle d’inscription.</span><span class="sxs-lookup"><span data-stu-id="b3733-126">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="b3733-127">Nous avons également fourni un nom pour le modèle (« simpleWNSTemplateExample »), parce qu’il est possible que nous inscrivions plusieurs modèles (par exemple un pour les notifications toast et un pour les vignettes) et nous devons donc les nommer pour pouvoir les mettre à jour ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="b3733-127">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="b3733-128">Notez que si un appareil inscrit plusieurs modèles avec la même balise, un message entrant ciblant cette balise entraînera l'envoi de plusieurs notifications à l'appareil (un pour chaque modèle).</span><span class="sxs-lookup"><span data-stu-id="b3733-128">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="b3733-129">Ce comportement s'avère utile lorsque le même message logique doit générer plusieurs notifications visuelles, par exemple affichant un badge et un toast dans une application Windows Store.</span><span class="sxs-lookup"><span data-stu-id="b3733-129">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="b3733-130">Pour plus d’informations sur les modèles, consultez la rubrique [Modèles](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="b3733-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="b3733-131">Dans le fichier projet App.xaml.cs, ajoutez la propriété suivante à la classe **App** :</span><span class="sxs-lookup"><span data-stu-id="b3733-131">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="b3733-132">Cette propriété sert à créer l'instance **Notifications** et à y accéder.</span><span class="sxs-lookup"><span data-stu-id="b3733-132">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="b3733-133">Dans le code ci-dessus, remplacez les espaces réservés `<hub name>` et `<connection string with listen access>` par le nom du hub de notification et la chaîne de connexion pour *DefaultListenSharedAccessSignature* obtenue précédemment.</span><span class="sxs-lookup"><span data-stu-id="b3733-133">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b3733-134">Les informations d’identification distribuées avec une application cliente n’étant généralement pas sécurisées, vous ne devez distribuer que la clé d’accès d’écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="b3733-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="b3733-135">L'accès d'écoute permet à votre application de s'inscrire à des notifications, mais les inscriptions existantes ne peuvent pas être modifiées et les notifications ne peuvent pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="b3733-135">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="b3733-136">La clé d’accès complet est utilisée dans un service de serveur principal sécurisé pour l’envoi de notifications et la modification d’inscriptions existantes.</span><span class="sxs-lookup"><span data-stu-id="b3733-136">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="b3733-137">Dans MainPage.xaml.cs, ajoutez la ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="b3733-137">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="b3733-138">Dans le fichier projet MainPage.xaml.cs, ajoutez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="b3733-138">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="b3733-139">Cette méthode crée une liste de catégories et utilise la classe **Notifications** pour stocker la liste dans le stockage local et inscrire les balises correspondantes auprès du Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="b3733-139">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="b3733-140">Lorsque des catégories sont modifiées, l'inscription est à nouveau créée avec les nouvelles catégories.</span><span class="sxs-lookup"><span data-stu-id="b3733-140">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="b3733-141">Votre application peut désormais stocker un ensemble de catégories dans le stockage local sur l’appareil et s’inscrire auprès du hub de notification lorsque l’utilisateur modifie la sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="b3733-141">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="b3733-142">Inscription à des notifications</span><span class="sxs-lookup"><span data-stu-id="b3733-142">Register for notifications</span></span>
<span data-ttu-id="b3733-143">Les étapes suivantes permettent l’inscription auprès du hub de notification au démarrage en utilisant les catégories qui ont été stockées dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="b3733-143">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b3733-144">L'URI de canal affecté par le Service de notifications Push Windows (WNS) pouvant changer à n'importe quel moment, vous devez vous inscrire fréquemment aux notifications afin d'éviter les défaillances de notification.</span><span class="sxs-lookup"><span data-stu-id="b3733-144">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="b3733-145">Cet exemple s’inscrit aux notifications chaque fois que l’application démarre.</span><span class="sxs-lookup"><span data-stu-id="b3733-145">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="b3733-146">Pour les applications exécutées fréquemment, plus d'une fois par jour, vous pouvez probablement ignorer l'inscription afin de préserver la bande passante si moins d'un jour s'est écoulé depuis l'inscription précédente.</span><span class="sxs-lookup"><span data-stu-id="b3733-146">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="b3733-147">Ouvrez le fichier App.xaml.cs et mettez à jour la méthode **InitNotificationsAsync** pour utiliser la classe `notifications` pour vous abonner en fonction des catégories.</span><span class="sxs-lookup"><span data-stu-id="b3733-147">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="b3733-148">Cette opération garantit que chaque fois que l'application démarre, elle récupère les catégories du stockage local et demande une inscription pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="b3733-148">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="b3733-149">La méthode **InitNotificationsAsync** a été créée dans le cadre du didacticiel [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="b3733-149">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="b3733-150">Dans le fichier projet MainPage.xaml.cs, ajoutez le code suivant à la méthode *OnNavigatedTo* :</span><span class="sxs-lookup"><span data-stu-id="b3733-150">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="b3733-151">Cette opération met la page principale à jour selon le statut des catégories enregistrées précédemment.</span><span class="sxs-lookup"><span data-stu-id="b3733-151">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="b3733-152">L'application est désormais terminée et peut stocker un ensemble de catégories dans le stockage local de l'appareil utilisé pour s'inscrire auprès du Notification Hub lorsque l'utilisateur modifie la sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="b3733-152">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="b3733-153">Ensuite, nous allons définir un serveur principal qui peut envoyer des notifications de catégorie à cette application.</span><span class="sxs-lookup"><span data-stu-id="b3733-153">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="b3733-154">Envoi des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="b3733-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="b3733-155">Exécution de l’application et génération de notifications</span><span class="sxs-lookup"><span data-stu-id="b3733-155">Run the app and generate notifications</span></span>
1. <span data-ttu-id="b3733-156">Dans Visual Studio, appuyez sur la touche F5 pour compiler et démarrer l’application.</span><span class="sxs-lookup"><span data-stu-id="b3733-156">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="b3733-157">Notez que l’interface utilisateur de l’application fournit un ensemble de bascules qui vous permet de choisir les catégories auxquelles vous abonner.</span><span class="sxs-lookup"><span data-stu-id="b3733-157">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="b3733-158">Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.</span><span class="sxs-lookup"><span data-stu-id="b3733-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="b3733-159">L'application convertit les catégories sélectionnées en balises et demande une nouvelle inscription de l'appareil pour les balises sélectionnées depuis le Notification Hub.</span><span class="sxs-lookup"><span data-stu-id="b3733-159">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="b3733-160">Les catégories inscrites sont renvoyées et affichées dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b3733-160">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="b3733-161">Envoyez une nouvelle notification depuis le serveur principal de l’une des manières suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3733-161">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="b3733-162">**Application console :** démarrez l'application console.</span><span class="sxs-lookup"><span data-stu-id="b3733-162">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="b3733-163">**Java/PHP :** exécutez votre application/script.</span><span class="sxs-lookup"><span data-stu-id="b3733-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="b3733-164">Les notifications pour les catégories sélectionnées apparaissent comme notifications toast.</span><span class="sxs-lookup"><span data-stu-id="b3733-164">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="b3733-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3733-165">Next steps</span></span>
<span data-ttu-id="b3733-166">Dans ce didacticiel, nous avons appris à diffuser les dernières nouvelles par catégorie.</span><span class="sxs-lookup"><span data-stu-id="b3733-166">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="b3733-167">Envisagez de suivre un des didacticiels suivants qui soulignent d’autres scénarios avancés Notification Hubs :</span><span class="sxs-lookup"><span data-stu-id="b3733-167">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="b3733-168">[Utilisation de Notification Hubs pour diffuser les dernières nouvelles localisées]</span><span class="sxs-lookup"><span data-stu-id="b3733-168">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="b3733-169">Apprenez à développer l’application relative aux dernières nouvelles pour permettre l’envoi de notifications localisées.</span><span class="sxs-lookup"><span data-stu-id="b3733-169">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
<span data-ttu-id="b3733-170">[Utilisation de Notification Hubs pour diffuser les dernières nouvelles localisées]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="b3733-170">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
