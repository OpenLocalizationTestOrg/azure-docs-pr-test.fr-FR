---
title: aaaSending des notifications de push avec Azure Notification Hubs sur Windows Phone | Documents Microsoft
description: Dans ce didacticiel, vous apprendrez comment des notifications de toouse Azure Notification Hubs toopush tooa Windows Phone 8 ou Windows Phone 8.1 Silverlight application.
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
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="c9c3e-104">Envoi de notifications Push avec Azure Notification Hubs sur Windows Phone</span><span class="sxs-lookup"><span data-stu-id="c9c3e-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c9c3e-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="c9c3e-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="c9c3e-106">toocomplete ce didacticiel, vous devez disposer d’un compte Azure actif.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="c9c3e-107">Si vous ne possédez pas de compte, vous pouvez créer un compte d'évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="c9c3e-108">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="c9c3e-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="c9c3e-109">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 ou Windows Phone 8.1 Silverlight une application.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="c9c3e-110">Si vous ciblez Windows Phone 8.1 (non Silverlight), puis consultez toohello [Windows universel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="c9c3e-111">Dans ce didacticiel, vous créez une application Windows Phone 8 vide qui reçoit des notifications push à l’aide de hello services de notifications Push Microsoft (MPNS).</span><span class="sxs-lookup"><span data-stu-id="c9c3e-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="c9c3e-112">Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c3e-113">Hello Notification Hubs Windows Phone SDK ne prend pas en charge à l’aide de hello services de notifications Push Windows (WNS) avec les applications Windows Phone 8.1 Silverlight.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="c9c3e-114">toouse WNS (au lieu de MPNS) avec les applications Windows Phone 8.1 Silverlight, suivez hello [Notification Hubs - didacticiel de Windows Phone Silverlight], qui utilise l’API REST.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="c9c3e-115">didacticiel de Hello montre le scénario de diffusion simple hello dans à l’aide de concentrateurs de Notification.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9c3e-116">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c9c3e-116">Prerequisites</span></span>
<span data-ttu-id="c9c3e-117">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="c9c3e-118">[Visual Studio 2012 Express pour Windows Phone]ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="c9c3e-119">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels concernant les Notification Hubs pour les applications Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="c9c3e-120">Création de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="c9c3e-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="c9c3e-121">Cliquez sur hello <b>Notification Services</b> section (dans <i>paramètres</i>), cliquez sur <b>Windows Phone (MPNS)</b> puis cliquez sur hello <b>activer push non authentifiées </b> case à cocher.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Portail Azure - Activez les notifications Push non authentifiées](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="c9c3e-123">Votre concentrateur est maintenant créé et configuré toosend non authentifié de notification pour Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c3e-124">Ce didacticiel utilise MPNS en mode non authentifié.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="c9c3e-125">Le mode MPNS non authentifié est fourni avec des restrictions sur les notifications que vous pouvez envoyer tooeach canal.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="c9c3e-126">Prend en charge les concentrateurs de notification [MPNS authentifié mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) en vous tooupload votre certificat.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="c9c3e-127">Connectez votre concentrateur de notification d’application toohello</span><span class="sxs-lookup"><span data-stu-id="c9c3e-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="c9c3e-128">Dans Visual Studio, créez une application Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="c9c3e-129">Dans Visual Studio 2013 Update 2 ou version ultérieure, vous créez plutôt une application Silverlight Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - Nouveau projet - Application vide - Windows Phone Silverlight][11]
2. <span data-ttu-id="c9c3e-131">Dans Visual Studio, cliquez sur la solution de hello, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="c9c3e-132">Cela affiche hello **gérer les Packages NuGet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="c9c3e-133">Recherchez `WindowsAzure.Messaging.Managed` et cliquez sur **installer**, puis acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio - Gestionnaire de packages NuGet][20]
   
    <span data-ttu-id="c9c3e-135">Il télécharge, installe et ajoute une bibliothèque de messagerie Azure référence toohello pour Windows à l’aide de hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">package NuGet de WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="c9c3e-136">Ouvrez le fichier de hello App.xaml.cs et ajoutez les éléments suivants de hello `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="c9c3e-137">Ajouter hello suivant code haut hello **Application_Launching** méthode dans App.xaml.cs :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
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
   > <span data-ttu-id="c9c3e-138">valeur de Hello **MyPushChannel** est un index qui est utilisé toolookup un canal existant Bonjour [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="c9c3e-139">S’il n’y en a aucun, créez une entrée portant ce nom.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="c9c3e-140">Assurez-vous que le nom de hello tooinsert de votre chaîne de connexion de concentrateur et hello appelé **DefaultListenSharedAccessSignature** que vous avez obtenu dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="c9c3e-141">Ce code récupère l’URI de canal hello pour une application hello de MPNS et inscrit ce canal URI avec votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="c9c3e-142">Elle garantit également que ce canal hello QU'URI est enregistré dans votre concentrateur de notification que chaque application hello de temps est lancée.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c9c3e-143">Ce didacticiel envoie un périphérique toohello de notification toast.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="c9c3e-144">Lorsque vous envoyez une notification de vignette, vous devez appeler hello **BindToShellTile** méthode sur le canal de hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="c9c3e-145">toosupport des notifications toast et vignette, appeler à la fois **BindToShellTile** et **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="c9c3e-146">Dans l’Explorateur de solutions, développez **propriétés**, ouvrez hello `WMAppManifest.xml` de fichiers, cliquez sur hello **fonctionnalités** onglet et vérifiez que ce hello **ID_CAP_PUSH_NOTIFICATION** fonctionnalité est activée.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="c9c3e-147">Hello de presse `F5` toorun clé hello application.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="c9c3e-148">Un message d’inscription s’affiche dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="c9c3e-149">Hello fermer l’application.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="c9c3e-150">tooreceive une notification toast, application hello ne doit pas exécuter de premier plan de hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="c9c3e-151">Envoi de notifications Push à partir de votre serveur principal</span><span class="sxs-lookup"><span data-stu-id="c9c3e-151">Send push notifications from your backend</span></span>
<span data-ttu-id="c9c3e-152">Vous pouvez envoyer des notifications push à l’aide de concentrateurs de Notification à partir de n’importe quel serveur principal via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">interface REST</a>.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="c9c3e-153">Ce didacticiel montre comment envoyer des notifications Push à l’aide d’une application de console .NET.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="c9c3e-154">Pour obtenir un exemple de comment toosend des notifications push à partir d’un serveur principal ASP.NET WebAPI intégré avec Notification Hubs, consultez [Azure Notification Hubs d’avertir les utilisateurs avec le serveur principal .NET](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="c9c3e-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="c9c3e-155">Pour obtenir un exemple de comment toosend les notifications push à l’aide de hello [API REST](https://msdn.microsoft.com/library/azure/dn223264.aspx), extraire [comment toouse concentrateurs de Notification à partir de Java](notification-hubs-java-push-notification-tutorial.md) et [comment toouse concentrateurs de Notification à partir de PHP](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="c9c3e-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="c9c3e-156">Solution de hello avec le bouton droit, sélectionnez **ajouter** et **nouveau projet...** , puis sous **Visual C#**, cliquez sur **Windows** et **Application Console**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="c9c3e-157">Cette opération ajoute une nouvelle Visual C# toohello solution d’application console.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="c9c3e-158">Vous pouvez également réaliser cette opération dans une solution distincte.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="c9c3e-159">Cliquez sur **Outils**, sur **Library Package Manager**, puis sur **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="c9c3e-160">Cette opération affiche hello Console du Gestionnaire de Package.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="c9c3e-161">Bonjour **Package Manager Console** fenêtre, jeu hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="c9c3e-162">Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="c9c3e-163">Ouvrez hello `Program.cs` et ajoutez les suivant hello `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="c9c3e-164">Bonjour `Program` de classe, ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-164">In hello `Program` class, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="c9c3e-165">Assurez-vous que tooreplace hello `<hub name>` espace réservé par nom de hello du hub de notification hello qui apparaît dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="c9c3e-166">En outre, remplacez espace réservé de chaîne hello connexion avec la chaîne de connexion hello appelé **DefaultFullSharedAccessSignature** que vous avez obtenu dans la section de hello « Configurer votre concentrateur de notification ».</span><span class="sxs-lookup"><span data-stu-id="c9c3e-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c9c3e-167">Assurez-vous que vous utilisez avec la chaîne de connexion de hello **complète** accéder, pas **écouter** accès.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="c9c3e-168">chaîne d’accès à l’écoute de Hello n’a pas de notifications push de toosend autorisations.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="c9c3e-169">Ajouter hello ligne dans votre `Main` méthode :</span><span class="sxs-lookup"><span data-stu-id="c9c3e-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="c9c3e-170">Avec votre Windows Phone émulateur en cours d’exécution et votre projet d’application de console application hello fermé, définissez comme hello par défaut du projet de démarrage, puis appuyez sur hello `F5` toorun clé hello application.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="c9c3e-171">Vous recevrez une notification Push toast.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-171">You will receive a toast push notification.</span></span> <span data-ttu-id="c9c3e-172">En appuyant sur la bannière de toast hello charge application hello.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="c9c3e-173">Vous pouvez trouver toutes les charges utiles de possibles hello Bonjour [catalogue de toast] et [vignette catalogue] rubriques sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c3e-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c9c3e-174">Next steps</span></span>
<span data-ttu-id="c9c3e-175">Dans cet exemple simple, vous diffusées tooall de notifications push à vos appareils Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="c9c3e-176">Dans l’ordre tootarget des utilisateurs spécifiques, consultez toohello [utiliser Notification Hubs toopush notifications toousers] didacticiel.</span><span class="sxs-lookup"><span data-stu-id="c9c3e-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="c9c3e-177">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, vous pouvez lire [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="c9c3e-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="c9c3e-178">En savoir plus sur la façon toouse Notification Hubs dans [des conseils de concentrateurs de Notification].</span><span class="sxs-lookup"><span data-stu-id="c9c3e-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

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
[Visual Studio 2012 Express pour Windows Phone]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[des conseils de concentrateurs de Notification]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[utiliser Notification Hubs toopush notifications toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[catalogue de toast]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[vignette catalogue]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - didacticiel de Windows Phone Silverlight]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

