---
title: application de plateforme Windows universelle (UWP) aaaAdd push notifications tooyour | Documents Microsoft
description: "Découvrez comment toouse Azure App Service Mobile Apps et Azure Notification Hubs toosend push application de plateforme Windows universelle (UWP) tooyour des notifications."
services: app-service\mobile,notification-hubs
documentationcenter: windows
author: ysxu
manager: syntaxc4
editor: 
ms.assetid: 6de1b9d4-bd28-43e4-8db4-94cd3b187aa3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/12/2016
ms.author: yuaxu
ms.openlocfilehash: 378ce59cab974830c0a3801108b24b30a21ae5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-windows-app"></a><span data-ttu-id="3f398-103">Ajouter une application Windows de push notifications tooyour</span><span class="sxs-lookup"><span data-stu-id="3f398-103">Add push notifications tooyour Windows app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a><span data-ttu-id="3f398-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="3f398-104">Overview</span></span>
<span data-ttu-id="3f398-105">Dans ce didacticiel, vous allez ajouter toohello de notifications push [démarrage rapide Windows](app-service-mobile-windows-store-dotnet-get-started.md) projet afin qu’une notification push est envoyée toohello périphérique chaque fois qu’un enregistrement est inséré.</span><span class="sxs-lookup"><span data-stu-id="3f398-105">In this tutorial, you add push notifications toohello [Windows quick start](app-service-mobile-windows-store-dotnet-get-started.md) project so that a push notification is sent toohello device every time a record is inserted.</span></span>

<span data-ttu-id="3f398-106">Si vous n’utilisez pas hello téléchargé le projet de démarrage rapide de serveur, vous devez serez hello package d’extension de notification push.</span><span class="sxs-lookup"><span data-stu-id="3f398-106">If you do not use hello downloaded quick start server project, you will need hello push notification extension package.</span></span> <span data-ttu-id="3f398-107">Consultez [fonctionne avec serveur principal de .NET hello SDK pour les applications mobiles Azure](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="3f398-107">See [Work with hello .NET backend server SDK for Azure Mobile Apps](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md) for more information.</span></span>

## <span data-ttu-id="3f398-108"><a name="configure-hub"></a>Configurer un nouveau hub de notification</span><span class="sxs-lookup"><span data-stu-id="3f398-108"><a name="configure-hub"></a>Configure a Notification Hub</span></span>
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="3f398-109">Inscription de votre application pour les notifications Push</span><span class="sxs-lookup"><span data-stu-id="3f398-109">Register your app for push notifications</span></span>
<span data-ttu-id="3f398-110">Vous devez toosubmit votre toohello d’application du Windows Store, puis configurez votre toointegrate de project server avec les Services de Notification de Windows (WNS) toosend push.</span><span class="sxs-lookup"><span data-stu-id="3f398-110">You need toosubmit your app toohello Windows Store, then configure your server project toointegrate with Windows Notification Services (WNS) toosend push.</span></span>

1. <span data-ttu-id="3f398-111">Dans l’Explorateur de solutions Visual Studio, projet d’application hello UWP avec le bouton droit, cliquez sur **magasin** > **associer application hello Store...** .</span><span class="sxs-lookup"><span data-stu-id="3f398-111">In Visual Studio Solution Explorer, right-click hello UWP app project, click **Store** > **Associate App with hello Store...**.</span></span>

    ![Associer une application au Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/notification-hub-associate-uwp-app.png)
2. <span data-ttu-id="3f398-113">Dans l’Assistant de hello, cliquez sur **suivant**, connectez-vous avec votre compte Microsoft, tapez un nom pour votre application dans **réserver un nouveau nom de l’application**, puis cliquez sur **réserve**.</span><span class="sxs-lookup"><span data-stu-id="3f398-113">In hello wizard, click **Next**, sign in with your Microsoft account, type a name for your app in **Reserve a new app name**, then click **Reserve**.</span></span>
3. <span data-ttu-id="3f398-114">Une fois l’inscription d’une application hello nouveau nom d’application a été créé correctement, sélectionnez hello, cliquez sur **suivant**, puis cliquez sur **associer**.</span><span class="sxs-lookup"><span data-stu-id="3f398-114">After hello app registration is successfully created, select hello new app name, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="3f398-115">Cela ajoute le manifeste d’application d’enregistrement d’informations toohello hello requis du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="3f398-115">This adds hello required Windows Store registration information toohello application manifest.</span></span>  
4. <span data-ttu-id="3f398-116">Accédez toohello [centre de développement Windows](https://dev.windows.com/en-us/overview), connectez-vous avec votre compte Microsoft, cliquez sur nouvelle inscription d’application hello dans **mes applications**, puis développez **Services**  >  **Des notifications push**.</span><span class="sxs-lookup"><span data-stu-id="3f398-116">Navigate toohello [Windows Dev Center](https://dev.windows.com/en-us/overview), sign-in with your Microsoft account, click hello new app registration in **My apps**, then expand **Services** > **Push notifications**.</span></span>
5. <span data-ttu-id="3f398-117">Bonjour **des notifications Push** , cliquez sur **site des Services Live** sous **Microsoft Azure Mobile Services**.</span><span class="sxs-lookup"><span data-stu-id="3f398-117">In hello **Push notifications** page, click **Live Services site** under **Microsoft Azure Mobile Services**.</span></span>
6. <span data-ttu-id="3f398-118">Dans la page d’inscription de hello, prenez note de la valeur hello sous **secrets d’Application** et hello **SID du Package**, qui vous allez ensuite utiliser tooconfigure service principal de votre application mobile.</span><span class="sxs-lookup"><span data-stu-id="3f398-118">In hello registration page, make a note of hello value under **Application secrets** and hello **Package SID**, which you will next use tooconfigure your mobile app backend.</span></span>

    ![Associer une application au Windows Store](./media/app-service-mobile-windows-store-dotnet-get-started-push/app-service-mobile-uwp-app-push-auth.png)

   > [!IMPORTANT]
   > <span data-ttu-id="3f398-120">question secrète du client Hello et le SID du package sont des informations d’identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="3f398-120">hello client secret and package SID are important security credentials.</span></span> <span data-ttu-id="3f398-121">Ne partagez pas ces valeurs avec quiconque et ne les distribuez pas avec votre application.</span><span class="sxs-lookup"><span data-stu-id="3f398-121">Do not share these values with anyone or distribute them with your app.</span></span> <span data-ttu-id="3f398-122">Hello **Id d’Application** est utilisé avec l’authentification de Microsoft Account hello tooconfigure secret principal.</span><span class="sxs-lookup"><span data-stu-id="3f398-122">hello **Application Id** is used with hello secret tooconfigure Microsoft Account authentication.</span></span>
   >
   >

## <a name="configure-hello-backend-toosend-push-notifications"></a><span data-ttu-id="3f398-123">Configurer les notifications de push toosend hello principal</span><span class="sxs-lookup"><span data-stu-id="3f398-123">Configure hello backend toosend push notifications</span></span>
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

## <span data-ttu-id="3f398-124"><a id="update-service"></a>Mettre à jour des notifications push de hello server toosend</span><span class="sxs-lookup"><span data-stu-id="3f398-124"><a id="update-service"></a>Update hello server toosend push notifications</span></span>
<span data-ttu-id="3f398-125">Utilisez hello procédure ci-dessous qui correspond à votre type de projet principal&mdash;soit [service principal .NET](#dotnet) ou [Node.js principal](#nodejs).</span><span class="sxs-lookup"><span data-stu-id="3f398-125">Use hello procedure below that matches your backend project type&mdash;either [.NET backend](#dotnet) or [Node.js backend](#nodejs).</span></span>

### <span data-ttu-id="3f398-126"><a name="dotnet"></a>Projet de serveur principal .NET</span><span class="sxs-lookup"><span data-stu-id="3f398-126"><a name="dotnet"></a>.NET backend project</span></span>
1. <span data-ttu-id="3f398-127">Dans Visual Studio, cliquez sur le projet de serveur hello et cliquez sur **gérer les Packages NuGet**, recherchez Microsoft.Azure.NotificationHubs, puis cliquez sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="3f398-127">In Visual Studio, right-click hello server project and click **Manage NuGet Packages**, search for Microsoft.Azure.NotificationHubs, then click **Install**.</span></span> <span data-ttu-id="3f398-128">Bibliothèque cliente de concentrateurs de Notification hello sont ainsi installés.</span><span class="sxs-lookup"><span data-stu-id="3f398-128">This installs hello Notification Hubs client library.</span></span>
2. <span data-ttu-id="3f398-129">Développez **contrôleurs**, ouvrez TodoItemController.cs et ajoutez hello qui suit à l’aide des instructions :</span><span class="sxs-lookup"><span data-stu-id="3f398-129">Expand **Controllers**, open TodoItemController.cs, and add hello following using statements:</span></span>

        using System.Collections.Generic;
        using Microsoft.Azure.NotificationHubs;
        using Microsoft.Azure.Mobile.Server.Config;
3. <span data-ttu-id="3f398-130">Bonjour **PostTodoItem** (méthode), ajouter hello suivant code après appel de hello trop**InsertAsync**:</span><span class="sxs-lookup"><span data-stu-id="3f398-130">In hello **PostTodoItem** method, add hello following code after hello call too**InsertAsync**:</span></span>

        // Get hello settings for hello server project.
        HttpConfiguration config = this.Configuration;
        MobileAppSettingsDictionary settings =
            this.Configuration.GetMobileAppSettingsProvider().GetMobileAppSettings();

        // Get hello Notification Hubs credentials for hello Mobile App.
        string notificationHubName = settings.NotificationHubName;
        string notificationHubConnection = settings
            .Connections[MobileAppSettingsKeys.NotificationHubConnectionString].ConnectionString;

        // Create hello notification hub client.
        NotificationHubClient hub = NotificationHubClient
            .CreateClientFromConnectionString(notificationHubConnection, notificationHubName);

        // Define a WNS payload
        var windowsToastPayload = @"<toast><visual><binding template=""ToastText01""><text id=""1"">"
                                + item.Text + @"</text></binding></visual></toast>";
        try
        {
            // Send hello push notification.
            var result = await hub.SendWindowsNativeNotificationAsync(windowsToastPayload);

            // Write hello success result toohello logs.
            config.Services.GetTraceWriter().Info(result.State.ToString());
        }
        catch (System.Exception ex)
        {
            // Write hello failure result toohello logs.
            config.Services.GetTraceWriter()
                .Error(ex.Message, null, "Push.SendAsync Error");
        }

    <span data-ttu-id="3f398-131">Ce code indique à hello notification hub toosend une notification une fois un nouvel élément de l’insertion.</span><span class="sxs-lookup"><span data-stu-id="3f398-131">This code tells hello notification hub toosend a push notification after a new item is insertion.</span></span>
4. <span data-ttu-id="3f398-132">Publiez de nouveau projet de serveur hello.</span><span class="sxs-lookup"><span data-stu-id="3f398-132">Republish hello server project.</span></span>

### <span data-ttu-id="3f398-133"><a name="nodejs"></a>Projet de back-end Node.js</span><span class="sxs-lookup"><span data-stu-id="3f398-133"><a name="nodejs"></a>Node.js backend project</span></span>
1. <span data-ttu-id="3f398-134">Si vous n’avez pas déjà fait, [télécharger le projet de démarrage rapide de hello](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) ou sinon utilisez hello [éditeur en ligne Bonjour Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span><span class="sxs-lookup"><span data-stu-id="3f398-134">If you haven't already done so, [download hello quickstart project](app-service-mobile-node-backend-how-to-use-server-sdk.md#download-quickstart) or else use hello [online editor in hello Azure portal](app-service-mobile-node-backend-how-to-use-server-sdk.md#online-editor).</span></span>
2. <span data-ttu-id="3f398-135">Remplacez le code existant dans le fichier de todoitem.js hello hello suivant de hello :</span><span class="sxs-lookup"><span data-stu-id="3f398-135">Replace hello existing code in hello todoitem.js file with hello following:</span></span>

        var azureMobileApps = require('azure-mobile-apps'),
        promises = require('azure-mobile-apps/src/utilities/promises'),
        logger = require('azure-mobile-apps/src/logger');

        var table = azureMobileApps.table();

        table.insert(function (context) {
        // For more information about hello Notification Hubs JavaScript SDK,
        // see http://aka.ms/nodejshubs
        logger.info('Running TodoItem.insert');

        // Define hello WNS payload that contains hello new item Text.
        var payload = "<toast><visual><binding template=\ToastText01\><text id=\"1\">"
                                    + context.item.text + "</text></binding></visual></toast>";

        // Execute hello insert.  hello insert returns hello results as a Promise,
        // Do hello push as a post-execute action within hello promise flow.
        return context.execute()
            .then(function (results) {
                // Only do hello push if configured
                if (context.push) {
                    // Send a WNS native toast notification.
                    context.push.wns.sendToast(null, payload, function (error) {
                        if (error) {
                            logger.error('Error while sending push notification: ', error);
                        } else {
                            logger.info('Push notification sent successfully!');
                        }
                    });
                }
                // Don't forget tooreturn hello results from hello context.execute()
                return results;
            })
            .catch(function (error) {
                logger.error('Error while running context.execute: ', error);
            });
        });

        module.exports = table;

    <span data-ttu-id="3f398-136">Envoie une notification toast WNS contenant hello item.text lors de l’insertion d’un nouvel élément de tâche.</span><span class="sxs-lookup"><span data-stu-id="3f398-136">This sends a WNS toast notification that contains hello item.text when a new todo item is inserted.</span></span>
3. <span data-ttu-id="3f398-137">Lorsque vous modifiez le fichier hello sur votre ordinateur local, le projet de serveur hello republier.</span><span class="sxs-lookup"><span data-stu-id="3f398-137">When editing hello file on your local computer, republish hello server project.</span></span>

## <span data-ttu-id="3f398-138"><a id="update-app"></a>Ajouter une application de tooyour de notifications push</span><span class="sxs-lookup"><span data-stu-id="3f398-138"><a id="update-app"></a>Add push notifications tooyour app</span></span>
<span data-ttu-id="3f398-139">Ensuite, votre application doit s’inscrire pour les notifications Push au démarrage.</span><span class="sxs-lookup"><span data-stu-id="3f398-139">Next, your app must register for push notifications on start-up.</span></span> <span data-ttu-id="3f398-140">Lorsque vous avez déjà activé l’authentification, assurez-vous que l’utilisateur hello se connecte en avant d’essayer de tooregister pour les notifications push.</span><span class="sxs-lookup"><span data-stu-id="3f398-140">When you have already enabled authentication, make sure that hello user signs-in before trying tooregister for push notifications.</span></span>

1. <span data-ttu-id="3f398-141">Ouvrez hello **App.xaml.cs** fichier projet et ajoutez hello suit `using` instructions :</span><span class="sxs-lookup"><span data-stu-id="3f398-141">Open hello **App.xaml.cs** project file and add hello following `using` statements:</span></span>

        using System.Threading.Tasks;
        using Windows.Networking.PushNotifications;
2. <span data-ttu-id="3f398-142">Dans hello du même fichier, ajoutez hello **InitNotificationsAsync** toohello de définition de méthode **application** classe :</span><span class="sxs-lookup"><span data-stu-id="3f398-142">In hello same file, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>

        private async Task InitNotificationsAsync()
        {
            // Get a channel URI from WNS.
            var channel = await PushNotificationChannelManager
                .CreatePushNotificationChannelForApplicationAsync();

            // Register hello channel URI with Notification Hubs.
            await App.MobileService.GetPush().RegisterAsync(channel.Uri);
        }

    <span data-ttu-id="3f398-143">Ce code récupère hello ChannelURI pour l’application hello WNS et inscrit ce ChannelURI avec votre application de Service d’applications mobiles.</span><span class="sxs-lookup"><span data-stu-id="3f398-143">This code retrieves hello ChannelURI for hello app from WNS, and then registers that ChannelURI with your App Service Mobile App.</span></span>
3. <span data-ttu-id="3f398-144">En haut de hello Hello **OnLaunched** Gestionnaire d’événements dans **App.xaml.cs**, ajouter hello **async** définition de méthode modificateur toohello et ajoutez suivant de hello appeler denouveautoohello **InitNotificationsAsync** méthode, comme dans hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="3f398-144">At hello top of hello **OnLaunched** event handler in **App.xaml.cs**, add hello **async** modifier toohello method definition and add hello following call toohello new **InitNotificationsAsync** method, as in hello following example:</span></span>

        protected async override void OnLaunched(LaunchActivatedEventArgs e)
        {
            await InitNotificationsAsync();

            // ...
        }

    <span data-ttu-id="3f398-145">Cela garantit que hello que channeluri de courte durée de vie est enregistré à chaque lancement de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="3f398-145">This guarantees that hello short-lived ChannelURI is registered each time hello application is launched.</span></span>
4. <span data-ttu-id="3f398-146">Recréez votre projet d’application UWP.</span><span class="sxs-lookup"><span data-stu-id="3f398-146">Rebuild your UWP app project.</span></span> <span data-ttu-id="3f398-147">Votre application est maintenant prêt tooreceive des notifications de toast.</span><span class="sxs-lookup"><span data-stu-id="3f398-147">Your app is now ready tooreceive toast notifications.</span></span>

## <span data-ttu-id="3f398-148"><a id="test"></a>Tester les notifications push dans votre application</span><span class="sxs-lookup"><span data-stu-id="3f398-148"><a id="test"></a>Test push notifications in your app</span></span>
[!INCLUDE [app-service-mobile-windows-universal-test-push](../../includes/app-service-mobile-windows-universal-test-push.md)]

## <span data-ttu-id="3f398-149"><a id="more"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3f398-149"><a id="more"></a>Next steps</span></span>
<span data-ttu-id="3f398-150">Apprenez-en plus sur les notifications Push :</span><span class="sxs-lookup"><span data-stu-id="3f398-150">Learn more about push notifications:</span></span>

* [<span data-ttu-id="3f398-151">Comment toouse hello gérées client pour les applications mobiles Azure</span><span class="sxs-lookup"><span data-stu-id="3f398-151">How toouse hello managed client for Azure Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md#pushnotifications)  
  <span data-ttu-id="3f398-152">Les modèles vous permettent de push de flexibilité toosend inter-plateformes et push localisée.</span><span class="sxs-lookup"><span data-stu-id="3f398-152">Templates give you flexibility toosend cross-platform pushes and localized pushes.</span></span> <span data-ttu-id="3f398-153">Découvrez comment tooregister modèles.</span><span class="sxs-lookup"><span data-stu-id="3f398-153">Learn how tooregister templates.</span></span>
* [<span data-ttu-id="3f398-154">Diagnostiquer les problèmes de notification Push</span><span class="sxs-lookup"><span data-stu-id="3f398-154">Diagnose push notification issues</span></span>](../notification-hubs/notification-hubs-push-notification-fixer.md)  
  <span data-ttu-id="3f398-155">Il existe différentes raisons pour lesquelles les notifications peuvent être perdues ou n’arrivent pas sur les appareils.</span><span class="sxs-lookup"><span data-stu-id="3f398-155">There are various reasons why notifications may get dropped or do not end up on devices.</span></span> <span data-ttu-id="3f398-156">Cette rubrique vous montre comment tooanalyze et déterminer la racine de hello provoquent des erreurs de notification push.</span><span class="sxs-lookup"><span data-stu-id="3f398-156">This topic shows you how tooanalyze and figure out hello root cause of push notification failures.</span></span>

<span data-ttu-id="3f398-157">Envisagez de continuer sur tooone Hello suivant didacticiels :</span><span class="sxs-lookup"><span data-stu-id="3f398-157">Consider continuing on tooone of hello following tutorials:</span></span>

* [<span data-ttu-id="3f398-158">Ajouter une application de tooyour d’authentification</span><span class="sxs-lookup"><span data-stu-id="3f398-158">Add authentication tooyour app</span></span>](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  <span data-ttu-id="3f398-159">Découvrez comment tooauthenticate les utilisateurs de votre application avec un fournisseur d’identité.</span><span class="sxs-lookup"><span data-stu-id="3f398-159">Learn how tooauthenticate users of your app with an identity provider.</span></span>
* [<span data-ttu-id="3f398-160">Activer la synchronisation hors connexion pour votre application</span><span class="sxs-lookup"><span data-stu-id="3f398-160">Enable offline sync for your app</span></span>](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  <span data-ttu-id="3f398-161">Découvrez comment tooadd hors connexion prennent en charge votre application à l’aide d’un serveur principal de l’application Mobile.</span><span class="sxs-lookup"><span data-stu-id="3f398-161">Learn how tooadd offline support your app using an Mobile App backend.</span></span> <span data-ttu-id="3f398-162">Synchronisation hors connexion permet de toointeract les utilisateurs finaux avec une application mobile&mdash;affichage, l’ajout ou la modification des données&mdash;même quand il n’existe aucune connexion réseau.</span><span class="sxs-lookup"><span data-stu-id="3f398-162">Offline sync allows end-users toointeract with a mobile app&mdash;viewing, adding, or modifying data&mdash;even when there is no network connection.</span></span>

<!-- Anchors. -->

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

<!-- Images. -->
