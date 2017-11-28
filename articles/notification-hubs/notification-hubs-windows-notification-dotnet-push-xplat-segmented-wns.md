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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="db143-103">Utilisez toosend concentrateurs de Notification dernières actualités</span><span class="sxs-lookup"><span data-stu-id="db143-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="db143-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="db143-104">Overview</span></span>
<span data-ttu-id="db143-105">Cette rubrique vous montre comment toobroadcast d’Azure Notification Hubs toouse dernières nouvelles notifications tooa Windows Store ou Windows Phone 8.1 (non Silverlight).</span><span class="sxs-lookup"><span data-stu-id="db143-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="db143-106">Si vous ciblez Windows Phone 8.1 Silverlight, consultez toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span><span class="sxs-lookup"><span data-stu-id="db143-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="db143-107">Lorsque vous avez terminé, vous être en mesure de tooregister la rupture des catégories d’actualités que vous intéressez et recevoir des notifications push uniquement pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="db143-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="db143-108">Ce scénario est courant pour de nombreuses applications où les notifications ont toogroups toobe envoyé d’utilisateurs qui ont précédemment été déclaré intérêt, par exemple, lecteur RSS, les applications de ventilateurs de musique et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="db143-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="db143-109">Scénarios de diffusion sont activés en incluant un ou plusieurs *balises* lors de la création d’un enregistrement dans le hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="db143-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="db143-110">Lorsque les notifications sont envoyées tooa balise, tous les appareils qui ont inscrit pour la balise de hello seront recevoir une notification de hello.</span><span class="sxs-lookup"><span data-stu-id="db143-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="db143-111">Étant donné que les balises sont simplement des chaînes, ils n’ont pas toobe configuré à l’avance.</span><span class="sxs-lookup"><span data-stu-id="db143-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="db143-112">Pour plus d’informations sur les balises, consultez trop[le routage des concentrateurs de Notification et les Expressions de balises](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="db143-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="db143-113">Les projets Windows Store et Windows Phone version 8.1 et versions antérieures ne sont pas pris en charge dans Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="db143-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="db143-114">Pour en savoir plus, consultez [Plateforme cible et compatibilité dans Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="db143-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db143-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="db143-115">Prerequisites</span></span>
<span data-ttu-id="db143-116">Cette rubrique s’appuie sur l’application hello que vous avez créé dans [prise en main des concentrateurs de Notification][get-started].</span><span class="sxs-lookup"><span data-stu-id="db143-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="db143-117">Avant de commencer ce didacticiel, vous devez suivre celui intitulé [Prise en main de Notification Hubs][get-started].</span><span class="sxs-lookup"><span data-stu-id="db143-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="db143-118">Ajouter une application de toohello de sélection de catégorie</span><span class="sxs-lookup"><span data-stu-id="db143-118">Add category selection toohello app</span></span>
<span data-ttu-id="db143-119">première étape de Hello est tooadd hello UI éléments tooyour principale page existante qui permettent de hello utilisateur tooselect catégories tooregister.</span><span class="sxs-lookup"><span data-stu-id="db143-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="db143-120">catégories de Hello sélectionnées par un utilisateur sont stockées sur l’appareil de hello.</span><span class="sxs-lookup"><span data-stu-id="db143-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="db143-121">Au démarrage de l’application hello, une inscription de périphérique est créée dans votre concentrateur de notification avec les catégories de hello sélectionné sous forme de balises.</span><span class="sxs-lookup"><span data-stu-id="db143-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="db143-122">Ouvrez le fichier de projet hello MainPage.xaml, puis hello copie suivant code Bonjour **grille** élément :</span><span class="sxs-lookup"><span data-stu-id="db143-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
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
2. <span data-ttu-id="db143-123">Cliquez avec le bouton droit sur hello **Shared** de projet et ajoutez une nouvelle classe nommée **Notifications**, ajouter hello **public** modificateur toohello définition de classe, puis ajoutez hello suivant **à l’aide de** instructions toohello nouveau fichier de code :</span><span class="sxs-lookup"><span data-stu-id="db143-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="db143-124">De code suivant de hello de copie dans hello nouvelle **Notifications** classe :</span><span class="sxs-lookup"><span data-stu-id="db143-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
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
   
    <span data-ttu-id="db143-125">Cette classe utilise hello stockage local des catégories de hello toostore de news que ce périphérique a tooreceive.</span><span class="sxs-lookup"><span data-stu-id="db143-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="db143-126">Notez que, au lieu de l’appel hello *RegisterNativeAsync* méthode que nous appelons *RegisterTemplateAsync* tooregister pour les catégories de hello à l’aide d’une inscription de modèle.</span><span class="sxs-lookup"><span data-stu-id="db143-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="db143-127">Nous avons également fournir un nom pour le modèle hello (« simpleWNSTemplateExample »), car nous souhaitions tooregister plusieurs modèles (par exemple un pour les notifications de toast) et l’autre pour les vignettes et nous devons tooname dans tooupdate en mesure de toobe de commande ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="db143-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="db143-128">Notez que si un appareil inscrit plusieurs modèles avec hello même balise, un message entrant de ciblage que balise entraîne plusieurs remettre les notifications d’appareil toohello (un pour chaque modèle).</span><span class="sxs-lookup"><span data-stu-id="db143-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="db143-129">Ce comportement est utile lorsque hello message logique même a tooresult dans plusieurs notifications visuelles, par exemple avec un badge et un toast dans une application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="db143-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="db143-130">Pour plus d’informations sur les modèles, consultez la rubrique [Modèles](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="db143-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="db143-131">Dans le fichier de projet App.xaml.cs hello, ajouter hello suivant propriété toohello **application** classe :</span><span class="sxs-lookup"><span data-stu-id="db143-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="db143-132">Cette propriété est utilisée toocreate et accès un **Notifications** instance.</span><span class="sxs-lookup"><span data-stu-id="db143-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="db143-133">Bonjour au-dessus de code, remplacez hello `<hub name>` et `<connection string with listen access>` des espaces réservés avec votre notification hub hello et nom de chaîne de connexion pour *DefaultListenSharedAccessSignature* que vous avez obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="db143-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="db143-134">Étant donné que les informations d’identification qui sont distribuées avec une application cliente ne sont pas sécurisées en règle générale, vous devez distribuer clé hello pour l’accès en écoute avec votre application cliente.</span><span class="sxs-lookup"><span data-stu-id="db143-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="db143-135">Écouter access active que tooregister de votre application pour les notifications, mais les inscriptions existantes ne peut pas être modifié et des notifications ne peut pas être envoyées.</span><span class="sxs-lookup"><span data-stu-id="db143-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="db143-136">clé d’accès complet de Hello est utilisée dans un service principal sécurisé pour envoyer des notifications et la modification des enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="db143-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="db143-137">Dans votre MainPage.xaml.cs, ajoutez hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="db143-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="db143-138">Dans le fichier de projet hello MainPage.xaml.cs, ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="db143-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="db143-139">Cette méthode crée une liste de catégories et les utilisations hello **Notifications** classe liste de hello toostore dans le stockage local hello et inscrire les balises correspondantes hello avec votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="db143-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="db143-140">Si des catégories sont modifiées, l’inscription de hello est recréée avec les nouvelles catégories de hello.</span><span class="sxs-lookup"><span data-stu-id="db143-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="db143-141">Votre application est maintenant en mesure de toostore un ensemble de catégories dans le stockage local sur l’appareil de hello ; inscrire auprès de hub de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories</span><span class="sxs-lookup"><span data-stu-id="db143-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="db143-142">Inscription à des notifications</span><span class="sxs-lookup"><span data-stu-id="db143-142">Register for notifications</span></span>
<span data-ttu-id="db143-143">Ces étapes auprès du hub de notification hello au démarrage à l’aide de catégories hello qui ont été stockés dans le stockage local.</span><span class="sxs-lookup"><span data-stu-id="db143-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="db143-144">Étant donné que le canal hello URI affecté par hello Service de Notification de Windows (WNS) permettre changer à tout moment, vous devez inscrire pour les notifications fréquemment tooavoid les échecs de notification.</span><span class="sxs-lookup"><span data-stu-id="db143-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="db143-145">Cet exemple inscrit pour la notification chaque fois que cette application hello démarre.</span><span class="sxs-lookup"><span data-stu-id="db143-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="db143-146">Pour les applications qui sont exécutées fréquemment, plusieurs fois par jour, vous pouvez probablement ignorer la bande passante de l’inscription toopreserve si l’enregistrement précédent de hello remonte à moins d’un jour.</span><span class="sxs-lookup"><span data-stu-id="db143-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="db143-147">Hello de fichier et de mise à jour de App.xaml.cs hello ouvrir **InitNotificationsAsync** hello toouse de méthode `notifications` toosubscribe de classe en fonction de catégories.</span><span class="sxs-lookup"><span data-stu-id="db143-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="db143-148">Cela permet de s’assurer que chaque démarrage d’application hello, il récupère les catégories hello du stockage local et demande une inscription pour ces catégories.</span><span class="sxs-lookup"><span data-stu-id="db143-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="db143-149">Hello **InitNotificationsAsync** méthode a été créée dans le cadre de hello [prise en main des concentrateurs de Notification] [ get-started] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="db143-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="db143-150">Dans le fichier de projet hello MainPage.xaml.cs, ajouter hello suivant code toohello *OnNavigatedTo* méthode :</span><span class="sxs-lookup"><span data-stu-id="db143-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="db143-151">Cette page principale de hello mises à jour selon l’état hello précédemment enregistré des catégories.</span><span class="sxs-lookup"><span data-stu-id="db143-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="db143-152">application Hello est maintenant terminée et permettre de stocker un ensemble de catégories dans tooregister de stockage local utilisé hello appareil avec un concentrateur de notification hello chaque fois que les modifications de l’utilisateur hello hello sélection des catégories.</span><span class="sxs-lookup"><span data-stu-id="db143-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="db143-153">Ensuite, nous allons définir un serveur principal qui peut envoyer catégorie notifications toothis application.</span><span class="sxs-lookup"><span data-stu-id="db143-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="db143-154">Envoi des notifications avec balises</span><span class="sxs-lookup"><span data-stu-id="db143-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="db143-155">Exécutez l’application hello et générer des notifications</span><span class="sxs-lookup"><span data-stu-id="db143-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="db143-156">Dans Visual Studio, appuyez sur F5 toocompile et démarrer l’application hello.</span><span class="sxs-lookup"><span data-stu-id="db143-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="db143-157">Notez que cette application hello de que l’interface utilisateur fournit un ensemble bascule qui permet de choisir toosubscribe de catégories hello pour.</span><span class="sxs-lookup"><span data-stu-id="db143-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="db143-158">Activez une ou plusieurs bascules de catégories, puis cliquez sur **S'abonner**.</span><span class="sxs-lookup"><span data-stu-id="db143-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="db143-159">application Hello convertit les catégories de hello sélectionné en balises et demande une nouvelle inscription de périphérique pour les balises de hello sélectionné à partir du hub de notification hello.</span><span class="sxs-lookup"><span data-stu-id="db143-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="db143-160">Hello catégories inscrits sont retournés et affichés dans une boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="db143-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="db143-161">Envoyer une nouvelle notification de back-end hello dans un des hello suivant façons :</span><span class="sxs-lookup"><span data-stu-id="db143-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="db143-162">**Application console :** démarrer l’application de console hello.</span><span class="sxs-lookup"><span data-stu-id="db143-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="db143-163">**Java/PHP :** exécutez votre application/script.</span><span class="sxs-lookup"><span data-stu-id="db143-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="db143-164">Les notifications pour les catégories de hello sélectionné s’affichent sous forme de notifications de toast.</span><span class="sxs-lookup"><span data-stu-id="db143-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="db143-165">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="db143-165">Next steps</span></span>
<span data-ttu-id="db143-166">Dans ce didacticiel, nous l’avons vu comment toobroadcast actualités par catégorie.</span><span class="sxs-lookup"><span data-stu-id="db143-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="db143-167">Envisager d’effectuer une des hello suivant des didacticiels qui mettent en évidence les autres scénarios avancés de concentrateurs de Notification :</span><span class="sxs-lookup"><span data-stu-id="db143-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="db143-168">[Utiliser les informations de dernière minute toobroadcast localisée de concentrateurs de Notification]</span><span class="sxs-lookup"><span data-stu-id="db143-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="db143-169">Découvrez comment hello tooexpand dernières actualités application tooenable envoi localisée des notifications.</span><span class="sxs-lookup"><span data-stu-id="db143-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
