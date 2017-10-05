---
title: "Envoi de notifications Push avec Azure Notification Hubs sur Windows Phone | Microsoft Docs"
description: "Ce didacticiel vous apprend à utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Windows Phone 8 ou Windows Phone 8.1 Silverlight."
services: notification-hubs
documentationcenter: windows
keywords: notification push,notification push,push windows phone
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f0bfe81f849813d146d644b32490af657b1071b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="3ac96-104">Envoi de notifications Push avec Azure Notification Hubs sur Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3ac96-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="3ac96-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3ac96-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="3ac96-106">Pour suivre ce didacticiel, vous avez besoin d'un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="3ac96-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3ac96-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="3ac96-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3ac96-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="3ac96-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="3ac96-109">Ce didacticiel montre comment utiliser Azure Notification Hubs pour envoyer des notifications Push vers une application Windows Phone 8 ou Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="3ac96-109">This tutorial shows you how to use Azure Notification Hubs to send push notifications to a Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="3ac96-110">Si vous ciblez Windows Phone 8.1 (non-Silverlight), reportez-vous à la version [Windows Universel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) .</span><span class="sxs-lookup"><span data-stu-id="3ac96-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer to the [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="3ac96-111">Ce didacticiel vous apprend à créer une application Windows Phone 8 vide qui reçoit des notifications Push au moyen du Service de notifications Push Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="3ac96-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using the Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="3ac96-112">Une fois l’opération terminée, vous pouvez utiliser votre hub de notification pour diffuser des notifications Push sur tous les appareils exécutant votre application.</span><span class="sxs-lookup"><span data-stu-id="3ac96-112">When you're finished, you'll be able to use your notification hub to broadcast push notifications to all the devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="3ac96-113">Le kit de développement logiciel (SDK) Windows Phone Notification Hubs ne prend pas en charge l’utilisation des services WNS avec les applications Silverlight Windows Phone 8.1.</span><span class="sxs-lookup"><span data-stu-id="3ac96-113">The Notification Hubs Windows Phone SDK does not support using the Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="3ac96-114">Pour utiliser WNS (et non MPNS) avec les applications Windows Phone 8.1 Silverlight, suivez le [didacticiel Notification Hubs - Windows Phone Silverlight], qui s’appuie sur des API REST.</span><span class="sxs-lookup"><span data-stu-id="3ac96-114">To use WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow the [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="3ac96-115">Ce didacticiel présente un scénario de diffusion simple avec Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="3ac96-115">The tutorial demonstrates the simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ac96-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="3ac96-116">Prerequisites</span></span>
<span data-ttu-id="3ac96-117">Ce didacticiel requiert les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="3ac96-117">This tutorial requires the following:</span></span>

* <span data-ttu-id="3ac96-118">[Visual Studio 2012 Express pour Windows Phone]ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="3ac96-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="3ac96-119">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels concernant les Notification Hubs pour les applications Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="3ac96-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="3ac96-120">Création de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="3ac96-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="3ac96-121">Sous <i>Paramètres</i>, cliquez sur la section <b>Services de notification</b>, cliquez sur <b>Windows Phone (MPNS)</b>, puis cochez la case <b>Activez des notifications Push non authentifiées</b>.</span><span class="sxs-lookup"><span data-stu-id="3ac96-121">Click the <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click the <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portail Azure - Activez les notifications Push non authentifiées](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="3ac96-123">Le concentrateur est maintenant créé et configuré pour envoyer une notification non authentifiée pour Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="3ac96-123">Your hub is now created and configured to send unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="3ac96-124">Ce didacticiel utilise MPNS en mode non authentifié.</span><span class="sxs-lookup"><span data-stu-id="3ac96-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="3ac96-125">Le mode MPNS non authentifié est assorti de restrictions sur les notifications que vous pouvez envoyer à chaque canal.</span><span class="sxs-lookup"><span data-stu-id="3ac96-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send to each channel.</span></span> <span data-ttu-id="3ac96-126">Notification Hubs prend en charge le [mode authentifié MPNS](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) en vous permettant de télécharger votre certificat.</span><span class="sxs-lookup"><span data-stu-id="3ac96-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you to upload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-to-the-notification-hub"></a><span data-ttu-id="3ac96-127">Connexion de votre application au hub de notification</span><span class="sxs-lookup"><span data-stu-id="3ac96-127">Connecting your app to the notification hub</span></span>
1. <span data-ttu-id="3ac96-128">Dans Visual Studio, créez une application Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="3ac96-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="3ac96-129">Dans Visual Studio 2013 Update 2 ou version ultérieure, vous créez plutôt une application Silverlight Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="3ac96-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - Nouveau projet - Application vide - Windows Phone Silverlight][11]
2. <span data-ttu-id="3ac96-131">Dans Visual Studio, cliquez avec le bouton droit sur la solution, puis cliquez sur **Gérer les packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="3ac96-131">In Visual Studio, right-click the solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="3ac96-132">La boîte de dialogue **Gérer les packages NuGet** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="3ac96-132">This displays the **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="3ac96-133">Recherchez `WindowsAzure.Messaging.Managed` , puis cliquez sur **Installer**et acceptez les conditions d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="3ac96-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept the terms of use.</span></span>
   
    ![Visual Studio - Gestionnaire de packages NuGet][20]
   
    <span data-ttu-id="3ac96-135">Une référence à la bibliothèque Azure Messaging pour Windows est alors téléchargée, installée et ajoutée à l’aide du <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">package NuGet WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="3ac96-135">This downloads, installs, and adds a reference to the Azure Messaging library for Windows by using the <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="3ac96-136">Ouvrez le fichier App.xaml.cs et ajoutez les instructions `using` suivantes :</span><span class="sxs-lookup"><span data-stu-id="3ac96-136">Open the file App.xaml.cs and add the following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="3ac96-137">Au niveau du code suivant en haut de la méthode **Application_Launching** dans App.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="3ac96-137">Add the following code at the top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="3ac96-138">La valeur **MyPushChannel** est un index utilisé pour rechercher un canal existant dans la collection [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) .</span><span class="sxs-lookup"><span data-stu-id="3ac96-138">The value **MyPushChannel** is an index that is used to lookup an existing channel in the [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="3ac96-139">S’il n’y en a aucun, créez une entrée portant ce nom.</span><span class="sxs-lookup"><span data-stu-id="3ac96-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="3ac96-140">Insérez le nom de votre hub et la chaîne de connexion appelée **DefaultListenSharedAccessSignature** obtenue dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="3ac96-140">Make sure to insert the name of your hub and the connection string called **DefaultListenSharedAccessSignature** that you obtained in the previous section.</span></span>
    <span data-ttu-id="3ac96-141">Ce code récupère l’URI de canal correspondant à l’application dans MPNS, puis inscrit ce dernier avec votre notification Hub.</span><span class="sxs-lookup"><span data-stu-id="3ac96-141">This code retrieves the channel URI for the app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="3ac96-142">Il garantit également l’inscription de l’URI de canal dans votre hub de notification à chaque fois que l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="3ac96-142">It also guarantees that the channel URI is registered in your notification hub each time the application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3ac96-143">Ce didacticiel permet d'envoyer une notification toast à l'appareil.</span><span class="sxs-lookup"><span data-stu-id="3ac96-143">This tutorial sends a toast notification to the device.</span></span> <span data-ttu-id="3ac96-144">Lorsque vous envoyez une notification par vignette, vous devez appeler la méthode **BindToShellTile** sur le canal.</span><span class="sxs-lookup"><span data-stu-id="3ac96-144">When you send a tile notification, you must instead call the **BindToShellTile** method on the channel.</span></span> <span data-ttu-id="3ac96-145">Pour la prise en charge des notifications toast ainsi que des notifications par vignette, appelez **BindToShellTile** et **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="3ac96-145">To support both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="3ac96-146">Dans l’Explorateur de solutions, développez **Propriétés**, ouvrez le fichier `WMAppManifest.xml`, cliquez sur l’onglet **Fonctionnalités** et assurez-vous que la fonctionnalité **ID_CAP_PUSH_NOTIFICATION** soit activée.</span><span class="sxs-lookup"><span data-stu-id="3ac96-146">In Solution Explorer, expand **Properties**, open the `WMAppManifest.xml` file, click the **Capabilities** tab, and make sure that the **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt to send a push notification to the app will fail.
7. <span data-ttu-id="3ac96-147">Appuyez sur la touche `F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="3ac96-147">Press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="3ac96-148">Un message d’inscription s’affiche dans l’application.</span><span class="sxs-lookup"><span data-stu-id="3ac96-148">A registration message is displayed in the app.</span></span>
8. <span data-ttu-id="3ac96-149">Fermez l’application.</span><span class="sxs-lookup"><span data-stu-id="3ac96-149">Close the app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="3ac96-150">Pour recevoir une notification Push toast, l’application ne doit pas s’exécuter au premier plan.</span><span class="sxs-lookup"><span data-stu-id="3ac96-150">To receive a toast push notification, the application must not be running in the foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="3ac96-151">Envoi de notifications Push à partir de votre serveur principal</span><span class="sxs-lookup"><span data-stu-id="3ac96-151">Send push notifications from your backend</span></span>
<span data-ttu-id="3ac96-152">Vous pouvez envoyer des notifications Push en utilisant Notification Hubs à partir d’un serveur principal utilisant l’<a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a> publique.</span><span class="sxs-lookup"><span data-stu-id="3ac96-152">You can send push notifications by using Notification Hubs from any backend via the public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="3ac96-153">Ce didacticiel montre comment envoyer des notifications Push à l’aide d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="3ac96-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="3ac96-154">Pour découvrir un exemple de la procédure d’envoi de notifications Push à partir d’un serveur principal WebAPI ASP.NET intégré à Notification Hubs, consultez l’article [Notification des utilisateurs via Azure Notification Hubs avec service principal .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="3ac96-154">For an example of how to send push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="3ac96-155">Pour voir un exemple d’envoi de notifications Push au moyen des [API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), consultez les articles [Utilisation de Notification Hubs à partir de Java](notification-hubs-java-push-notification-tutorial.md) et [Utilisation de Notification Hubs à partir de PHP](notification-hubs-php-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="3ac96-155">For an example of how to send push notifications by using the [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How to use Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How to use Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="3ac96-156">Cliquez avec le bouton droit sur la solution, sélectionnez **Ajouter** et **Nouveau projet**, puis sous **Visual C#**, cliquez sur **Windows** et **Application Console**. Enfin, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="3ac96-156">Right-click the solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="3ac96-157">Une nouvelle application console Visual C# est ajoutée à la solution.</span><span class="sxs-lookup"><span data-stu-id="3ac96-157">This adds a new Visual C# console application to the solution.</span></span> <span data-ttu-id="3ac96-158">Vous pouvez également réaliser cette opération dans une solution distincte.</span><span class="sxs-lookup"><span data-stu-id="3ac96-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="3ac96-159">Cliquez sur **Outils**, sur **Library Package Manager**, puis sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="3ac96-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="3ac96-160">La Console du Gestionnaire de package apparaît.</span><span class="sxs-lookup"><span data-stu-id="3ac96-160">This displays the Package Manager Console.</span></span>
3. <span data-ttu-id="3ac96-161">Dans la fenêtre **Console du gestionnaire de package**, choisissez **Projet par défaut** comme nouveau projet d’application console, puis exécutez la commande suivante dans la fenêtre de console :</span><span class="sxs-lookup"><span data-stu-id="3ac96-161">In the **Package Manager Console** window, set the **Default project** to your new console application project, and then in the console window, execute the following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="3ac96-162">Cette opération ajoute une référence au Kit de développement logiciel (SDK) Azure Notification Hubs à l’aide du <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet Microsoft.Azure.Notification Hubs</a>.</span><span class="sxs-lookup"><span data-stu-id="3ac96-162">This adds a reference to the Azure Notification Hubs SDK using the <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="3ac96-163">Ouvrez le fichier `Program.cs` et ajoutez l’instruction `using` suivante :</span><span class="sxs-lookup"><span data-stu-id="3ac96-163">Open the `Program.cs` file and add the following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="3ac96-164">Dans la classe `Program`, ajoutez la méthode suivante :</span><span class="sxs-lookup"><span data-stu-id="3ac96-164">In the `Program` class, add the following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="3ac96-165">Remplacez l’espace réservé `<hub name>` par le nom du hub de notification affiché sur le portail.</span><span class="sxs-lookup"><span data-stu-id="3ac96-165">Make sure to replace the `<hub name>` placeholder with the name of the notification hub that appears in the portal.</span></span> <span data-ttu-id="3ac96-166">Remplacez également l’espace réservé de la chaîne de connexion par la chaîne de connexion appelée **DefaultFullSharedAccessSignature** que vous avez obtenue dans la section Configuration de votre hub de notification.</span><span class="sxs-lookup"><span data-stu-id="3ac96-166">Also, replace the connection string placeholder with the connection string called **DefaultFullSharedAccessSignature** that you obtained in the section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3ac96-167">Veillez à utiliser la chaîne de connexion avec un accès **Total**, et non un accès **Écouter**.</span><span class="sxs-lookup"><span data-stu-id="3ac96-167">Make sure that you use the connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="3ac96-168">La chaîne d’accès en écoute seule ne dispose pas des autorisations pour envoyer des notifications Push.</span><span class="sxs-lookup"><span data-stu-id="3ac96-168">The listen-access string does not have permissions to send push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="3ac96-169">Ajoutez la ligne suivante dans votre méthode `Main` :</span><span class="sxs-lookup"><span data-stu-id="3ac96-169">Add the following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="3ac96-170">Votre émulateur Windows Phone étant en cours d’exécution et votre application fermée, configurez le projet d’application console comme projet de démarrage par défaut, puis appuyez sur la touche `F5` pour exécuter l’application.</span><span class="sxs-lookup"><span data-stu-id="3ac96-170">With your Windows Phone emulator running and your app closed, set the console application project as the default startup project, and then press the `F5` key to run the app.</span></span>
   
    <span data-ttu-id="3ac96-171">Vous recevrez une notification Push toast.</span><span class="sxs-lookup"><span data-stu-id="3ac96-171">You will receive a toast push notification.</span></span> <span data-ttu-id="3ac96-172">Une pression sur la bannière du toast pour charger l’application.</span><span class="sxs-lookup"><span data-stu-id="3ac96-172">Tapping the toast banner loads the app.</span></span>

<span data-ttu-id="3ac96-173">Vous trouverez toutes les charges utiles possibles dans le [catalogue toast] et le [catalogue de modèles de vignette] sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="3ac96-173">You can find all the possible payloads in the [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ac96-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3ac96-174">Next steps</span></span>
<span data-ttu-id="3ac96-175">Dans cet exemple simple, vous avez diffusé des notifications Push à tous vos appareils Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="3ac96-175">In this simple example, you broadcasted push notifications to all your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="3ac96-176">Pour cibler certains utilisateurs, reportez-vous au didacticiel [Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs] .</span><span class="sxs-lookup"><span data-stu-id="3ac96-176">In order to target specific users, refer to the [Use Notification Hubs to push notifications to users] tutorial.</span></span> 

<span data-ttu-id="3ac96-177">Pour segmenter vos utilisateurs par groupes d'intérêt, consultez la page [Utilisation des Notification Hubs pour diffuser les dernières nouvelles].</span><span class="sxs-lookup"><span data-stu-id="3ac96-177">If you want to segment your users by interest groups, you can read [Use Notification Hubs to send breaking news].</span></span> 

<span data-ttu-id="3ac96-178">Découvrez plus en détail comment utiliser Notification Hubs dans [Recommandations relatives à Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="3ac96-178">Learn more about how to use Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
<span data-ttu-id="3ac96-179">[Visual Studio 2012 Express pour Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span><span class="sxs-lookup"><span data-stu-id="3ac96-179">[Visual Studio 2012 Express for Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374</span></span>
<span data-ttu-id="3ac96-180">[Recommandations relatives à Notification Hubs]: http://msdn.microsoft.com/library/jj927170.aspx</span><span class="sxs-lookup"><span data-stu-id="3ac96-180">[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx</span></span>
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
<span data-ttu-id="3ac96-181">[Utilisation des Notification Hubs pour envoyer des notifications Push aux utilisateurs]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span><span class="sxs-lookup"><span data-stu-id="3ac96-181">[Use Notification Hubs to push notifications to users]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md</span></span>
<span data-ttu-id="3ac96-182">[Utilisation des Notification Hubs pour diffuser les dernières nouvelles]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span><span class="sxs-lookup"><span data-stu-id="3ac96-182">[Use Notification Hubs to send breaking news]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md</span></span>
<span data-ttu-id="3ac96-183">[catalogue toast]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="3ac96-183">[toast catalog]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx</span></span>
<span data-ttu-id="3ac96-184">[catalogue de modèles de vignette]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="3ac96-184">[tile catalog]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx</span></span>
<span data-ttu-id="3ac96-185">[didacticiel Notification Hubs - Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span><span class="sxs-lookup"><span data-stu-id="3ac96-185">[Notification Hubs - Windows Phone Silverlight tutorial]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp</span></span>

