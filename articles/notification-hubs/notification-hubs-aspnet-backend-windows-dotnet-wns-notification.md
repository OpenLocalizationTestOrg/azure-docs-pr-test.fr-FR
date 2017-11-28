---
title: Notification des utilisateurs via Azure Notification Hubs avec service principal .NET
description: "Découvrez comment envoyer des notifications Push sécurisées dans Azure. Exemples de code écrits en C# à l’aide de l’API .NET."
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
ms.openlocfilehash: c0b963ef661612b1a176dd8e5f01d56e61eb5acb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="f1d91-104">Notification des utilisateurs via Azure Notification Hubs avec service principal .NET</span><span class="sxs-lookup"><span data-stu-id="f1d91-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="f1d91-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="f1d91-105">Overview</span></span>
<span data-ttu-id="f1d91-106">La prise en charge des notifications Push dans Azure vous permet d’accéder à une infrastructure Push conviviale, multi-plateforme et avec montée en charge qui simplifie fortement l’implémentation des notifications Push pour les applications consommateur et entreprise pour les plateformes mobiles.</span><span class="sxs-lookup"><span data-stu-id="f1d91-106">Push notification support in Azure enables you to access an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies the implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="f1d91-107">Ce didacticiel explique comment utiliser Azure Notification Hubs pour envoyer des notifications Push à un utilisateur particulier d'une application sur un appareil spécifique.</span><span class="sxs-lookup"><span data-stu-id="f1d91-107">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a specific app user on a specific device.</span></span> <span data-ttu-id="f1d91-108">Un serveur principal WebAPI ASP.NET est utilisé pour authentifier les clients.</span><span class="sxs-lookup"><span data-stu-id="f1d91-108">An ASP.NET WebAPI backend is used to authenticate clients.</span></span> <span data-ttu-id="f1d91-109">Il ajoute automatiquement une balise à l’enregistrement des notifications en se basant sur l’utilisateur du client authentifié.</span><span class="sxs-lookup"><span data-stu-id="f1d91-109">Using the authenticated client user, and tag will be automatically added by the backend to notification registration.</span></span> <span data-ttu-id="f1d91-110">Cette balise sera utilisée pour l’envoi par le serveur principal afin de générer des notifications pour un utilisateur spécifique.</span><span class="sxs-lookup"><span data-stu-id="f1d91-110">This tag will be used to send by the backend to generate notifications for a specific user.</span></span> <span data-ttu-id="f1d91-111">Pour plus d’informations sur l’enregistrement pour les notifications à l’aide d’un serveur principal d’application, consultez la rubrique d’aide [Inscription auprès du serveur principal de votre application](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1d91-111">For more information on registering for notifications using an app backend, see the guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="f1d91-112">Ce didacticiel fait intervenir le hub de notification et le projet que vous avez créés dans le didacticiel intitulé [Prise en main de Notification Hubs] .</span><span class="sxs-lookup"><span data-stu-id="f1d91-112">This tutorial builds on the notification hub and project that you created in the [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="f1d91-113">Ce didacticiel est également un prérequis pour le didacticiel [sur les notifications Push sécurisées] .</span><span class="sxs-lookup"><span data-stu-id="f1d91-113">This tutorial is also the prerequisite to the [Secure Push] tutorial.</span></span> <span data-ttu-id="f1d91-114">Une fois que vous avez suivi la procédure de ce didacticiel, vous pouvez passer au didacticiel [sur les notifications Push sécurisées] qui explique comment modifier le code de ce didacticiel pour envoyer une notification Push en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="f1d91-114">After you have completed the steps in this tutorial, you can proceed to the [Secure Push] tutorial, which shows how to modify the code in this tutorial to send a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f1d91-115">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="f1d91-115">Before you begin</span></span>
<span data-ttu-id="f1d91-116">Nous accordons de l’importance à vos commentaires.</span><span class="sxs-lookup"><span data-stu-id="f1d91-116">We do take your feedback seriously.</span></span> <span data-ttu-id="f1d91-117">Si vous avez des difficultés à terminer cette rubrique ou si vous avez des conseils pour améliorer ce contenu, nous apprécierions que vous nous fassiez part de vos commentaires en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="f1d91-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span>

<span data-ttu-id="f1d91-118">Le code complet de ce didacticiel est disponible sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="f1d91-118">The completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f1d91-119">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f1d91-119">Prerequisites</span></span>
<span data-ttu-id="f1d91-120">Avant de commencer ce didacticiel, vous devez suivre les didacticiels Mobile Services suivants :</span><span class="sxs-lookup"><span data-stu-id="f1d91-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="f1d91-121">[Prise en main de Notification Hubs]</span><span class="sxs-lookup"><span data-stu-id="f1d91-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="f1d91-122">Ce didacticiel vous permet de créer votre concentrateur de notification, de réserver le nom de l’application et de vous inscrire pour recevoir des notifications.</span><span class="sxs-lookup"><span data-stu-id="f1d91-122">You create your notification hub and reserve the app name and register to receive notifications in this tutorial.</span></span> <span data-ttu-id="f1d91-123">Ce didacticiel part du principe que vous avez déjà effectué ces étapes.</span><span class="sxs-lookup"><span data-stu-id="f1d91-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="f1d91-124">Si ce n’est pas le cas, suivez les étapes de la rubrique [Prise en main de Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md), en particulier les sections [Inscrire votre application auprès du Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) et [Configurer votre hub de notification](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="f1d91-124">If not, please follow the steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, the sections [Register your app for the Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="f1d91-125">Vérifiez aussi que vous avez bien entré les valeurs **SID du package** et **Clé secrète client** dans le portail, sous l’onglet **Configurer** de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="f1d91-125">In particular, make sure that you have entered the **Package SID** and **Client Secret** values in the portal, in the **Configure** tab for your notification hub.</span></span> <span data-ttu-id="f1d91-126">Cette procédure de configuration est décrite dans la section [Configuration de votre concentrateur de notification](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="f1d91-126">This configuration procedure is described in the section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="f1d91-127">Il s’agit d’une étape importante : si les informations d’identification sur le portail ne correspondent pas à celles spécifiées pour le nom d’application que vous avez choisi, la notification Push ne fonctionnera pas.</span><span class="sxs-lookup"><span data-stu-id="f1d91-127">This is an important step: if the credentials on the portal do not match those specified for the app name you choose, the push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="f1d91-128">Si vous utilisez Mobile Apps dans Azure App Service comme service principal, consultez la [version Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="f1d91-128">If you are using Mobile Apps in Azure App Service as your backend service, see the [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-the-code-for-the-client-project"></a><span data-ttu-id="f1d91-129">Mise à jour du code pour le projet client</span><span class="sxs-lookup"><span data-stu-id="f1d91-129">Update the code for the client project</span></span>
<span data-ttu-id="f1d91-130">Dans cette section, vous allez mettre à jour le code du projet que vous avez terminé lors du didacticiel [Prise en main de Notification Hubs] .</span><span class="sxs-lookup"><span data-stu-id="f1d91-130">In this section, you update the code in the project you completed for the [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="f1d91-131">Il doit déjà être associé au magasin et configuré pour votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="f1d91-131">The should already be associated with the store and configured for your notification hub.</span></span> <span data-ttu-id="f1d91-132">Dans cette section, vous allez ajouter du code pour appeler le nouveau serveur principal WebAPI et l’utiliser pour l’enregistrement et l’envoi de notifications.</span><span class="sxs-lookup"><span data-stu-id="f1d91-132">In this section, you will add code to call the new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="f1d91-133">Dans Visual Studio, ouvrez la solution que vous avez créée lors du didacticiel [Prise en main de Notification Hubs] .</span><span class="sxs-lookup"><span data-stu-id="f1d91-133">In Visual Studio, open the the solution you created for the [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="f1d91-134">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **(Windows 8.1)**, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-134">In Solution Explorer, right-click the **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="f1d91-135">Dans la partie gauche, cliquez sur **En ligne**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-135">On the left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="f1d91-136">Dans la zone **Rechercher**, entrez **Client Http**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-136">In the **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="f1d91-137">Dans la liste de résultats, cliquez sur **Bibliothèques clientes HTTP Microsoft**, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-137">In the results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="f1d91-138">Terminez l'installation.</span><span class="sxs-lookup"><span data-stu-id="f1d91-138">Complete the installation.</span></span>
6. <span data-ttu-id="f1d91-139">De retour dans la zone **Recherche** NuGet, tapez **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-139">Back in the NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="f1d91-140">Installez le package **Json.NET** , puis fermez la fenêtre du Gestionnaire de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="f1d91-140">Install the **Json.NET** package, and then close the NuGet Package Manager window.</span></span>
7. <span data-ttu-id="f1d91-141">Répétez les étapes ci-dessus pour le projet **(Windows Phone 8.1)** afin d’installer le package NuGet **JSON.NET** pour le projet Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="f1d91-141">Repeat the steps above for the **(Windows Phone 8.1)** project to install the **JSON.NET** NuGet package for the Windows Phone project.</span></span>
8. <span data-ttu-id="f1d91-142">Dans l’Explorateur de solutions, dans le projet **(Windows 8.1)**, double-cliquez sur **MainPage.xaml** pour l’ouvrir dans l’éditeur de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f1d91-142">In Solution Explorer, in the **(Windows 8.1)** project, double-click **MainPage.xaml** to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="f1d91-143">Dans le code XML de **MainPage.xaml**, remplacez la section `<Grid>` par le code suivant.</span><span class="sxs-lookup"><span data-stu-id="f1d91-143">In the **MainPage.xaml** XML code, replace the `<Grid>` section with the following code.</span></span> <span data-ttu-id="f1d91-144">Ce code ajoute une zone de texte Nom d’utilisateur et Mot de passe pour l’authentification de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f1d91-144">This code adds a username and password textbox that the user will authenticate with.</span></span> <span data-ttu-id="f1d91-145">Il ajoute également des zones de texte pour le message de notification et la balise username qui doit recevoir la notification :</span><span class="sxs-lookup"><span data-stu-id="f1d91-145">It also adds textboxes for the notification message and the username tag that should receive the notification:</span></span>
   
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
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag To Send To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="f1d91-146">Dans l’Explorateur de solutions, dans le projet **(Windows Phone 8.1)**, ouvrez **MainPage.xaml** et remplacez la section Windows Phone 8.1 `<Grid>` par le code précédent.</span><span class="sxs-lookup"><span data-stu-id="f1d91-146">In Solution Explorer, in the **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace the Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="f1d91-147">L’interface doit ressembler à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="f1d91-147">The interface should look similar to whats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="f1d91-148">Dans l’Explorateur de solutions, ouvrez le fichier **MainPage.xaml.cs** pour les projets **(Windows 8.1)** et **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-148">In Solution Explorer, open the **MainPage.xaml.cs** file for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="f1d91-149">Ajoutez les instructions `using` suivantes au début des deux fichiers :</span><span class="sxs-lookup"><span data-stu-id="f1d91-149">Add the following `using` statements at the top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="f1d91-150">Dans **MainPage.xaml.cs** pour les projets **(Windows 8.1)** et **(Windows Phone 8.1)**, ajoutez le membre suivant à la classe `MainPage`.</span><span class="sxs-lookup"><span data-stu-id="f1d91-150">In **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add the following member to the `MainPage` class.</span></span> <span data-ttu-id="f1d91-151">Remplacez bien `<Enter Your Backend Endpoint>` par le point de terminaison réel de votre serveur principal, obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="f1d91-151">Be sure to replace `<Enter Your Backend Endpoint>` with the your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="f1d91-152">Par exemple : `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="f1d91-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="f1d91-153">Ajoutez le code ci-dessous à la classe MainPage dans **MainPage.xaml.cs** pour les projets **(Windows 8.1)** et **(Windows Phone 8.1)**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-153">Add the code below to the MainPage class in **MainPage.xaml.cs** for the **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="f1d91-154">La méthode `PushClick` correspond au gestionnaire de clic du bouton **Envoyer des notifications Push** .</span><span class="sxs-lookup"><span data-stu-id="f1d91-154">The `PushClick` method is the click handler for the **Send Push** button.</span></span> <span data-ttu-id="f1d91-155">Elle appelle le serveur principal pour déclencher une notification vers tous les appareils avec une balise de nom d’utilisateur correspondant au paramètre `to_tag` .</span><span class="sxs-lookup"><span data-stu-id="f1d91-155">It calls the backend to trigger a notification to all devices with a username tag that matches the `to_tag` parameter.</span></span> <span data-ttu-id="f1d91-156">Le message de notification est envoyé en tant que contenu JSON dans le corps de la demande.</span><span class="sxs-lookup"><span data-stu-id="f1d91-156">The notification message is sent as JSON content in the request body.</span></span>
    
    <span data-ttu-id="f1d91-157">La méthode `LoginAndRegisterClick` correspond au gestionnaire de clic du bouton **Se connecter et s’inscrire** .</span><span class="sxs-lookup"><span data-stu-id="f1d91-157">The `LoginAndRegisterClick` method is the click handler for the **Log in and register** button.</span></span> <span data-ttu-id="f1d91-158">Elle stocke le jeton d’authentification de base dans un stockage local (notez que cela représente n’importe quel jeton utilisé par votre système d’authentification), puis utilise `RegisterClient` pour l’inscription aux notifications à l’aide du serveur principal.</span><span class="sxs-lookup"><span data-stu-id="f1d91-158">It stores the basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` to register for notifications using the backend.</span></span>

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
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed to send " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // The "username:<user name>" tag gets automatically added by the message handler in the backend.
            // The tag passed here can be whatever other tags you may want to use.
            try
            {
                // The device handle used will be different depending on the device and PNS. 
                // Windows devices use the channel uri as the PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed to register with RegisterClient");
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



1. <span data-ttu-id="f1d91-159">Dans l’Explorateur de solutions, sous le projet **Partagé**, ouvrez le fichier **App.xaml.cs**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-159">In Solution Explorer, under the **Shared** project, open the **App.xaml.cs** file.</span></span> <span data-ttu-id="f1d91-160">Recherchez l’appel vers `InitNotificationsAsync()` in the `OnLaunched()` .</span><span class="sxs-lookup"><span data-stu-id="f1d91-160">Find the call to `InitNotificationsAsync()` in the `OnLaunched()` event handler.</span></span> <span data-ttu-id="f1d91-161">Commentez ou supprimez l’appel vers `InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="f1d91-161">Comment out or delete the call to `InitNotificationsAsync()`.</span></span> <span data-ttu-id="f1d91-162">Le gestionnaire de bouton ajouté précédemment initialise les inscriptions aux notifications.</span><span class="sxs-lookup"><span data-stu-id="f1d91-162">The button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="f1d91-163">Dans l’Explorateur de solutions, cliquez avec le bouton droit sur le projet **Partagé**, puis cliquez sur **Ajouter** et sur **Classe**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-163">In Solution Explorer, right-click the **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="f1d91-164">Nommez la classe **RegisterClient.cs**, puis cliquez sur **OK** pour générer la classe.</span><span class="sxs-lookup"><span data-stu-id="f1d91-164">Name the class **RegisterClient.cs**, then click **OK** to generate the class.</span></span>
   
   <span data-ttu-id="f1d91-165">Cette classe encapsule les appels REST nécessaires pour contacter le service principal de l'application et inscrire cette dernière pour les notifications Push.</span><span class="sxs-lookup"><span data-stu-id="f1d91-165">This class will wrap the REST calls required to contact the app backend, in order to register for push notifications.</span></span> <span data-ttu-id="f1d91-166">Il enregistre également en local les informations *registrationIds* créées par le hub de notification, comme expliqué dans la rubrique [Inscription auprès du serveur principal de votre application](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1d91-166">It also locally stores the *registrationIds* created by the Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="f1d91-167">Notez qu'il utilise un jeton d'autorisation qui se trouve dans le stockage local lorsque vous cliquez sur le bouton **Se connecter et s'inscrire** .</span><span class="sxs-lookup"><span data-stu-id="f1d91-167">Note that it uses an authorization token stored in local storage when you click the **Log in and register** button.</span></span>
2. <span data-ttu-id="f1d91-168">Ajoutez les instructions `using` suivantes au début du fichier RegisterClient.cs :</span><span class="sxs-lookup"><span data-stu-id="f1d91-168">Add the following `using` statements at the top of the RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="f1d91-169">Ajoutez le code suivant dans la définition de classe `RegisterClient` .</span><span class="sxs-lookup"><span data-stu-id="f1d91-169">Add the following code inside the `RegisterClient` class definition.</span></span>
   
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
4. <span data-ttu-id="f1d91-170">Enregistrez toutes vos modifications.</span><span class="sxs-lookup"><span data-stu-id="f1d91-170">Save all your changes.</span></span>

## <a name="testing-the-application"></a><span data-ttu-id="f1d91-171">Test de l’application</span><span class="sxs-lookup"><span data-stu-id="f1d91-171">Testing the Application</span></span>
1. <span data-ttu-id="f1d91-172">Lancez l’application sur Windows 8.1 et Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="f1d91-172">Launch the application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="f1d91-173">Pour Windows Phone 8.1, vous pouvez exécuter l’instance dans l’émulateur ou avec un appareil ciblé.</span><span class="sxs-lookup"><span data-stu-id="f1d91-173">For Windows Phone 8.1 you can run the instance in the emulator or an actual device.</span></span>
2. <span data-ttu-id="f1d91-174">Dans l’instance Windows 8.1 de l’application, entrez un **Nom d’utilisateur** et un **Mot de passe**, comme indiqué dans l’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f1d91-174">In the Windows 8.1 instance of the app, enter a **Username** and **Password** as shown in the screen below.</span></span> <span data-ttu-id="f1d91-175">Ces informations d’identification doivent différer du nom d’utilisateur et du mot de passe entrés sur Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="f1d91-175">It should differ from the user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="f1d91-176">Cliquez sur **Se connecter et s’inscrire** et vérifiez le contenu de la boîte de dialogue indiquant que vous êtes connecté.</span><span class="sxs-lookup"><span data-stu-id="f1d91-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="f1d91-177">Cette opération active également le bouton **Envoyer des notifications Push** .</span><span class="sxs-lookup"><span data-stu-id="f1d91-177">This will also enable the **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="f1d91-178">Sur l’instance Windows Phone 8.1, entrez une chaîne de nom d’utilisateur dans les champs **Nom d’utilisateur** et **Mot de passe**, puis cliquez sur **Se connecter et s’inscrire**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-178">On the Windows Phone 8.1 instance, enter a user name string in both the **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="f1d91-179">Puis, dans le champ **Balise de nom d’utilisateur** , entrez le nom d’utilisateur enregistré sur Windows 8.1.</span><span class="sxs-lookup"><span data-stu-id="f1d91-179">Then in the **Recipient Username Tag** field, enter the user name registered on Windows 8.1.</span></span> <span data-ttu-id="f1d91-180">Entrez un message de notification, puis cliquez sur **Envoyer des notifications Push**.</span><span class="sxs-lookup"><span data-stu-id="f1d91-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="f1d91-181">Seuls les appareils enregistrés avec la balise de nom d’utilisateur correspondant reçoivent le message de notification.</span><span class="sxs-lookup"><span data-stu-id="f1d91-181">Only the devices that have registered with the matching username tag receive the notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="f1d91-182">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f1d91-182">Next Steps</span></span>
* <span data-ttu-id="f1d91-183">Pour segmenter vos utilisateurs par groupes d'intérêt, consultez la page [Utilisation des Notification Hubs pour diffuser les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="f1d91-183">If you want to segment your users by interest groups, see [Use Notification Hubs to send breaking news].</span></span>
* <span data-ttu-id="f1d91-184">Pour en savoir plus sur l'utilisation de Notification Hubs, consultez la page [Recommandations relatives à Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="f1d91-184">To learn more about how to use Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
<span data-ttu-id="f1d91-185">[Prise en main de Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="f1d91-185">[Get started with Notification Hubs]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md</span></span>
<span data-ttu-id="f1d91-186">[sur les notifications Push sécurisées]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span><span class="sxs-lookup"><span data-stu-id="f1d91-186">[Secure Push]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md</span></span>
<span data-ttu-id="f1d91-187">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span><span class="sxs-lookup"><span data-stu-id="f1d91-187">[Use Notification Hubs to send breaking news]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md</span></span>
<span data-ttu-id="f1d91-188">[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="f1d91-188">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
