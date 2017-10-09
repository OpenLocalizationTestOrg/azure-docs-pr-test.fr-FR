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
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="2d4cd-104">Notification des utilisateurs via Azure Notification Hubs avec service principal .NET</span><span class="sxs-lookup"><span data-stu-id="2d4cd-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="2d4cd-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2d4cd-105">Overview</span></span>
<span data-ttu-id="2d4cd-106">Prise en charge des notifications push dans Azure vous permet de tooaccess un facile à utiliser, multiplateforme et infrastructure par émission de données à grande échelle, ce qui simplifie considérablement l’implémentation hello de notifications push pour les applications consommateur et d’entreprise mobile plateformes.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="2d4cd-107">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push utilisateur de notifications tooa application spécifique sur un périphérique spécifique.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="2d4cd-108">Un serveur principal ASP.NET WebAPI est utilisé tooauthenticate clients.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="2d4cd-109">À l’aide de hello authentifié l’utilisateur du client, et étiquette est automatiquement ajoutée par l’inscription de toonotification hello principale.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="2d4cd-110">Cette balise sera toosend utilisé par les notifications de toogenerate hello principal pour un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="2d4cd-111">Pour plus d’informations sur l’inscription aux notifications à l’aide d’un serveur principal d’application, consultez la rubrique de guide de hello [l’inscription à partir de votre serveur principal d’application](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d4cd-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="2d4cd-112">Ce didacticiel s’appuie sur le concentrateur de notification hello et de projet que vous avez créé dans hello [prise en main des concentrateurs de Notification] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="2d4cd-113">Ce didacticiel est également toohello requis de hello [Secure Push] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="2d4cd-114">Après avoir terminé les étapes de hello dans ce didacticiel, vous pouvez passer toohello [Secure Push] didacticiel qui montre comment toomodify hello de code dans ce didacticiel toosend une notification push en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2d4cd-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="2d4cd-115">Before you begin</span></span>
<span data-ttu-id="2d4cd-116">Nous accordons de l’importance à vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-116">We do take your feedback seriously.</span></span> <span data-ttu-id="2d4cd-117">Si vous avez des difficultés à la fin de cette rubrique, ou des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="2d4cd-118">code Hello terminée pour ce didacticiel se trouve sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="2d4cd-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2d4cd-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2d4cd-119">Prerequisites</span></span>
<span data-ttu-id="2d4cd-120">Avant de commencer ce didacticiel, vous devez suivre les didacticiels Mobile Services suivants :</span><span class="sxs-lookup"><span data-stu-id="2d4cd-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="2d4cd-121">[prise en main des concentrateurs de Notification]</span><span class="sxs-lookup"><span data-stu-id="2d4cd-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="2d4cd-122">Vous créez votre hub de notification et réservez le nom de l’application hello et enregistrez les notifications de tooreceive dans ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="2d4cd-123">Ce didacticiel part du principe que vous avez déjà effectué ces étapes.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="2d4cd-124">Dans le cas contraire, suivez les étapes de hello dans [mise en route avec Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); plus précisément, hello sections [inscrire votre application pour hello du Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) et [configurer votre concentrateur de Notification](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="2d4cd-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="2d4cd-125">En particulier, assurez-vous que vous avez entré hello **SID du Package** et **clé secrète Client** valeurs dans le portail de hello hello **configurer** onglet votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="2d4cd-126">Cette procédure de configuration est décrite dans la section de hello [configurer votre concentrateur de Notification](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="2d4cd-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="2d4cd-127">Il s’agit d’une étape importante : si les informations d’identification hello sur le portail hello ne correspondent pas celles spécifiées pour le nom de l’application hello choisie, les notifications de push hello ne réussissent pas.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="2d4cd-128">Si vous utilisez des applications mobiles dans Azure App Service en tant que votre service principal, consultez hello [version des applications mobiles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="2d4cd-129">Mettre à jour le code hello pour le projet de client hello</span><span class="sxs-lookup"><span data-stu-id="2d4cd-129">Update hello code for hello client project</span></span>
<span data-ttu-id="2d4cd-130">Dans cette section, vous mettez à jour code hello dans le projet hello pour hello [prise en main des concentrateurs de Notification] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="2d4cd-131">Hello doit déjà être associée au magasin hello et configuré pour votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="2d4cd-132">Dans cette section, vous ajouter code toocall hello WebAPI serveur principal et l’utiliser pour l’inscription et l’envoi de notifications.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="2d4cd-133">Dans Visual Studio, ouvrez la solution de hello de hello vous avez créé pour hello [prise en main des concentrateurs de Notification] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="2d4cd-134">Dans l’Explorateur de solutions, cliquez sur hello **(Windows 8.1)** de projet, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="2d4cd-135">Dans la partie gauche hello, cliquez sur **Online**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="2d4cd-136">Bonjour **recherche** , tapez **Http Client**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="2d4cd-137">Dans la liste des résultats hello, cliquez sur **Microsoft HTTP Client Libraries**, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="2d4cd-138">Terminer l’installation de hello.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-138">Complete hello installation.</span></span>
6. <span data-ttu-id="2d4cd-139">Dans hello NuGet **recherche** , tapez **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="2d4cd-140">Installer hello **Json.NET** package et la fenêtre du Gestionnaire de Package NuGet hello puis fermer.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="2d4cd-141">Répétez les étapes de hello ci-dessus pour hello **(8.1 de Windows Phone)** hello tooinstall de projet **JSON.NET** package NuGet pour le projet Windows Phone de hello.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="2d4cd-142">Dans l’Explorateur de solutions, Bonjour **(Windows 8.1)** de projet, double-cliquez sur **MainPage.xaml** tooopen dans l’éditeur de Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="2d4cd-143">Bonjour **MainPage.xaml** code XML, remplacer hello `<Grid>` section avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="2d4cd-144">Ce code ajoute une zone de texte Nom d’utilisateur et mot de passe utilisateur de hello authentifiera avec.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="2d4cd-145">Il ajoute également des zones de texte pour le message de notification hello et étiquette de nom d’utilisateur hello qui doit recevoir une notification hello :</span><span class="sxs-lookup"><span data-stu-id="2d4cd-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
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
10. <span data-ttu-id="2d4cd-146">Dans l’Explorateur de solutions, Bonjour **(8.1 de Windows Phone)** projet, ouvrez **MainPage.xaml** et remplacer hello Windows Phone 8.1 `<Grid>` section avec ce même code ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="2d4cd-147">interface de Hello doit ressembler toowhats comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="2d4cd-148">Dans l’Explorateur de solutions, ouvrez hello **MainPage.xaml.cs** fichier hello **(Windows 8.1)** et **(8.1 de Windows Phone)** projets.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="2d4cd-149">Ajoutez hello suit `using` instructions haut hello des deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="2d4cd-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="2d4cd-150">Dans **MainPage.xaml.cs** pour hello **(Windows 8.1)** et **(8.1 de Windows Phone)** projets, ajouter hello suivant membre toohello `MainPage` classe.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="2d4cd-151">Être vraiment tooreplace `<Enter Your Backend Endpoint>` avec hello votre point de terminaison principal réel obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="2d4cd-152">Par exemple, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="2d4cd-153">Ajoutez le code hello sous la classe MainPage toohello **MainPage.xaml.cs** pour hello **(Windows 8.1)** et **(8.1 de Windows Phone)** projets.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="2d4cd-154">Hello `PushClick` méthode est hello Gestionnaire click pour hello **envoi Push** bouton.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="2d4cd-155">Il appelle hello principal tootrigger un tooall de notification des appareils avec une étiquette de nom d’utilisateur qui correspond à hello `to_tag` paramètre.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="2d4cd-156">message de notification Hello est envoyé en tant que contenu JSON dans le corps de la demande hello.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="2d4cd-157">Hello `LoginAndRegisterClick` méthode est hello Gestionnaire click pour hello **connectez-vous et inscrivez** bouton.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="2d4cd-158">Il stocke basic de hello jeton d’authentification dans le stockage local (Notez que cela représente n’importe quel jeton utilise de votre schéma d’authentification), puis utilise `RegisterClient` tooregister pour les notifications à l’aide de hello principal.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

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



1. <span data-ttu-id="2d4cd-159">Dans l’Explorateur de solutions, sous hello **Shared** projet, ouvrez hello **App.xaml.cs** fichier.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="2d4cd-160">Rechercher les appels hello trop`InitNotificationsAsync()` Bonjour `OnLaunched()` Gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="2d4cd-161">Commentez ou supprimer les appels hello trop`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="2d4cd-162">Gestionnaire de bouton Hello ajoutée ci-dessus initialisera les inscriptions de notification.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="2d4cd-163">Dans l’Explorateur de solutions, cliquez sur hello **Shared** de projet, puis cliquez sur **ajouter**, puis cliquez sur **classe**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="2d4cd-164">Nom de classe hello **RegisterClient.cs**, puis cliquez sur **OK** classe hello de toogenerate.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="2d4cd-165">Cette classe encapsule hello REST appelle toocontact requis hello serveur principal d’application, dans tooregister d’ordre pour les notifications push.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="2d4cd-166">Il stocke également localement hello *registrationIds* créé par hello Hub de Notification comme détaillé dans [l’inscription à partir de votre serveur principal d’application](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="2d4cd-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="2d4cd-167">Notez qu’il utilise un jeton d’autorisation stocké dans le stockage local lorsque vous cliquez sur hello **connectez-vous et inscrivez** bouton.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="2d4cd-168">Ajoutez hello suit `using` instructions haut hello du fichier de RegisterClient.cs hello :</span><span class="sxs-lookup"><span data-stu-id="2d4cd-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="2d4cd-169">Ajouter hello suivant du code à l’intérieur de hello `RegisterClient` définition de classe.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="2d4cd-170">Enregistrez toutes vos modifications.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="2d4cd-171">Hello Application de test</span><span class="sxs-lookup"><span data-stu-id="2d4cd-171">Testing hello Application</span></span>
1. <span data-ttu-id="2d4cd-172">Lancez l’application hello sur Windows 8.1 et Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="2d4cd-173">Pour Windows Phone 8.1, vous pouvez exécuter les instance hello dans l’émulateur de hello ou un appareil réel.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="2d4cd-174">Dans l’instance de hello Windows 8.1 d’application hello, entrez un **nom d’utilisateur** et **mot de passe** comme indiqué dans l’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="2d4cd-175">Il doit différer de nom d’utilisateur hello et le mot de passe entré sur Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="2d4cd-176">Cliquez sur **Se connecter et s’inscrire** et vérifiez le contenu de la boîte de dialogue indiquant que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="2d4cd-177">Cela permettra également hello **envoi Push** bouton.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="2d4cd-178">Sur l’instance de hello Windows Phone 8.1, entrez une chaîne de nom d’utilisateur dans les deux hello **nom d’utilisateur** et **mot de passe** champs puis cliquez sur **connexion et inscription**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="2d4cd-179">Ensuite, dans hello **balise de nom d’utilisateur destinataire** , entrez le nom d’utilisateur hello inscrit sur Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="2d4cd-180">Entrez un message de notification, puis cliquez sur **Envoyer des notifications Push**.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="2d4cd-181">Seuls les appareils hello qui ont été inscrits auprès de balise de nom d’utilisateur hello recevoir message de notification de hello.</span><span class="sxs-lookup"><span data-stu-id="2d4cd-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="2d4cd-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2d4cd-182">Next Steps</span></span>
* <span data-ttu-id="2d4cd-183">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, consultez [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="2d4cd-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="2d4cd-184">consultez des concentrateurs de Notification toouse, toolearn plus sur la façon [des conseils de concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="2d4cd-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

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
