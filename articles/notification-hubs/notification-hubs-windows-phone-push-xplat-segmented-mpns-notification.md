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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="1b71e-103">Utilisez toosend concentrateurs de Notification dernières actualités</span><span class="sxs-lookup"><span data-stu-id="1b71e-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="1b71e-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="1b71e-104">Overview</span></span>
<span data-ttu-id="1b71e-105">Cette rubrique vous montre comment toouse Azure Notification Hubs toobroadcast avec rupture nouvelles notifications tooa Windows Phone 8.0/8.1 Silverlight application.</span><span class="sxs-lookup"><span data-stu-id="1b71e-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="1b71e-106">Si vous ciblez Windows Store ou Windows Phone 8.1, consultez tootoohello [Windows universel](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span><span class="sxs-lookup"><span data-stu-id="1b71e-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="1b71e-107">Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="1b71e-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="1b71e-108">Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications pour des ventilateurs de musique, etc..</span><span class="sxs-lookup"><span data-stu-id="1b71e-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="1b71e-109">Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="1b71e-110">Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="1b71e-111">Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance.</span><span class="sxs-lookup"><span data-stu-id="1b71e-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="1b71e-112">Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="1b71e-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b71e-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1b71e-113">Prerequisites</span></span>
<span data-ttu-id="1b71e-114">Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="1b71e-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="1b71e-115">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [prise en main des concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="1b71e-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="1b71e-116">Ajouter une application de toohello de sélection de catégorie</span><span class="sxs-lookup"><span data-stu-id="1b71e-116">Add category selection toohello app</span></span>
<span data-ttu-id="1b71e-117">première étape de Hello est tooadd hello UI éléments tooyour principale page existante qui permettent de hello utilisateur tooselect catégories tooregister.</span><span class="sxs-lookup"><span data-stu-id="1b71e-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="1b71e-118">catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="1b71e-119">Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="1b71e-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="1b71e-120">Ouvrir le fichier de projet hello MainPage.xaml, puis remplacez hello **grille** éléments nommés `TitlePanel` et `ContentPanel` avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="1b71e-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
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
2. <span data-ttu-id="1b71e-121">Dans le projet de hello, créez une nouvelle classe nommée **Notifications**, ajouter hello **public** modificateur toohello définition de classe, puis ajoutez hello suivant **à l’aide de** instructions nouveau fichier de code toohello :</span><span class="sxs-lookup"><span data-stu-id="1b71e-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="1b71e-122">De code suivant de hello de copie dans hello nouvelle **Notifications** classe :</span><span class="sxs-lookup"><span data-stu-id="1b71e-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
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

    <span data-ttu-id="1b71e-123">Cette classe utilise hello isolé stockage toostore hello catégories de news que cet appareil est tooreceive.</span><span class="sxs-lookup"><span data-stu-id="1b71e-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="1b71e-124">Il contient également des tooregister des méthodes pour ces catégories en utilisant un [modèle](notification-hubs-templates-cross-platform-push-messages.md) l’enregistrement des notifications.</span><span class="sxs-lookup"><span data-stu-id="1b71e-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="1b71e-125">Dans le fichier de projet App.xaml.cs hello, ajouter hello suivant propriété toohello **application** classe.</span><span class="sxs-lookup"><span data-stu-id="1b71e-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="1b71e-126">Remplacez hello `<hub name>` et `<connection string with listen access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature* que vous avez obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="1b71e-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="1b71e-127">Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="1b71e-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="1b71e-128">Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="1b71e-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="1b71e-129">clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="1b71e-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="1b71e-130">Dans votre MainPage.xaml.cs, ajoutez hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="1b71e-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="1b71e-131">Dans le fichier de projet hello MainPage.xaml.cs, ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="1b71e-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="1b71e-132">Cette méthode crée une liste de catégories et les utilisations hello **Notifications** classe liste de hello toostore dans le stockage local hello et inscrire les balises correspondantes hello avec votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="1b71e-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="1b71e-133">Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="1b71e-134">Votre application est maintenant en mesure de toostore un ensemble de catégories dans le stockage local sur l’appareil de hello ; inscrire auprès de hub de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories</span><span class="sxs-lookup"><span data-stu-id="1b71e-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="1b71e-135">Inscription à des notifications</span><span class="sxs-lookup"><span data-stu-id="1b71e-135">Register for notifications</span></span>
<span data-ttu-id="1b71e-136">Ces étapes auprès du hub de notification hello au démarrage à l’aide de catégories hello qui ont été stockés dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="1b71e-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="1b71e-137">Étant donné que le canal hello URI affecté par hello services de notifications Push Microsoft (MPNS) peut changer à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification.</span><span class="sxs-lookup"><span data-stu-id="1b71e-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="1b71e-138">Cet exemple s’inscrit aux notifications à chaque démarrage de cette application hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="1b71e-139">Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.</span><span class="sxs-lookup"><span data-stu-id="1b71e-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="1b71e-140">Ouvrez le fichier App.xaml.cs de hello et ajouter hello **async** modificateur trop**Application_Launching** méthode replace hello concentrateurs de Notification d’enregistrement code et que vous avez ajouté dans [prise en main des concentrateurs de Notification] avec hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="1b71e-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="1b71e-141">Cela permet de s’assurer que chaque démarrage d’application hello, il récupère les catégories hello du stockage local et un enregistrement pour ces catégories de demande.</span><span class="sxs-lookup"><span data-stu-id="1b71e-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="1b71e-142">Dans le fichier de projet hello MainPage.xaml.cs, ajouter hello suivant le code qui implémente hello **OnNavigatedTo** méthode :</span><span class="sxs-lookup"><span data-stu-id="1b71e-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="1b71e-143">Cette page principale de hello mises à jour selon l’état hello précédemment enregistré des catégories.</span><span class="sxs-lookup"><span data-stu-id="1b71e-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="1b71e-144">application Hello est maintenant terminée et permettre de stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="1b71e-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="1b71e-145">Ensuite, nous allons définir un serveur principal qui peut envoyer catégorie notifications toothis application.</span><span class="sxs-lookup"><span data-stu-id="1b71e-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="1b71e-146">Envoi des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="1b71e-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="1b71e-147">Exécutez l’application hello et générer des notifications</span><span class="sxs-lookup"><span data-stu-id="1b71e-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="1b71e-148">Dans Visual Studio, appuyez sur F5 toocompile et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="1b71e-149">Notez que cette application hello de que l’interface utilisateur fournit un ensemble bascule qui permet de choisir toosubscribe de catégories hello pour.</span><span class="sxs-lookup"><span data-stu-id="1b71e-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="1b71e-150">Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.</span><span class="sxs-lookup"><span data-stu-id="1b71e-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="1b71e-151">application Hello convertit les catégories de hello sélectionné en balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="1b71e-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="1b71e-152">Hello catégories inscrits sont retournés et affichés dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1b71e-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="1b71e-153">Après avoir reçu une confirmation que vos catégories ont été abonnement terminé, exécutez hello console application toosend des notifications pour chaque catégories.</span><span class="sxs-lookup"><span data-stu-id="1b71e-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="1b71e-154">Vérifiez que vous recevez uniquement une notification pour les catégories hello à que vous êtes abonné.</span><span class="sxs-lookup"><span data-stu-id="1b71e-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="1b71e-155">Vous avez terminé cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="1b71e-155">You have completed this topic.</span></span>

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

