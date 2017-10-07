---
title: "aaaGet main d’Azure Notification Hubs pour les applications Windows universelles plateforme | Documents Microsoft"
description: Dans ce didacticiel, vous apprendrez comment toouse Azure Notification Hubs toopush notifications tooa application de plateforme universelle Windows.
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="ee721-103">Prise en main de Notification Hubs pour les applications de plateforme Windows universelle</span><span class="sxs-lookup"><span data-stu-id="ee721-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="ee721-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ee721-104">Overview</span></span>
<span data-ttu-id="ee721-105">Ce didacticiel vous montre comment toouse Azure Notification Hubs toosend push application de plateforme Windows universelle (UWP) tooa des notifications.</span><span class="sxs-lookup"><span data-stu-id="ee721-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="ee721-106">Dans ce didacticiel, vous créez une application du Windows Store vide qui reçoit des notifications push à l’aide de hello services de notifications Push Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="ee721-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="ee721-107">Lorsque vous avez terminé, vous serez en mesure de toouse votre toobroadcast de concentrateur de notification push des appareils de hello notifications tooall votre application en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="ee721-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ee721-108">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="ee721-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="ee721-109">code Hello terminée pour ce didacticiel se trouve sur GitHub [ici](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="ee721-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee721-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ee721-110">Prerequisites</span></span>
<span data-ttu-id="ee721-111">Ce didacticiel requiert hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="ee721-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="ee721-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) ou version ultérieure</span><span class="sxs-lookup"><span data-stu-id="ee721-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="ee721-113">Outils de développement d’applications Windows universelles installés</span><span class="sxs-lookup"><span data-stu-id="ee721-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="ee721-114">Un compte Azure actif </span><span class="sxs-lookup"><span data-stu-id="ee721-114">An active Azure account</span></span> <br/><span data-ttu-id="ee721-115">Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ee721-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ee721-116">Pour plus d'informations, consultez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="ee721-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="ee721-117">Un compte Windows Store actif</span><span class="sxs-lookup"><span data-stu-id="ee721-117">An active Windows Store account</span></span>

<span data-ttu-id="ee721-118">Vous devez suivre ce didacticiel avant de pouvoir suivre tous les autres didacticiels Notification Hubs pour les applications de plateforme Windows universelle.</span><span class="sxs-lookup"><span data-stu-id="ee721-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="ee721-119">Inscrire votre application pour hello du Windows Store</span><span class="sxs-lookup"><span data-stu-id="ee721-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="ee721-120">applications de tooUWP toosend push notifications, vous devez associer votre toohello d’application du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="ee721-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="ee721-121">Vous devez ensuite configurer votre toointegrate de concentrateur de notification avec WNS.</span><span class="sxs-lookup"><span data-stu-id="ee721-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="ee721-122">Si vous n’avez pas encore inscrit votre application, accédez à toohello [centre de développement Windows](https://dev.windows.com/overview), connectez-vous avec votre compte Microsoft, puis cliquez sur **créer une application**.</span><span class="sxs-lookup"><span data-stu-id="ee721-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="ee721-123">Saisissez un nom pour votre application et cliquez sur **Réserver le nom d’application**.</span><span class="sxs-lookup"><span data-stu-id="ee721-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="ee721-124">La nouvelle inscription au Windows Store pour votre application est créée.</span><span class="sxs-lookup"><span data-stu-id="ee721-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="ee721-125">Dans Visual Studio, créez un projet de Visual C# applications du Windows Store à l’aide de hello Windows universel **application vide** modèle et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee721-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="ee721-126">Acceptez les valeurs par défaut de hello pour cible de hello et les versions de plateforme minimales.</span><span class="sxs-lookup"><span data-stu-id="ee721-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="ee721-127">Dans l’Explorateur de solutions, projet d’application hello du Windows Store avec le bouton droit, cliquez sur **magasin**, puis cliquez sur **associer application hello Store...** . hello **associer votre application du Windows Store de hello** Assistant s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ee721-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="ee721-128">Dans l’Assistant de hello, connectez-vous avec votre compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ee721-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="ee721-129">Cliquez sur l’application hello que vous avez enregistré à l’étape 2, cliquez sur **suivant**, puis cliquez sur **associer**.</span><span class="sxs-lookup"><span data-stu-id="ee721-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="ee721-130">Cela ajoute le manifeste d’application d’enregistrement d’informations toohello hello requis du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="ee721-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="ee721-131">Retour sur hello [centre de développement Windows](http://dev.windows.com/overview) pour votre nouvelle application, cliquez sur **Services**, cliquez sur **des notifications Push**, puis cliquez sur **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="ee721-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="ee721-132">Cliquez sur **Nouvelle notification**.</span><span class="sxs-lookup"><span data-stu-id="ee721-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="ee721-133">Cliquez sur le modèle **Blank (Toast)** (Vide (Toast), puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee721-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="ee721-134">Saisissez un **nom** et un message de **contexte** Visual pour la notification.</span><span class="sxs-lookup"><span data-stu-id="ee721-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="ee721-135">Cliquez ensuite sur **Enregistrer en tant que brouillon**.</span><span class="sxs-lookup"><span data-stu-id="ee721-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="ee721-136">Accédez toohello [portail de l’enregistrement d’Application](http://apps.dev.microsoft.com) et connectez-vous.</span><span class="sxs-lookup"><span data-stu-id="ee721-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="ee721-137">Cliquez sur le nom de votre application.</span><span class="sxs-lookup"><span data-stu-id="ee721-137">Click on your application name.</span></span> <span data-ttu-id="ee721-138">Prenez note de hello **Secret d’Application** hello et le mot de passe **Package SID (security identifier)** situé dans hello **du Windows Store** paramètres de plateforme.</span><span class="sxs-lookup"><span data-stu-id="ee721-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="ee721-139">secret d’application Hello et le SID du package sont des informations d’identification de sécurité importantes.</span><span class="sxs-lookup"><span data-stu-id="ee721-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="ee721-140">Ne partagez pas ces valeurs avec quiconque et ne les distribuez pas avec votre application.</span><span class="sxs-lookup"><span data-stu-id="ee721-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="ee721-141">Configuration de votre hub de notification</span><span class="sxs-lookup"><span data-stu-id="ee721-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="ee721-142">Sélectionnez hello <b>Notification Services</b> option et hello <b>Windows (WNS)</b> option.</span><span class="sxs-lookup"><span data-stu-id="ee721-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="ee721-143">Puis entrez hello <b>secret d’Application</b> mot de passe dans hello <b>clé de sécurité</b> champ.</span><span class="sxs-lookup"><span data-stu-id="ee721-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="ee721-144">Entrez votre <b>SID du Package</b> valeur obtenue à partir de WNS dans la section précédente de hello, puis cliquez sur <b>enregistrer</b>.</span><span class="sxs-lookup"><span data-stu-id="ee721-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="ee721-145">Votre concentrateur de notification est maintenant configuré toowork avec WNS, et vous avez tooregister de chaînes de connexion hello votre application et envoyez des notifications.</span><span class="sxs-lookup"><span data-stu-id="ee721-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="ee721-146">Se connecter à votre hub de notification d’application toohello</span><span class="sxs-lookup"><span data-stu-id="ee721-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="ee721-147">Dans Visual Studio, cliquez sur la solution de hello, puis cliquez sur **gérer les Packages NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ee721-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="ee721-148">Cela affiche hello **gérer les Packages NuGet** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ee721-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="ee721-149">Recherchez `WindowsAzure.Messaging.Managed` et cliquez sur **installer**et acceptez les conditions d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="ee721-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="ee721-150">Il télécharge, installe et ajoute une bibliothèque de messagerie Azure référence toohello pour Windows à l’aide de hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">package NuGet de WindowsAzure.Messaging.Managed</a>.</span><span class="sxs-lookup"><span data-stu-id="ee721-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="ee721-151">Ouvrez le fichier de projet App.xaml.cs hello et ajoutez hello suit `using` instructions.</span><span class="sxs-lookup"><span data-stu-id="ee721-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="ee721-152">Également, dans App.xaml.cs, ajoutez le code suivant de hello **InitNotificationsAsync** toohello de définition de méthode **application** classe :</span><span class="sxs-lookup"><span data-stu-id="ee721-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="ee721-153">Ce code récupère les URI de canal hello pour une application hello WNS et inscrit ce canal URI avec votre concentrateur de notification.</span><span class="sxs-lookup"><span data-stu-id="ee721-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ee721-154">Assurez-vous que tooreplace hello espace réservé de « nom de votre concentrateur » avec le nom hello du concentrateur de notification hello qui s’affiche dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ee721-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="ee721-155">Remplacez également espace réservé chaîne de connexion hello hello **DefaultListenSharedAccessSignature** chaîne de connexion que vous avez obtenue à partir de hello **stratégies d’accès** page de votre concentrateur de Notification dans un section précédente.</span><span class="sxs-lookup"><span data-stu-id="ee721-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="ee721-156">En haut de hello Hello **OnLaunched** Gestionnaire d’événements dans App.xaml.cs, ajouter hello suivant toohello appel nouvelle **InitNotificationsAsync** méthode :</span><span class="sxs-lookup"><span data-stu-id="ee721-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="ee721-157">Cela garantit ce canal hello QU'URI est enregistré dans votre concentrateur de notification que chaque application hello de temps est lancée.</span><span class="sxs-lookup"><span data-stu-id="ee721-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="ee721-158">Hello de presse **F5** toorun clé hello application.</span><span class="sxs-lookup"><span data-stu-id="ee721-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="ee721-159">Une boîte de dialogue contextuelle qui contient la clé d’inscription de hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="ee721-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="ee721-160">Votre application est maintenant prêt tooreceive des notifications de toast.</span><span class="sxs-lookup"><span data-stu-id="ee721-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="ee721-161">Envoi de notifications</span><span class="sxs-lookup"><span data-stu-id="ee721-161">Send notifications</span></span>
<span data-ttu-id="ee721-162">Vous pouvez tester rapidement la réception de notifications dans votre application en envoyant des notifications Bonjour [Azure Portal](https://portal.azure.com/) à l’aide de hello **envoi Test** bouton sur le concentrateur de notification hello, comme indiqué dans l’écran hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="ee721-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="ee721-163">Les notifications Push sont normalement envoyées dans un service principal tel que Mobile Services ou ASP.NET à l’aide d’une bibliothèque compatible.</span><span class="sxs-lookup"><span data-stu-id="ee721-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="ee721-164">Vous pouvez également utiliser les API REST de hello directement les messages de notification de toosend si une bibliothèque n’est pas disponible pour votre serveur principal.</span><span class="sxs-lookup"><span data-stu-id="ee721-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="ee721-165">Dans ce didacticiel, nous plus de simplicité et simplement montrent le test de votre application cliente en envoyant des notifications à l’aide de hello SDK .NET pour les concentrateurs de notification dans une application console à la place d’un service principal.</span><span class="sxs-lookup"><span data-stu-id="ee721-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="ee721-166">Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers] didacticiel en tant qu’étape suivante de hello pour envoyer des notifications à partir d’un serveur principal d’ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ee721-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="ee721-167">Toutefois, hello méthodes suivantes peut servir pour envoyer des notifications :</span><span class="sxs-lookup"><span data-stu-id="ee721-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="ee721-168">**Interface REST**: peut prendre en charge notification sur toute plateforme principale à l’aide de hello [interface REST](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="ee721-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="ee721-169">**Kit de développement logiciel Microsoft Azure Notification Hubs .NET**: Bonjour Gestionnaire de Package Nuget pour Visual Studio, exécutez [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="ee721-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="ee721-170">**Node.js** : [comment toouse concentrateurs de Notification à partir de Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ee721-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="ee721-171">**Azure Mobile Apps**: pour obtenir un exemple de notifications toosend à partir d’une application Mobile Azure qui est intégré avec Notification Hubs, consultez [ajouter des notifications de push pour les applications mobiles](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="ee721-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="ee721-172">**Java / PHP**: pour obtenir un exemple de comment toosend des notifications à l’aide de hello API REST, consultez « Comment toouse concentrateurs de Notification à partir de Java/PHP » ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="ee721-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="ee721-173">(Facultatif) Envoi de notifications à partir d’une application de console</span><span class="sxs-lookup"><span data-stu-id="ee721-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="ee721-174">toosend des notifications à l’aide d’une application console .NET procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="ee721-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="ee721-175">Solution de hello avec le bouton droit, sélectionnez **ajouter** et **nouveau projet...** , puis sous **Visual C#**, cliquez sur **Windows** et **Application Console**, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="ee721-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="ee721-176">Cette opération ajoute une nouvelle Visual C# toohello solution d’application console.</span><span class="sxs-lookup"><span data-stu-id="ee721-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="ee721-177">Vous pouvez également réaliser cette opération dans une solution distincte.</span><span class="sxs-lookup"><span data-stu-id="ee721-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="ee721-178">Dans Visual Studio, cliquez successivement sur **Outils**, **Gestionnaire de package NuGet** et **Console du gestionnaire de package**.</span><span class="sxs-lookup"><span data-stu-id="ee721-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="ee721-179">Cela affiche hello Package Manager Console dans Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ee721-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="ee721-180">Dans la fenêtre de Console du Gestionnaire de Package de hello, définissez hello **projet par défaut** tooyour nouveau projet d’application console et puis, dans la fenêtre de console hello, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ee721-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="ee721-181">Cette opération ajoute une référence de toohello Azure Notification Hubs SDK à l’aide de hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">package NuGet de concentrateurs Microsoft.Azure.Notification</a>.</span><span class="sxs-lookup"><span data-stu-id="ee721-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="ee721-182">Ouvrez le fichier Program.cs de hello et ajoutez hello suit `using` instruction :</span><span class="sxs-lookup"><span data-stu-id="ee721-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="ee721-183">Bonjour **programme** de classe, ajoutez hello suivant de méthode :</span><span class="sxs-lookup"><span data-stu-id="ee721-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="ee721-184">Assurez-vous que vous utilisez chaîne de connexion hello a **complète** accéder, pas **écouter** accès.</span><span class="sxs-lookup"><span data-stu-id="ee721-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="ee721-185">chaîne d’accès à l’écoute de Hello n’a pas de notifications de toosend d’autorisations.</span><span class="sxs-lookup"><span data-stu-id="ee721-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="ee721-186">Ajouter des lignes Bonjour suivantes de hello **Main** méthode :</span><span class="sxs-lookup"><span data-stu-id="ee721-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="ee721-187">Cliquez sur le projet d’application console hello dans Visual Studio, puis cliquez sur **définir comme projet de démarrage** tooset en tant que projet de démarrage hello.</span><span class="sxs-lookup"><span data-stu-id="ee721-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="ee721-188">Appuyez sur hello **F5** application hello de toorun de clé.</span><span class="sxs-lookup"><span data-stu-id="ee721-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="ee721-189">Vous recevrez une notification toast sur tous les appareils enregistrés.</span><span class="sxs-lookup"><span data-stu-id="ee721-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="ee721-190">Bannière de toast hello cliquant ou appuyant sur charge application hello.</span><span class="sxs-lookup"><span data-stu-id="ee721-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="ee721-191">Vous pouvez trouver toutes les charges utiles de hello pris en charge dans hello [catalogue de toast], [vignette catalogue], et [vue d’ensemble de badge] rubriques sur MSDN.</span><span class="sxs-lookup"><span data-stu-id="ee721-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee721-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ee721-192">Next steps</span></span>
<span data-ttu-id="ee721-193">Dans cet exemple simple, vous avez envoyé notifications diffusion tooall vos appareils Windows à l’aide du portail de hello ou une application console.</span><span class="sxs-lookup"><span data-stu-id="ee721-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="ee721-194">Nous vous recommandons de hello [utiliser Notification Hubs toopush notifications toousers] didacticiel en tant qu’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="ee721-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="ee721-195">Il va vous montrer comment les notifications toosend à partir d’un serveur principal ASP.NET à l’aide de balises tootarget des utilisateurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ee721-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="ee721-196">Si vous souhaitez toosegment vos utilisateurs en groupes d’intérêt, consultez [toosend utiliser Notification Hubs actualités].</span><span class="sxs-lookup"><span data-stu-id="ee721-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="ee721-197">toolearn plus d’informations sur les concentrateurs de Notification, consultez [des conseils de concentrateurs de Notification](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ee721-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[utiliser Notification Hubs toopush notifications toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[toosend utiliser Notification Hubs actualités]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[catalogue de toast]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[vignette catalogue]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[vue d’ensemble de badge]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
